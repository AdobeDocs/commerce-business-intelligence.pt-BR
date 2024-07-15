---
title: Identificação de suas fontes e canais de marketing mais valiosos
description: Saiba mais sobre alguns relatórios que você pode usar para descobrir seus canais de marketing mais valiosos.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identificar fontes de marketing bem-sucedidas

Você pesquisou seu público, criou sua campanha, investiu em alguns canais de marketing. Agora que já passou algum tempo, como esses canais estão se saindo? Qual canal trouxe os usuários mais novos? Qual fonte contribuiu mais para sua receita total?

Com o [!DNL Adobe Commerce Intelligence], você pode facilmente segmentar sua receita e usuários por fonte de referência, quer corresponda ao [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) ou a campos de dados personalizados. Essa segmentação permite encontrar seus canais com melhor desempenho e investir melhor seu orçamento de marketing.

Este tópico explora alguns relatórios que você pode usar para descobrir seus canais de marketing mais valiosos:

* [Novos usuários por origens](#newusersbysource)
* [Receita média vitalícia por origem do usuário](#avglifetimerev)
* [Valor médio de pedido por origem de usuário](#avgorderval)
* [Receita por data e origens de registro do usuário](#revbyregdateandsource)
* [Repetir ordens por origem do usuário](#repeatordersbysource)

## Pré-requisitos {#prereqs}

Para criar as análises neste tópico, é necessário acesso aos dados de aquisição de marketing/fonte de referência. Se você ainda não estiver rastreando, será necessário trazer [dados de origem da referência do pedido de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) para [!DNL Adobe Commerce Intelligence] antes de continuar. Além disso, adicionar informações do dispositivo do usuário às análises permite que você veja qual tecnologia suas indicações estão usando.

## Novos usuários por origem {#newusersbysource}

Avaliar o desempenho das fontes de referência é fundamental para determinar seus canais mais valiosos. Este relatório mostra o número de usuários recém-registrados, por fonte de aquisição, ao longo do tempo, permitindo, assim, rastrear o desempenho das fontes de referência na aquisição de novos usuários registrados.

Para criar este relatório no [Report Builder](../../tutorials/using-visual-report-builder.md), adicione a métrica **Novos usuários** (ou uma métrica equivalente que conte o número de novos usuários ao longo do tempo) ao relatório. Em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] como o período de registro que você deseja analisar.
1. Defina o [!UICONTROL Interval] como mensal.
1. Defina [!UICONTROL Group By] como fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o `stacked columns` [!UICONTROL chart type].

Veja uma apresentação visual:

![Criando um novo relatório de usuários por origem.](../../assets/New_Users_by_source.gif)

## Receita média vitalícia por origem do usuário {#avglifetimerev}

Encontrar os canais que trazem novos usuários é importante, mas qual é o valor geral dessas indicações? Este relatório mostra a receita média por vida útil dos usuários de fontes de aquisição específicas ao longo do tempo. Em outras palavras, isso permite ver se os usuários adquiridos de uma origem específica gastam mais com você durante a vida útil do que um grupo de usuários adquiridos de uma origem diferente.

Para criar este relatório no Report Builder, adicione a métrica **Receita média ao longo da vida** ao relatório. Em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] com o período que deseja analisar.
1. Defina o [!UICONTROL Interval] como mensal.
   [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o tipo `line chart`.

Veja uma apresentação visual:

![Criando uma receita média vitalícia por origem de usuário](../../assets/Lifetime_revenue_by_user_source.gif).

Este exemplo considera apenas a receita vitalícia, mas você também pode replicar essa análise para observar [!UICONTROL Number of orders] ou [!UICONTROL Distinct buyers] por fonte de referência.

## Valor médio de pedido por origem de usuário {#avgorderval}

Para ter uma ideia melhor de quanto dinheiro os usuários de uma fonte de aquisição específica gastam, você pode criar um relatório que observa seu valor médio de pedido. Isso permite rastrear se os usuários adquiridos de uma determinada origem gastam mais por pedido do que os usuários de outra origem.

Para criar este relatório no Report Builder, adicione a métrica **Valor médio de pedido** e faça o seguinte:

1. Defina o [!UICONTROL Time Period] como o período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] como mensal.
1. Defina [!UICONTROL Group By] como fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o tipo de gráfico **colunas empilhadas**.

Veja uma apresentação visual:

![Criando um relatório de valor médio de pedido por origem de usuário.](../../assets/Average_order_value_by_source.gif)

## Receita total por data e origem de registro do usuário {#revbyregdateandsource}

A análise de receita da duração que foi abordada anteriormente permite que você observe a receita média da duração de vida dos usuários adquiridos de diferentes fontes, mas e quanto à receita total da duração? Esse relatório permite identificar quantos usuários de receita geral registrados durante um horário específico e de uma origem específica são gerados.

Para criar este relatório no Report Builder, adicione a métrica `Revenue by user registration date`. Se você ainda não [criou esta métrica](../../data-user/reports/ess-manage-data-metrics.md), faça isso replicando a métrica `Revenue` e alterando a `time stamp` para a `creation date` do Usuário. Depois de adicionar a métrica, faça o seguinte:

1. Defina o [!UICONTROL Time Period] como o período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] como mensal.
1. Defina [!UICONTROL Group By] como fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o tipo de gráfico `stacked columns`.

Veja uma apresentação visual:

![Criando uma receita total por data de registro do usuário e relatório de origem.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repetir ordens por origem do usuário {#repeatordersbysource}

O relatório Average order value mostra, em média, quantos usuários adquiridos de uma origem específica gastam ao fazer um pedido. No entanto, esse relatório não mostra se esses mesmos usuários são clientes recorrentes. Mas com as origens Repetir ordens por usuários, você pode ver se os usuários de uma determinada origem fazem compras mais ou menos repetidas.

Para criar este relatório no [Report Builder](../../tutorials/using-visual-report-builder.md), adicione a métrica **Número de pedidos** e faça o seguinte:

1. Defina o [!UICONTROL Time Period] como o período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] como mensal.
1. Adicione um [!UICONTROL filter] para que somente usuários com pedidos repetidos sejam incluídos:

   Número de ordem do usuário maior que 1

1. Defina [!UICONTROL Group By] como fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o tipo de gráfico `stacked columns`.

Veja uma apresentação visual:

![Criando um relatório de ordens repetidas por origem do usuário.](../../assets/Repeat_orders_by_user_source.gif)


## Encapsulamento {#wrapup}

Este tópico abordou apenas algumas análises que você pode usar para analisar o valor de seus canais de aquisição e marketing, mas isso é apenas a ponta do iceberg.

## Relacionados {#related}

* [Rastreando origem de referência de ordem via  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Conectando sua conta  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Compilando  [!DNL Google ECommerce] dimensões com pedidos e dados do cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Práticas recomendadas para marcação UTM em [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
