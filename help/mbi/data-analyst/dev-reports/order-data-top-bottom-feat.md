---
title: Solicitar dados usando o recurso Mostrar parte superior/inferior
description: Saiba como solicitar seus dados usando o recurso Mostrar parte superior/inferior.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Solicitar dados usando `Show Top/Bottom` recurso

Você pode fazer mais na `Visual Report Builder` do que criar análises dessa tendência ao longo do tempo. Por exemplo, você pode criar um relatório para mostrar o valor dos seus canais de aquisição e marketing, mas também pode criar um relatório que mostra apenas os cinco principais desempenhos. Da mesma forma, é possível reconcentrar seus esforços de marketing criando um relatório que mostra quais estados geram mais receita.

Esse tipo de classificação e ordem de dados pode ser feita em relatórios que usam uma `Group By` e `Time Interval of None`. Quando ambos os elementos estão em um relatório, a variável `Show Top/Bottom` será exibido acima da visualização do gráfico. Esse recurso permite ver os pontos de dados de cima (mais alto a mais baixo) e de baixo (do mais baixo ao mais alto) com base nos parâmetros definidos.

![Mostrar recurso Superior/Inferior no Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Como usar isso? {#how}

Depois de clicar no botão **[!UICONTROL Show Top/Bottom link]**, uma janela será exibida, onde é possível definir os parâmetros de exibição e classificação. O número na caixa de texto pode ser um número inteiro (como `5`) ou `ALL`. Em seguida, você pode optar por classificar o relatório pela métrica OU pelo agrupamento.

Por exemplo, se quisermos exibir as cinco fontes de referência que trouxeram mais receita, é assim que fazemos:

1. Adicione o `Revenue` para o relatório.

1. Adicione um `Group By` para segmentar a métrica por fonte de referência.

1. Definir `Time Interval` para `None`.

1. No `Show Top/Bottom` , defina a exibição como `5` assim, somente as fontes de referência com os cinco principais valores totais de receita são incluídas no relatório.

>[!NOTE]
>
>Porque o relatório não tem um `Time Interval`, os valores - nesse caso, as cinco principais fontes de referência - podem mudar com o tempo. Se uma fonte de referência ultrapassar outra em termos de receita, a ordem em que as fontes serão exibidas será alterada.

## E quanto ao uso de várias métricas? {#multiplemetrics}

O uso desse recurso é complicado quando há mais de uma métrica em um relatório, pois cada métrica só pode ser classificada sozinha ou por um dos agrupamentos.

Digamos que construímos um relatório com as duas `Revenue` e `Number of orders` métricas, agrupadas por fonte de referência. `Revenue` só pode ser classificado por `Revenue` ou fonte de referência e `Number of orders` só pode ser classificado por `Number of orders` ou fonte de referência.

Isso significa que, embora possamos mostrar a variável `Revenue` somente na parte superior `5` receita gerando fontes de referência, não podemos mostrar o número de pedidos também pelo topo `5` receita gerando fontes de referência. Simplificando: quando há várias métricas, a melhor opção é classificar cada métrica pelo agrupamento.

Aqui está um exemplo de um gráfico onde classificamos o `Revenue` por si só em vez do agrupamento. Como é possível ver, a não classificação da métrica pelo agrupamento criou um relatório estranho (e, em última análise, não útil):

![Resultados de relatórios estranhos e inúteis.](../../assets/strange-report-results.png)

Se as duas métricas fossem classificadas pelo agrupamento, o gráfico seria semelhante a:

![Classificação de ambas as métricas pelo agrupamento.](../../assets/sort-metrics-by-grouping.png)

## Como os valores são classificados por padrão? {#defaultsorting}

Quando apenas uma métrica é incluída em um relatório com uma `Group by` e `Time Interval` de `None`, a ordem padrão no `Visual Report Builder` é mostrar os valores principais com base na métrica. Nesse caso, a variável `Show Top/Bottom` pode não ser necessário se isso atender às suas necessidades.

Neste exemplo, estamos olhando para quantas oportunidades nossos representantes de vendas fecharam. Esta tabela é classificada automaticamente da mais alta para a mais baixa com base na métrica, neste caso `Won Opportunities`.

![Solicitação por métrica.](../../assets/Ordered_by_metric.png)

No entanto, quando uma segunda métrica é adicionada, o padrão é ordenar a parte superior com base no agrupamento. À medida que métricas e agrupamentos são adicionados, a classificação padrão será baseada no primeiro agrupamento, no segundo agrupamento e assim por diante.

![Ordem pelo agrupamento.](../../assets/Ordered_by_grouping.png)

## Quebra de linha {#wrapup}

Nós o mencionamos no início do artigo, mas o dizemos novamente: enquanto cobrimos alguns exemplos básicos, esse recurso tem muitos usos interessantes.

Pense em nosso representante de vendas anterior e no exemplo de oportunidades. Remoção do `Time Interval`, aplicando `Group By`, e classificar os dados com base no agrupamento nos permitiu obter uma imagem detalhada do número de oportunidades vencidas de cada representante. Além disso, usando o `Show Top/Bottom` permite descobrir quem são os melhores artistas.
