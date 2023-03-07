---
title: Google Analytics - Rastrear visão geral dos dados da fonte de aquisição de usuários
description: Saiba como segmentar seus dados por fonte de aquisição de usuário.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: ad95a03193853eebf2b695cd6f5c3cb5a9837f93
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Segmentação por fonte de aquisição do usuário

>[!NOTE]
>
>O processo abaixo não suporta [!DNL GoogleUniversal Analytics].

A capacidade de segmentar seus dados por fonte de aquisição de usuários é essencial para gerenciar efetivamente seu plano de marketing. Conhecer a fonte de aquisição de novos usuários mostra quais canais geram os melhores retornos e permite que sua equipe aloque dólares de marketing com confiança.

Se você ainda não estiver rastreando as fontes de aquisição de usuários no banco de dados, [!DNL MBI] O pode ajudar você a começar:

## Rastreamento da fonte de aquisição de usuários

O Adobe recomenda dois métodos para rastrear dados de origem de referência com base em sua configuração:

### (Opção 1) Rastrear dados de origem da indicação de ordem via [!DNL Google Analytics E-Commerce] (Incluindo [!DNL Shopify] Lojas)

Se você usar [!DNL Google Analytics E-Commerce] para acompanhar seus dados de pedidos e vendas, você pode usar o [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar os dados de origem de referência de cada pedido. Isso permite segmentar receita e ordens por origem de referência (por exemplo, `utm_source` ou `utm_medium`). Você também tem uma noção das fontes de aquisição de clientes por meio do [!DNL MBI] dimensões personalizadas, como `User's first order source`.

>[!NOTE]
>
>Para usuários do Shopify**: Ativar [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) antes de conectar seu [!DNL Google Analytics E-Commerce] conta para [!DNL MBI].

### (Opção 2) Salvar [!DNL Google Analytics]Dados da fonte de aquisição &#39; no banco de dados

Este artigo explica como economizar [!DNL Google Analytics] informações do canal de aquisição no seu próprio banco de dados, ou seja, o `source`, `medium`, `term`, `content`, `campaign`, e `gclid` parâmetros que estavam presentes na primeira visita de um usuário ao seu site. Para obter uma explicação sobre esses parâmetros, verifique a [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Em seguida, explore algumas análises de marketing avançadas que podem ser executadas com essas informações no [!DNL MBI].

#### Por quê?

Se você estiver apenas observando o padrão [!DNL Google Analytics] métricas de conversão e aquisição, você não está obtendo o panorama completo. Embora ver o número de conversões de pesquisa orgânica versus pesquisa paga seja interessante, o que você pode fazer com essa informação? Você deveria gastar mais dinheiro em pesquisa paga? Isso depende do valor dos clientes provenientes desse canal, o que não é algo que o Google Analytics oferece.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) atenua esse problema armazenando dados de transação no [!DNL Google Analytics], mas essa solução não funciona em sites que não sejam de comércio eletrônico. Além disso, certas ferramentas, como a análise de coorte, não são fáceis de fazer no [!DNL Google Analytics] interface.

E se você quiser enviar um email para um acordo de acompanhamento de todos os clientes adquiridos de uma determinada campanha de email? Ou integrar os dados de aquisição ao seu sistema de CRM? Isso é impossível em [!DNL Google Analytics] - na verdade, é contra os Termos de Serviço para [!DNL Google Analytics] para armazenar quaisquer dados que identifiquem uma pessoa. Mas você mesmo pode armazenar esses dados.

#### O Método

[!DNL Google Analytics] armazena informações de referência do visitante em um cookie chamado `__utmz`. Depois que este cookie for definido (pela variável [!DNL Google Analytics] tracking code), o conteúdo será enviado com cada solicitação subsequente desse usuário ao seu domínio. Então no PHP, por exemplo, você pode checar o conteúdo de `$_COOKIE['__utmz']` e você verá uma string parecida com esta:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Claramente, há alguns dados da fonte de aquisição codificados na string. Isso é testado para confirmar que essa é a fonte de aquisição mais recente do visitante e os dados de campanha associados. Agora você precisa saber como extrair os dados. Felizmente, Justin Cutroni já descreveu como essa codificação funciona e compartilhou um código JavaScript para extrair as informações principais.

Esse código foi traduzido em um [Biblioteca PHP hospedada no github](https://github.com/RJMetrics/referral-grabber-php). Para usar a biblioteca, `include` uma referência a `ReferralGrabber.php` e, em seguida, chame

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

O resultado `$data` matriz é um mapa das chaves `source`, `medium`, `term`, `content`, `campaign`, `gclid`, e seus respectivos valores.

A Adobe recomenda adicionar uma tabela ao banco de dados chamada, por exemplo, `user_referral`, com as colunas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Sempre que um usuário se inscrever, capture as informações de referência e armazene-as nesta tabela.

#### Como usar estes dados

Agora que você está salvando a fonte de aquisição do usuário, como você pode usá-la?

Suponha que você esteja usando um banco de dados SQL e tenha um `users` com a seguinte estrutura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | orgânico |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direto | - |
| 4 | jess@ghi.com | 2012-01-26 | referência | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | outro | orgânico |
| ... | ... | ... | ... | ... |

Para começar, você pode contar o número de usuários provenientes de cada canal de referência executando a seguinte query no banco de dados:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

O resultado é semelhante a:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direto | 156 |
| referência | 55 |
| outro | 16 |

Isso é interessante, mas de uso limitado. O que você realmente gostaria de saber é:

* a taxa de crescimento desses números ao longo do tempo
* a quantidade de receita gerada por cada fonte de aquisição
* a [análise de coorte](https://en.wikipedia.org/wiki/Cohort_analysis) de usuários provenientes de cada origem
* a probabilidade de um usuário de um desses canais retornar como um cliente no futuro.

As consultas necessárias para fazer essas análises são complexas. De posse dessas informações, você pode determinar seus canais de aquisição mais lucrativos e concentrar o tempo e o dinheiro de marketing de acordo.

### Relacionados

* **[Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)**
* **[Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)**
* **[Como o [!DNL Google Analytics] A atribuição UTM funciona?](../analysis/utm-attributes.md)**
