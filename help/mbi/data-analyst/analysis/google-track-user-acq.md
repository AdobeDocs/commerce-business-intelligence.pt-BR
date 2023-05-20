---
title: Visão geral dos dados de aquisição do usuário do Google Analytics Origem de rastreamento
description: Aprenda a segmentor seus dados por usuário fonte atração.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: af1e3839839b4c419beabb0cc666c996ea2179d4
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# Segmentação por fonte de atração usuário

>[!NOTE]
>
>O processo abaixo não suporta [!DNL Google Universal Analytics] .

A capacidade de segmento seus dados por usuário atração fonte é crítico para gerenciar o plano de marketing de maneira eficaz. Conhecer a fonte de atração de novos usuários mostra quais canais geram as principais Devoluções e permite que sua equipe aloque marketing reais com confiança.

Se você ainda não estiver rastreando as fontes de aquisição de usuários no banco de dados, [!DNL Adobe Commerce Intelligence] O pode ajudar você a começar:

## Rastreamento da fonte de aquisição de usuários

[!DNL Adobe] A recomenda dois métodos para rastrear dados de origem de referência com base na sua configuração:

### (Opção 1) Rastrear dados de origem da indicação de ordem via [!DNL Google Analytics E-Commerce] (Incluindo [!DNL Shopify] Lojas)

Se você usar [!DNL Google Analytics E-Commerce] para acompanhar seus dados de pedidos e vendas, você pode usar o [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar os dados de origem de referência de cada pedido. Isso permite segmentar receita e ordens por origem de referência (por exemplo, `utm_source` ou `utm_medium`). Você também tem uma noção de conquista de cliente fontes por meio [!DNL Commerce Intelligence] de dimensões personalizadas, `User's first order source` como.

>[!NOTE]
>
>**Para usuários** do Shopify: Ative [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) antes de conectar o [!DNL Google Analytics E-Commerce] conta [!DNL Commerce Intelligence] .

### (Opção 2) Salvar [!DNL Google Analytics] os dados de origem do atração no banco de dados

Este tópico explica como salvar [!DNL Google Analytics] as informações do atração canal no próprio banco de dados, ou seja, os `source` parâmetros, `term` `medium` ,, `content` `campaign` , e `gclid` que estavam presentes na primeira visita do usuário do site. Para obter uma explicação sobre esses parâmetros, verifique a [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Em seguida, explore algumas análises de marketing avançadas que podem ser executadas com essas informações no [!DNL Commerce Intelligence].

#### Por quê?

Se você estiver apenas olhando para as métricas de conversão e atração padrão [!DNL Google Analytics] , não estará obtendo a figura inteira. Ao ver o número de conversões de pesquisa orgânica versus pesquisa paga é interessante, o que você pode fazer com essas informações? Você deve dedicar mais dinheiro no pesquisa paga? Isso depende do valor dos clientes que vêm por esse canal, que não é algo que Google Analytics fornece.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) atenua essa problema ao armazenar dados de [!DNL Google Analytics] transação, mas esta solução não funciona para sites sem comércio eletrônico. Além disso, algumas ferramentas curtir coorte análise não são fáceis de fazer na [!DNL Google Analytics] interface.

E se você quiser enviar por e-mail uma dose de seguir para todos os clientes adquiridos de um certo campanha de email? Ou integre atração dados com seu sistema de CRM? Isso é impossível [!DNL Google Analytics] , de fato, é contra os termos de serviço para [!DNL Google Analytics] armazenamento qualquer dado que identifique um indivíduo. No entanto, é possível armazenamento esses dados.

#### O método

[!DNL Google Analytics] armazena visitante referência informações em um cookie chamado `__utmz` . Depois que essa cookie é definida (por [!DNL Google Analytics] código de rastreamento), seu conteúdo será enviado a cada solicitação subsequente para o seu domínio a partir dessa usuário. Portanto, no PHP, por exemplo, você pode verificar o conteúdo de `$_COOKIE['__utmz']` e verá uma String que parece algo curtir isso:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Há claramente alguns atração dados de origem codificados na String. Isso é testado para confirmar se essa é a fonte de atração mais recente do visitante e os dados campanha associados. Agora você precisa saber como extrair os dados.

Esse código foi traduzido em um [Biblioteca PHP hospedada no github](https://github.com/RJMetrics/referral-grabber-php). Para usar a biblioteca, `include` uma referência a `ReferralGrabber.php` e, em seguida, chame

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

O resultado `$data` matriz é um mapa das chaves `source`, `medium`, `term`, `content`, `campaign`, `gclid`, e seus respectivos valores.

[!DNL Adobe] A recomenda adicionar uma tabela ao banco de dados chamada, por exemplo, `user_referral`, com as colunas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Sempre que um usuário se inscrever, capture as informações de referência e armazene-as nesta tabela.

#### Como usar estes dados

Agora que você está salvando usuário fonte de atração, como é possível usá-la?

Suponha que você esteja usando um banco de dados SQL e tenha um `users` com a seguinte estrutura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | Google | orgânico |
| 2 | jim@abc.com | 2012-01-24 | google | Cpc |
| 3 | joe@def.com | 2012-01-25 | direto | - |
| 4 | jess@ghi.com | 2012-01-26 | referência | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | Outros | Orgânico |
| ... | ... | ... | ... | ... |

Para começar, você pode contar o número de usuários provenientes de cada canal de referência executando a seguinte query no banco de dados:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

O resultado parece algo curtir isso:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direto | 156 |
| referência | 55 |
| Outros | 16 |

Isso é interessante, mas de uso limitado. O que você realmente curtir saber é:

* a taxa de crescimento desses números ao longo do tempo
* a quantidade de receita geradas por cada fonte de atração
* uma [ análise ](https://en.wikipedia.org/wiki/Cohort_analysis) coorte dos usuários que vêm de cada fonte
* a probabilidade de um usuário de um desses canais ser retornado como um cliente no futuro.

As consultas necessárias para fazer essas análises são complexas. De posse dessas informações, você pode determinar seus canais de aquisição mais lucrativos e concentrar o tempo e o dinheiro de marketing de acordo.

### Relacionados

* **[Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)**
* **[Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)**
* **[Como o  [!DNL Google Analytics]  UTM atribuição funciona?](../analysis/utm-attributes.md)**
