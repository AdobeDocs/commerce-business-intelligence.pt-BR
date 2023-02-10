---
title: Google Analytics - Rastrear a visão geral dos dados da fonte de aquisição do usuário
description: Saiba como segmentar seus dados por fonte de aquisição do usuário.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# Segmentação por fonte de aquisição de usuário

>[!NOTE]
>
>O processo abaixo não é compatível [!DNL GoogleUniversal Analytics].

A capacidade de segmentar seus dados por fonte de aquisição do usuário é fundamental para gerenciar efetivamente seu plano de marketing. Conhecer a fonte de aquisição de novos usuários mostra quais canais produzem os principais retornos e permite que sua equipe aloque dólares de marketing com confiança.

Se você ainda não estiver rastreando as fontes de aquisição do usuário no seu banco de dados, [!DNL MBI] O pode ajudá-lo a começar:

## Rastreamento da fonte de aquisição do usuário

Recomendamos dois métodos para rastrear os dados da fonte de referência com base em sua configuração:

### (Opção 1) Rastrear os dados fonte de referência do pedido via [!DNL Google Analytics E-Commerce] (Incluindo [!DNL Shopify] Lojas)

Se você aproveitar [!DNL Google Analytics E-Commerce] para rastrear seus pedidos e dados de vendas, você pode utilizar nosso [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar os dados de origem de referência de cada pedido. Isso permitirá segmentar a receita e os pedidos por fonte de referência (por exemplo, `utm_source` ou `utm_medium`) e também ter uma ideia das fontes de aquisição do cliente por meio de [!DNL MBI] dimensões personalizadas, como `User's first order source`.

>[!NOTE]
>
>Para usuários do Shopify**: Ligar [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) antes de conectar [!DNL Google Analytics E-Commerce] para [!DNL MBI].

### (Opção 2) Salvando [!DNL Google Analytics]&#39; dados da fonte de aquisição no seu banco de dados

Neste artigo, explicaremos como salvar [!DNL Google Analytics] informações do canal de aquisição em seu próprio banco de dados - ou seja, o `source`, `medium`, `term`, `content`, `campaign`e `gclid` parâmetros que estavam presentes na primeira visita de um usuário ao seu site. Para obter uma explicação sobre esses parâmetros, verifique o [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). Em seguida, exploraremos algumas análises de marketing poderosas que podem ser realizadas com essas informações em [!DNL MBI].

#### Por quê?

Se você estiver apenas observando o padrão [!DNL Google Analytics] métricas de conversão e aquisição, você não está obtendo a imagem inteira. Embora ver o número de conversões da pesquisa orgânica versus a pesquisa paga seja interessante, o que você pode fazer com essa informação? Você deveria gastar mais dinheiro em busca paga? Isso depende do valor dos clientes que vêm desse canal, o que não é algo que o Google Analytics fornece.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) O reduz esse problema armazenando dados de transação no [!DNL Google Analytics], mas essa solução não funciona para sites que não são de comércio eletrônico e algumas ferramentas, como a análise de coorte, não são fáceis de fazer no [!DNL Google Analytics] interface.

E se você quiser enviar por email um negócio de acompanhamento para todos os clientes adquiridos de uma determinada campanha de email? Ou integrar os dados de aquisição ao seu sistema de CRM? Isso é impossível em [!DNL Google Analytics] - na verdade, é contra os Termos de Serviço para [!DNL Google Analytics] para armazenar quaisquer dados que identifiquem um indivíduo.  Mas isso não significa que você mesmo não possa armazenar esses dados.

#### O método

[!DNL Google Analytics] armazena informações de referência do visitante em um cookie chamado `__utmz`. Depois que este cookie for definido (pela variável [!DNL Google Analytics] código de rastreamento), seu conteúdo será enviado com cada solicitação subsequente para seu domínio desse usuário. Assim, em PHP, por exemplo, você pode verificar o conteúdo de `$_COOKIE['__utmz']` E vocês veriam uma corda que se parece com isto:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Há claramente alguns dados da fonte de aquisição codificados na string, e testamos para confirmar que essa é a fonte de aquisição mais recente do visitante e os dados de campanha associados. Agora precisamos apenas de saber como extrair os dados. Por sorte, Justin Cutroni descreveu anteriormente como essa codificação funciona e compartilhou algum código javascript para extrair as informações principais.

Pegamos esse código e o traduzimos em um [biblioteca PHP hospedada no github](https://github.com/RJMetrics/referral-grabber-php).   Para usar a biblioteca , `include` uma referência a `ReferralGrabber.php` e depois chame

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

O retorno `$data` matriz será um mapa das chaves `source`, `medium`, `term`, `content`, `campaign`, `gclid` e os respectivos valores.

Recomendamos adicionar uma nova tabela ao seu banco de dados chamado, por exemplo, `user_referral`, com as colunas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Sempre que um usuário se inscrever, capture as informações da referência e armazene-as nessa tabela.

#### Como usar esses dados

Agora que estamos salvando a fonte de aquisição do usuário, como podemos usá-la?

Vamos supor que estamos usando um banco de dados SQL e temos um `users` com a seguinte estrutura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | orgânico |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direct | - |
| 4 | jess@ghi.com | 2012-01-26 | referência | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | other | orgânico |
| ... | ... | ... | ... | ... |

Para começar, podemos contar o número de usuários provenientes de cada canal de referência executando a seguinte query no seu banco de dados:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

O resultado será algo assim:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| referência | 55 |
| other | 16 |

Isso é interessante, mas de uso limitado. O que nós realmente gostaríamos de saber é a taxa de crescimento desses números ao longo do tempo, a quantidade de receita gerada por cada fonte de aquisição, uma [análise de coorte](http://cohortanalysis.com/) de usuários provenientes de cada fonte e a probabilidade de um usuário de um desses canais retornar como cliente no futuro. As consultas necessárias para fazer essas análises são complexas - por isso criamos [!DNL MBI]. Munidos dessas informações, podemos determinar nossos canais de aquisição mais rentáveis e concentrar nosso tempo de marketing e dinheiro de acordo.

### Relacionado

* **[Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)**
* **[Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)**
* **[Como [!DNL Google Analytics] A atribuição de UTM funciona?](../analysis/utm-attributes.md)**
