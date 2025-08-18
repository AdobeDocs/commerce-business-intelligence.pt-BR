---
title: Google Analytics - Rastrear Visão geral dos dados do Source de aquisição de usuários
description: Saiba como segmentar seus dados por fonte de aquisição de usuário.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Segmentação por fonte de aquisição do usuário

>[!NOTE]
>
>O processo abaixo não oferece suporte a [!DNL Google Universal Analytics].

A capacidade de segmentar seus dados por fonte de aquisição de usuários é essencial para gerenciar efetivamente seu plano de marketing. Conhecer a fonte de aquisição de novos usuários mostra quais canais geram os melhores retornos e permite que sua equipe aloque dólares de marketing com confiança.

Se você ainda não estiver rastreando as fontes de aquisição de usuários no banco de dados, o [!DNL Adobe Commerce Intelligence] pode ajudá-lo a começar:

## Rastreamento da fonte de aquisição de usuários

O [!DNL Adobe] recomenda dois métodos para rastrear os dados da fonte de referência com base na sua configuração:

### (Opção 1) Rastrear dados de origem de referência de ordem via [!DNL Google Analytics E-Commerce]

Se você usa o [!DNL Google Analytics E-Commerce] para acompanhar seus dados de pedidos e vendas, você pode usar o [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar os dados de origem de referência de cada pedido. Isso permite segmentar receita e pedidos por fonte de referência (por exemplo, `utm_source` ou `utm_medium`). Você também tem uma noção das fontes de aquisição de clientes por meio de [!DNL Commerce Intelligence] dimensões personalizadas, como `User's first order source`.

### (Opção 2) Salvando os dados da fonte de aquisição [!DNL Google Analytics] em seu banco de dados

Este tópico explica como salvar as informações do canal de aquisição do [!DNL Google Analytics] no seu próprio banco de dados, ou seja, os parâmetros `source`, `medium`, `term`, `content`, `campaign` e `gclid` que estavam presentes na primeira visita de um usuário ao seu site. Para obter uma explicação sobre esses parâmetros, consulte a [[!DNL Google Analytics] documentação](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Em seguida, você explora algumas das análises de marketing avançadas que podem ser executadas com essas informações no [!DNL Commerce Intelligence].

#### Por quê?

Se você estiver apenas olhando para as métricas padrão de conversão e aquisição do [!DNL Google Analytics], não está obtendo uma visão completa. Embora ver o número de conversões de pesquisa orgânica versus pesquisa paga seja interessante, o que você pode fazer com essa informação? Você deveria gastar mais dinheiro em pesquisa paga? Isso depende do valor dos clientes provenientes desse canal, que não é algo que a Google Analytics fornece.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) atenua esse problema armazenando dados de transação em [!DNL Google Analytics], mas essa solução não funciona para sites que não sejam de comércio eletrônico. Além disso, certas ferramentas, como a análise de coorte, não são fáceis de fazer na interface [!DNL Google Analytics].

E se você quiser enviar um email para um acordo de acompanhamento de todos os clientes adquiridos de uma determinada campanha de email? Ou integrar os dados de aquisição ao seu sistema de CRM? Isso é impossível em [!DNL Google Analytics] - na verdade, é contra os Termos de Serviço para [!DNL Google Analytics] armazenar quaisquer dados que identifiquem um indivíduo. Mas você mesmo pode armazenar esses dados.

#### O Método

[!DNL Google Analytics] armazena as informações de referência do visitante em um cookie chamado `__utmz`. Depois que este cookie for definido (pelo código de rastreamento [!DNL Google Analytics]), seu conteúdo será enviado com cada solicitação subsequente desse usuário para o seu domínio. Assim, no PHP, por exemplo, você poderia checar o conteúdo de `$_COOKIE['__utmz']` e você veria uma string parecida com esta:

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Claramente, há alguns dados da fonte de aquisição codificados na string. Isso é testado para confirmar que essa é a fonte de aquisição mais recente do visitante e os dados de campanha associados. Agora você precisa saber como extrair os dados.

Este código foi traduzido em uma [biblioteca PHP hospedada no github](https://github.com/RJMetrics/referral-grabber-php). Para usar a biblioteca, `include` uma referência a `ReferralGrabber.php` e chame

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

A matriz `$data` retornada é um mapa das chaves `source`, `medium`, `term`, `content`, `campaign`, `gclid` e seus respectivos valores.

A Adobe recomenda adicionar uma tabela ao banco de dados chamada, por exemplo, `user_referral`, com as colunas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Sempre que um usuário se inscrever, capture as informações de referência e armazene-as nesta tabela.

#### Como usar estes dados

Agora que você está salvando a fonte de aquisição do usuário, como você pode usá-la?

Suponha que você esteja usando um banco de dados SQL e tenha uma tabela `users` com a seguinte estrutura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 24/01/2012 | google | orgânico |
| 2 | jim@abc.com | 24/01/2012 | google | cpc |
| 3 | joe@def.com | 25/01/2012 | direto | - |
| 4 | jess@ghi.com | 26/01/2012 | referência | techcrunch.com |
| 5 | jen@ghi.net | 30/01/2012 | outro | orgânico |
| .. | .. | .. | .. | .. |

Para começar, você pode contar o número de usuários provenientes de cada canal de referência executando a seguinte query no banco de dados:

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

O resultado é semelhante a:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direto | 156 |
| referência | 55 |
| outro | 16 |

Isso é interessante, mas de uso limitado. O que você realmente gostaria de saber é:

* A taxa de crescimento desses números ao longo do tempo
* A quantidade de receita gerada por cada fonte de aquisição
* Uma [análise de coorte](https://en.wikipedia.org/wiki/Cohort_analysis) de usuários provenientes de cada origem
* A probabilidade de um usuário de um desses canais retornar como um cliente no futuro

As consultas necessárias para fazer essas análises são complexas. De posse dessas informações, você pode determinar seus canais de aquisição mais lucrativos e concentrar o tempo e o dinheiro de marketing de acordo.

### Relacionados

* **[Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)**
* **[Conectar sua [!DNL Google Adwords] conta](../importing-data/integrations/google-adwords.md)**
* **[Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)**
* **[Como funciona a  [!DNL Google Analytics] atribuição de UTM?](../analysis/utm-attributes.md)**
