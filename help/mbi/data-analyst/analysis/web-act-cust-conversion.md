---
title: Analisando a atividade do site e as taxas de conversão do cliente
description: Saiba como configurar um painel que rastreará a atividade de seu site, incluindo exibições de página, sessões e usuários, bem como o índice de conversão do cliente ao longo do tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Analisar atividade do site

[!DNL MBI] O permite integrar facilmente os dados de custo de publicidade ao restante dos dados. Isso não somente permite entender a atividade do site, como também permite derivar a porcentagem de visitantes do site que se tornam usuários registrados ou fazem uma compra.

Neste artigo, demonstramos como configurar um painel que rastreará a atividade de seu site - incluindo exibições de página, sessões e usuários -, bem como a taxa de conversão do cliente ao longo do tempo.

## Pré-requisitos

**Importe os dados de custo de publicidade** - Conectar [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) para [!DNL MBI] - isso sincronizará automaticamente o [!DNL AdWords] gasto em BI.

**Rastrear dados do canal de aquisição do usuário** - Para amarrar o seu [!DNL Google AdWords] dados para pedidos específicos no banco de dados, precisamos [rastrear a aquisição do usuário](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce], permitindo conectar cada pedido com uma fonte e meio utm.

## Campanhas de aquisição do usuário

Essa coleção de relatórios é criada usando o seguinte:

* Métricas que são geradas automaticamente quando você conecta seu [!DNL Google AdWords] dados
* Métricas básicas que já devem estar disponíveis em sua conta, como `Number of orders` e `New users`
* Dimension criadas ao ingressar em seu [!DNL Google Analytics Ecommerce] dados para o banco de dados, como a origem utm do pedido e o meio utm do pedido. Entre em contato com a equipe de suporte se esses campos não estiverem disponíveis na sua conta

## Criar relatórios

**Comece criando um relatório que mostra o número de exibições de página, sessões e usuários ao longo do tempo:**

1. Crie um novo relatório.
1. Clique em **[!UICONTROL Add Metric]**, em seguida, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Page Views`.
1. Adicione outra métrica, novamente passando o mouse sobre a variável [!DNL Google Analytics] seção, desta vez selecionando `Sessions`.
1. Adicione uma terceira métrica, novamente usando o mouse sobre a variável [!DNL Google Analytics] seção, desta vez selecionando `Users`.
1. Agora altere seu período para um intervalo em movimento, de 31 dias atrás para 1 dia atrás, e ajuste o intervalo de tempo para `by day`.
1. Dê um nome ao seu relatório (por exemplo, `Page views, sessions and users by day`) e clique em **[!UICONTROL Save]**.

**Nosso segundo relatório analisará o número de exibições de página no ano passado:**

1. Crie um novo relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Exibições de página_.
1. Altere seu período para um intervalo em movimento, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Dê um nome ao seu relatório, como `Page views by month,` e clique em **[!UICONTROL Save]**.

**O terceiro gráfico observará a taxa de rejeição no ano passado:**

1. Crie um novo relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Taxa de rejeição_.
1. Altere seu período para um intervalo em movimento, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Dê um nome ao seu relatório, como `Bounce rate by month`e clique em **[!UICONTROL Save]**.

**Agora, verifique a duração média da sessão de novos visitantes em comparação aos visitantes recorrentes:**

1. Crie um novo relatório.
1. Clique em **UICONTROL Adicionar métrica**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Average Session Length`.
1. Altere seu período para um intervalo em movimento, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`?
1. Adicione um `Group by` e selecione `New or returning visitor`.  Verifique a `Show All` Caixa; em seguida, clique em **[!UICONTROL Apply]**.
1. Dê um nome ao seu relatório, como `Average session length`e clique em **[!UICONTROL Save]**.

**Em seguida, consulte os principais domínios de referência nos últimos 30 dias:**

1. Crie um novo relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Sessions`.
1. Altere seu período para um intervalo em movimento, de 31 dias atrás para 1 dia atrás, e ajuste o intervalo de tempo para `none`.
1. Adicione um `Group by` e selecione `ga:source`.  Verifique a _Mostrar tudo_ Caixa; em seguida, clique em **[!UICONTROL Apply]**.
1. Adicionar outro `group by` e selecione `ga:medium`. Novamente, verifique o `Show All` Caixa; em seguida, clique em **[!UICONTROL Apply]**.
1. Dê um nome ao seu relatório, como `Top 20 Referring Domains, 30 Days`e clique em **[!UICONTROL Save]**.

**Finalmente, veja a conversão:**

1. Crie um novo relatório.
1. Adicione as seguintes métricas:

* `New users`
   * Clique em **[!UICONTROL Hide]** abaixo do nome da métrica

* `Number of orders`
   * Adicionar um filtro para `Customer's order number` = 1 e clique **[!UICONTROL Apply]**
   * Renomeie a métrica clicando no nome da métrica, chamando-a `Number of first orders`e clique em **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** a métrica

* `Users`
   * **[!UICONTROL Hide]** a métrica
   * Alterar o período de tempo para `24 months ago to now`e ajuste o intervalo de tempo para `by month`.
   * Adicione as seguintes fórmulas clicando em **[!UICONTROL Formula]**.
   * A/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Registration conversion`
   * B/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `First order conversion`
   * C/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Any order conversion`

* Agora dê um nome ao seu relatório, como `Conversion by month`e, em seguida, clique em **[!UICONTROL Save]**.

## Próximas etapas

Agora que você tem acesso aos dados em seu tráfego da Web e taxas de conversão, você pode começar a usar esses recursos para impulsionar decisões comerciais. Quais sites são os melhores em impulsionar tráfego para seu site?  Quais das suas campanhas são mais eficazes para adquirir clientes com o alto valor vitalício?

À medida que você ajusta os gastos com publicidade e a estratégia de marketing, pode continuar a acompanhar os resultados em [!DNL MBI], iterando neste painel para atender às prioridades em evolução de sua empresa.
