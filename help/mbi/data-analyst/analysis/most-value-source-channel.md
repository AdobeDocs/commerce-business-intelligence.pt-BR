---
title: Identificando suas fontes e canais de marketing mais valiosos
description: Saiba mais sobre alguns relatórios que você pode usar para descobrir seus canais de marketing mais valiosos.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# Identificar fontes de marketing bem-sucedidas

Você pesquisou seu público, criou sua campanha, investiu em alguns canais de marketing. Agora que já passou algum tempo, como esses canais estão se saindo? Que canal trouxe mais usuários novos? Qual fonte contribuiu mais para sua receita total?

Com [!DNL MBI], você pode segmentar facilmente sua receita e seus usuários por fonte de referência, seja ela [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) ou campos de dados personalizados. Essa segmentação permitirá encontrar seus canais de melhor desempenho e investir melhor seu orçamento de marketing.

Neste artigo, exploramos alguns relatórios que podem ser usados para descobrir seus canais de marketing mais valiosos:

* [Novos usuários por fontes](#newusersbysource)
* [Receita vitalícia média por origem de usuário](#avglifetimerev)
* [Valor médio de pedido por origem de usuário](#avgorderval)
* [Receita por data de registro do usuário e fontes](#revbyregdateandsource)
* [Repetir pedidos por origem de usuário](#repeatordersbysource)

## Pré-requisitos {#prereqs}

Para criar as análises neste artigo, você precisa acessar os dados de aquisição/fonte de referência de marketing. Se você ainda não estiver rastreando, será necessário trazer [dados de origem de referência de pedido de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) em [!DNL MBI] antes de continuar. Além disso, adicionar as informações do dispositivo do usuário às suas análises permite que você veja a tecnologia que suas referências estão usando.

## Novos usuários por origem {#newusersbysource}

A avaliação do desempenho das fontes de referência é fundamental para determinar seus canais mais valiosos. Este relatório mostra o número de usuários recém-registrados, por fonte de aquisição, ao longo do tempo, permitindo rastrear o desempenho das fontes de referência na aquisição de novos usuários registrados.

Para criar este relatório na [Report Builder](../../tutorials/using-visual-report-builder.md), adicione o **Novos usuários** métrica (ou uma métrica equivalente que conta o número de novos usuários ao longo do tempo) para o relatório. Em seguida, faça o seguinte:

1. Defina as [!UICONTROL Time Period] ao período de registro que deseja analisar.
1. Defina as [!UICONTROL Interval] mensalmente.
1. Definir [!UICONTROL Group By] para a fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Neste exemplo, usamos o `stacked columns` [!UICONTROL chart type].

Aqui está uma apresentação visual:

![Criação de um relatório Novos usuários por origem .](../../assets/New_Users_by_source.gif)

## Receita vitalícia média por origem de usuário {#avglifetimerev}

Encontrar os canais que trazem novos usuários é importante, mas qual é o valor geral desses referenciadores? Este relatório mostra a receita média da vida útil de usuários de fontes de aquisição específicas ao longo do tempo. Em outras palavras, isso permite ver se os usuários adquiridos de uma fonte específica gastam mais com você ao longo da vida do que um grupo de usuários adquiridos de uma fonte diferente.

Para criar esse relatório no Report Builder, adicione o **Receita média da vida útil** para o relatório. Em seguida, faça o seguinte:

1. Defina as [!UICONTROL Time Period] para o período que você deseja analisar.
1. Defina as [!UICONTROL Interval] mensalmente.
   [!UICONTROL Group By] para a fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Neste exemplo, usamos o `line chart` tipo .

Veja uma apresentação visual:

![Criação de uma receita média vitalícia por fonte de usuário](../../assets/Lifetime_revenue_by_user_source.gif).

Este exemplo só observa a receita do tempo de vida, mas também é possível replicar essa análise para analisar a [!UICONTROL Number of orders] ou [!UICONTROL Distinct buyers] por fonte de referência.

## Valor médio de pedido por origem de usuário {#avgorderval}

Para ter uma ideia melhor de quanto dinheiro os usuários de uma fonte de aquisição específica gastam, você pode criar um relatório que examine o valor médio de pedido deles. Isso permitirá rastrear se os usuários adquiridos de uma fonte específica gastam mais por pedido do que os usuários de outra fonte.

Para criar esse relatório no Report Builder, adicione o **Valor médio de pedido** e faça o seguinte:

1. Defina as [!UICONTROL Time Period] ao período de registro que deseja analisar.
1. Defina as [!UICONTROL Time Interval] mensalmente.
1. Definir [!UICONTROL Group By] para a fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Neste exemplo, usamos o **colunas empilhadas** tipo de gráfico.

Veja uma apresentação visual:

![Criação de um valor de pedido médio por relatório de origem do usuário.](../../assets/Average_order_value_by_source.gif)

## Receita total por data de registro do usuário e fonte {#revbyregdateandsource}

A análise de receita vitalícia que passamos anteriormente permite que você veja a receita média vitalícia dos usuários adquiridos de diferentes fontes, mas e a receita total vitalícia? Esse relatório permitirá identificar a receita geral gerada pelos usuários que se registraram durante um tempo específico e de uma fonte específica.

Para criar esse relatório no Report Builder, adicione o `Revenue by user registration date` métrica. Se você não tiver [criou esta métrica](../../data-user/reports/ess-manage-data-metrics.md) já, você pode fazer isso replicando a variável `Revenue` e alterar a `time stamp` para usuários `creation date`. Depois de adicionar a métrica, faça o seguinte:

1. Defina as [!UICONTROL Time Period] ao período de registro que deseja analisar.
1. Defina as [!UICONTROL Time Interval] mensalmente.
1. Definir [!UICONTROL Group By] para a fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Neste exemplo, usamos o `stacked columns` tipo de gráfico.

Veja uma apresentação visual:

![Criação de um Relatório de receita total por data de registro do usuário e relatório de origem.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repetir pedidos por origem de usuário {#repeatordersbysource}

O relatório Valor médio de pedido mostra, em média, o quanto os usuários compraram de uma fonte específica gastaram ao fazer um pedido. Esse relatório, no entanto, não mostra se esses mesmos usuários são clientes recorrentes. Mas com as fontes Repetir pedidos por usuários, você pode ver se os usuários de uma fonte específica fazem mais ou menos compras repetidas.

Para criar este relatório na [Report Builder](../../tutorials/using-visual-report-builder.md), adicione o **Número de pedidos** e faça o seguinte:

1. Defina as [!UICONTROL Time Period] ao período de registro que deseja analisar.
1. Defina as [!UICONTROL Time Interval] mensalmente.
1. Adicione um [!UICONTROL filter] para que somente usuários com pedidos repetidos sejam incluídos:

   Número de pedido do usuário maior que 1

1. Definir [!UICONTROL Group By] para a fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Neste exemplo, usamos o `stacked columns` tipo de gráfico.

Veja uma apresentação visual:

![Criação de um relatório Repetir pedidos por fonte de usuário.](../../assets/Repeat_orders_by_user_source.gif)


## Quebra de linha {#wrapup}

Neste artigo, tocamos em apenas algumas análises que podem ser usadas para analisar o valor de seus canais de aquisição e marketing, mas esta é apenas a ponta do iceberg. Se você criou uma análise poderosa que não cobrimos aqui, deixe-nos entrar no que você está fazendo nos comentários.

## Relacionado {#related}

* [Fonte de referência da ordem de rastreamento via [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Conectar seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Construção [!DNL Google ECommerce] dimensões com ordens e dados do cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Práticas recomendadas para marcação de UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
