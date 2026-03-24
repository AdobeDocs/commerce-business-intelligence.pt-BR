---
title: Solicite dados usando o recurso Mostrar superior/inferior
description: Saiba como ordenar seus dados usando o recurso Mostrar superior/inferior.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/EbxcX2kLo3aKcj1KkCZLfkRlCbQ5q00m9zf-afGv1Ic
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---

# Ordenando Dados usando o recurso `Show Top/Bottom`

Você pode fazer mais no `Visual Report Builder` do que criar análises de tendência ao longo do tempo. Por exemplo, você pode criar um relatório para mostrar o valor de seus canais de aquisição e marketing, mas também pode criar um relatório que mostre apenas os cinco principais desempenhos. Da mesma forma, é possível redirecionar seus esforços de marketing criando um relatório que mostra quais estados geram mais receita.

Esse tipo de classificação e ordenação de dados pode ser feito em relatórios que usam um `Group By` e um `Time Interval of None`. Quando ambos os elementos estão em um relatório, o recurso `Show Top/Bottom` é exibido acima da visualização do gráfico. Esse recurso permite que você veja os pontos de dados superior (do mais alto ao mais baixo) e inferior (do mais baixo ao mais alto) com base nos parâmetros definidos.

![Mostrar recurso Superior/Inferior no Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Como faço para usá-lo? {#how}

Clique em **[!UICONTROL Show Top/Bottom link]** para definir os parâmetros de exibição e classificação. O número na caixa de texto pode ser um número inteiro (como `5`) ou `ALL`. Em seguida, você pode optar por classificar o relatório pela métrica OU pelo agrupamento.

Por exemplo, se você quiser exibir as cinco fontes de referência que geraram mais receita, esta é a maneira como você faz isso:

1. Adicionar a métrica `Revenue` ao relatório.

1. Adicione um `Group By` para segmentar a métrica por fonte de referência.

1. Defina `Time Interval` como `None`.

1. Nas configurações de `Show Top/Bottom`, defina a exibição para `5` para que somente as fontes de referência com os cinco principais valores de receita total sejam incluídas no relatório.

>[!NOTE]
>
>Como o relatório não tem um `Time Interval`, os valores - neste caso, as cinco principais fontes de referência - podem mudar com o tempo. Se uma origem de referência ultrapassar outra em termos de receita, a ordem em que as origens são exibidas será alterada.

## E quanto ao uso de várias métricas? {#multiplemetrics}

O uso desse recurso fica complicado quando há mais de uma métrica em um relatório porque cada métrica só pode ser classificada sozinha ou por um dos agrupamentos.

Digamos que você tenha criado um relatório com as métricas `Revenue` e `Number of orders`, agrupadas por fonte de referência. `Revenue` só pode ser classificado por `Revenue` ou fonte de referência e `Number of orders` só pode ser classificado por `Number of orders` ou fonte de referência.

Isso significa que, embora você possa mostrar `Revenue` somente das `5` principais fontes de referência geradoras de receita, você não pode mostrar o número de pedidos também pelas `5` principais fontes de referência geradoras de receita. Simplificando: quando há várias métricas, a melhor opção é classificar cada métrica pelo agrupamento.

Abaixo está um exemplo de um gráfico que classificou a métrica `Revenue` por ela mesma, em vez de pelo agrupamento. Como você pode ver, não classificar a métrica pelo agrupamento criou um relatório estranho (e, em última análise, inútil):

![Resultados de relatório estranhos e inúteis.](../../assets/strange-report-results.png)

Se você tivesse classificado ambas as métricas pelo agrupamento, o gráfico seria semelhante a:

![Classificando ambas as métricas pelo agrupamento.](../../assets/sort-metrics-by-grouping.png)

## Como os valores são classificados por padrão? {#defaultsorting}

Quando apenas uma métrica é incluída em um relatório com um `Group by` e um `Time Interval` de `None`, a ordenação padrão no `Visual Report Builder` é mostrar os valores principais com base na métrica. Nesta instância, o recurso `Show Top/Bottom` pode não ser necessário se isso atender às suas necessidades.

Este exemplo analisa quantas oportunidades seus representantes de vendas fecharam. Esta tabela é classificada automaticamente da mais alta para a mais baixa com base na métrica, neste caso `Won Opportunities`.

![Ordenação pela métrica.](../../assets/Ordered_by_metric.png)

No entanto, quando uma segunda métrica é adicionada, o padrão é ordenar a parte superior com base no agrupamento. À medida que métricas e agrupamentos são adicionados, a classificação padrão é baseada no primeiro agrupamento, depois no segundo agrupamento e assim por diante.

![Ordenação pelo agrupamento.](../../assets/Ordered_by_grouping.png)

## Encapsulamento {#wrapup}

Embora alguns recursos básicos sejam abordados aqui, esse recurso tem muitos usos interessantes.

Pense no exemplo de oportunidades e do representante de vendas anterior. Remover o `Time Interval`, aplicar um `Group By` e classificar os dados com base no agrupamento nos permitiu obter uma visão detalhada do número de oportunidades ganhas de cada representante. Além disso, o uso do recurso `Show Top/Bottom` permite descobrir quem são os melhores desempenhos.
