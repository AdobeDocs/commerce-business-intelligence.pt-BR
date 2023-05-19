---
title: Identificação de suas fontes e canais de marketing mais valiosos
description: Saiba mais sobre alguns relatórios que você pode usar para descobrir seus canais de marketing mais valiosos.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# Identificar fontes de marketing bem-sucedidas

Você pesquisou seu público, criou sua campanha, investiu em alguns canais de marketing. Agora que já passou algum tempo, como esses canais estão se saindo? Qual canal trouxe os usuários mais novos? Qual fonte contribuiu mais para sua receita total?

Com [!DNL Adobe Commerce Intelligence], você pode segmentar facilmente sua receita e seus usuários por fonte de referência, independentemente de ela corresponder a [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) ou campos de dados personalizados. Essa segmentação permite encontrar seus canais com melhor desempenho e investir melhor seu orçamento de marketing.

Este tópico explora alguns relatórios que você pode usar para descobrir seus canais de marketing mais valiosos:

* [Novos usuários por origens](#newusersbysource)
* [Receita média vitalícia por origem do usuário](#avglifetimerev)
* [Valor médio de pedido por origem de usuário](#avgorderval)
* [Receita por data e origens de registro do usuário](#revbyregdateandsource)
* [Repetir ordens por origem do usuário](#repeatordersbysource)

## Pré-requisitos {#prereqs}

Para criar as análises neste tópico, é necessário acesso aos dados de aquisição de marketing/fonte de referência. Se você ainda não estiver rastreando, será necessário trazer [ordenar dados de origem da referência de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) em [!DNL Adobe Commerce Intelligence] antes de continuar. Além disso, adicionar informações do dispositivo do usuário às análises permite que você veja qual tecnologia suas indicações estão usando.

## Novos usuários por origem {#newusersbysource}

Avaliar o desempenho das fontes de referência é fundamental para determinar seus canais mais valiosos. Este relatório mostra o número de usuários recém-registrados, por fonte de aquisição, ao longo do tempo, permitindo, assim, rastrear o desempenho das fontes de referência na aquisição de novos usuários registrados.

Para criar esse relatório no [Report Builder](../../tutorials/using-visual-report-builder.md), adicione o **Novos usuários** (ou uma métrica equivalente que conta o número de novos usuários ao longo do tempo) para o relatório. Em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] ao período de registro que você deseja analisar.
1. Defina o [!UICONTROL Interval] a mensalmente.
1. Definir [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o `stacked columns` [!UICONTROL chart type].

Veja uma apresentação visual:

![Criação de um relatório Novos usuários por origem.](../../assets/New_Users_by_source.gif)

## Receita média vitalícia por origem do usuário {#avglifetimerev}

Encontrar os canais que trazem novos usuários é importante, mas qual é o valor geral dessas indicações? Este relatório mostra a receita média por vida útil dos usuários de fontes de aquisição específicas ao longo do tempo. Em outras palavras, isso permite ver se os usuários adquiridos de uma origem específica gastam mais com você durante a vida útil do que um grupo de usuários adquiridos de uma origem diferente.

Para criar esse relatório no Report Builder, adicione o **Receita média vitalícia** para o relatório. Em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] ao período que você deseja analisar.
1. Defina o [!UICONTROL Interval] a mensalmente.
   [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o `line chart` tipo.

Veja uma apresentação visual:

![Criação de uma receita média por vida útil por origem do usuário](../../assets/Lifetime_revenue_by_user_source.gif).

Este exemplo analisa apenas a receita vitalícia, mas você também pode replicar essa análise para analisar a [!UICONTROL Number of orders] ou [!UICONTROL Distinct buyers] por fonte de referência.

## Valor médio de pedido por origem de usuário {#avgorderval}

Para ter uma ideia melhor de quanto dinheiro os usuários de uma fonte de aquisição específica gastam, você pode criar um relatório que observa seu valor médio de pedido. Isso permite rastrear se os usuários adquiridos de uma determinada origem gastam mais por pedido do que os usuários de outra origem.

Para criar esse relatório no Report Builder, adicione o **Valor médio de pedido** e, em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] ao período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] a mensalmente.
1. Definir [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o **colunas empilhadas** tipo de gráfico.

Veja uma apresentação visual:

![Criação de um relatório de Valor médio de pedido por origem de usuário.](../../assets/Average_order_value_by_source.gif)

## Receita total por data e origem de registro do usuário {#revbyregdateandsource}

A análise de receita da duração que foi abordada anteriormente permite que você observe a receita média da duração de vida dos usuários adquiridos de diferentes fontes, mas e quanto à receita total da duração? Esse relatório permite identificar quantos usuários de receita geral registrados durante um horário específico e de uma origem específica são gerados.

Para criar esse relatório no Report Builder, adicione o `Revenue by user registration date` métrica. Se você não tiver [criou esta métrica](../../data-user/reports/ess-manage-data-metrics.md) você já pode fazer isso replicando o `Revenue` e alteração da variável `time stamp` para o usuário `creation date`. Depois de adicionar a métrica, faça o seguinte:

1. Defina o [!UICONTROL Time Period] ao período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] a mensalmente.
1. Definir [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o `stacked columns` tipo de gráfico.

Veja uma apresentação visual:

![Criação de um relatório Receita total por data de registro do usuário e fonte.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repetir ordens por origem do usuário {#repeatordersbysource}

O relatório Average order value mostra, em média, quantos usuários adquiridos de uma origem específica gastam ao fazer um pedido. No entanto, esse relatório não mostra se esses mesmos usuários são clientes recorrentes. Mas com as origens Repetir ordens por usuários, você pode ver se os usuários de uma determinada origem fazem compras mais ou menos repetidas.

Para criar esse relatório no [Report Builder](../../tutorials/using-visual-report-builder.md), adicione o **Número de ordens** e, em seguida, faça o seguinte:

1. Defina o [!UICONTROL Time Period] ao período de registro que você deseja analisar.
1. Defina o [!UICONTROL Time Interval] a mensalmente.
1. Adicionar um [!UICONTROL filter] para que somente os usuários com ordens repetidas sejam incluídos:

   Número de ordem do usuário maior que 1

1. Definir [!UICONTROL Group By] para fonte de aquisição (ou referência) e selecione as fontes que deseja incluir.
1. Este exemplo usa o `stacked columns` tipo de gráfico.

Veja uma apresentação visual:

![Criando um relatório Repetir ordens por origem do usuário.](../../assets/Repeat_orders_by_user_source.gif)


## Encapsulamento {#wrapup}

Este tópico abordou apenas algumas análises que você pode usar para analisar o valor de seus canais de aquisição e marketing, mas isso é apenas a ponta do iceberg.

## Relacionados {#related}

* [Origem de referência da ordem de rastreamento via [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Conectar o [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Criação [!DNL Google ECommerce] dimensões com pedidos e dados do cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Práticas recomendadas para marcação UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
