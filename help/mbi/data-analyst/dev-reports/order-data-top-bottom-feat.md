---
title: Solicite dados usando o recurso Mostrar superior/inferior
description: Saiba como ordenar seus dados usando o recurso Mostrar superior/inferior.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Ordenação de dados usando `Show Top/Bottom` recurso

Você pode fazer mais no `Visual Report Builder` do que criar análises com tendência ao longo do tempo. Por exemplo, você pode criar um relatório para mostrar o valor de seus canais de aquisição e marketing, mas também pode criar um relatório que mostre apenas os cinco principais desempenhos. Da mesma forma, é possível redirecionar seus esforços de marketing criando um relatório que mostra quais estados geram mais receita.

Esse tipo de classificação e ordenação de dados pode ser feito em relatórios que usam a `Group By` e a `Time Interval of None` . Quando esses elementos estão em um relatório, o `Show Top/Bottom` recurso é exibido acima do gráfico pré-visualização. Esse recurso permite que você visualize os pontos de dados superior (mais alto para o mais baixo) e inferior (mais baixo para mais alto) com base nos parâmetros definidos.

![Exibir primeiro/último recurso no Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Como usar isso? {#how}

**[!UICONTROL Show Top/Bottom link]** Clique em para definir os parâmetros de exibição e classificação. O número na caixa de texto pode ser um número inteiro (curtir `5` ) ou `ALL` . Próximo, você pode optar por classificar o relatório pelo métrica ou pelo agrupamento.

Por exemplo, se você quiser exibir as cinco fontes de referência que geraram mais receita, esta é a maneira como você faz isso:

1. Adicione o `Revenue` para o relatório.

1. Adicionar um `Group By` para segmentar a métrica por fonte de referência.

1. Definir `Time Interval` para `None`.

1. No `Show Top/Bottom` , defina a exibição como `5` portanto, somente as fontes de referência com os cinco principais valores de receita total são incluídas no relatório.

>[!NOTE]
>
>Como o relatório não tem um `Time Interval` , os valores-neste caso, as cinco principais fontes de referência-podem mudar ao longo do tempo. Se uma fonte de referência supera outra em termos de receita, a solicitar em que as fontes são exibidas.

## E quanto ao uso de várias métricas? {#multiplemetrics}

O uso desse recurso fica complicado quando há mais de um métrica em um relatório, pois cada métrica só pode ser classificado por si mesmo ou por um dos agrupamentos.

Digamos que você tenha criado um relatório com as métricas e `Number of orders` as `Revenue` métricas, agrupadas por referência fonte. `Revenue` Só pode ser classificada por `Revenue` ou referência fonte e `Number of orders` só pode ser classificada por `Number of orders` ou referência fonte.

Isso significa que enquanto você só pode mostrar `Revenue` a partir das principais `5` fontes referência de geração de receita, não é possível mostrar o número de pedidos também pelas principais `5` fontes referência de receita geradas. Em síntese: quando há várias métricas, a melhor opção é classificar cada métrica pelo agrupamento.

Veja abaixo um exemplo de um gráfico que classificou a `Revenue` por si só, em vez de pelo agrupamento. Como você pode ver, não classificar a métrica pelo agrupamento criou um relatório estranho (e, em última análise, inútil):

![Resultados de relatório estranhos e inúteis.](../../assets/strange-report-results.png)

Se você tivesse classificado ambas as métricas pelo agrupamento, o gráfico seria semelhante a:

![Classificar ambas as métricas pelo agrupamento.](../../assets/sort-metrics-by-grouping.png)

## Como os valores são classificados por padrão? {#defaultsorting}

Quando apenas um métrica é incluído em um relatório com um `Group by` e um `Time Interval` de `None` , a ordenação padrão no `Visual Report Builder` é mostrar os valores principais com base na métrica. Nesse instância, o `Show Top/Bottom` recurso pode não ser necessário se isso atender às suas necessidades.

Este exemplo analisa Quantas oportunidades os seus representantes de vendas fecharam. Essa tabela é classificada automaticamente do mais alto para o mais baixo com base no métrica, nesse caso `Won Opportunities` .

![Ordenação pelo métrica.](../../assets/Ordered_by_metric.png)

No entanto, quando um segundo métrica é adicionado, o padrão é solicitar parte superior com base no agrupamento. Como métricas e agrupamentos são adicionados, a classificação padrão é baseada no primeiro Agrupamento, depois no segundo Agrupamento, e assim por diante.

![Ordenação pelo agrupamento.](../../assets/Ordered_by_grouping.png)

## Encapsulamento {#wrapup}

Embora alguns recursos básicos sejam abordados aqui, esse recurso tem muitos usos interessantes.

Pense no exemplo de oportunidades e do representante de vendas anterior. Remover o `Time Interval`, aplicando um `Group By`e classificar os dados com base no agrupamento nos permitiu obter uma imagem detalhada do número de oportunidades ganhas de cada representante. Além disso, usar o `Show Top/Bottom` recurso nos permite descobrir quem são os principais executores.
