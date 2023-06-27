---
title: Tradução de consultas SQL para relatórios do Commerce Intelligence
description: Saiba como as consultas SQL são convertidas nas colunas calculadas e nas métricas usadas no Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: fa65bd909495d4d73cabbc264e9a47b3e0a0da3b
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Traduzir consultas SQL no Commerce Intelligence

Já se perguntou como as consultas de SQL são traduzidas na variável [colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md), e [relatórios](../../tutorials/using-visual-report-builder.md) você usa em [!DNL Commerce Intelligence]? Se você for um usuário de SQL pesado, entender como o SQL é convertido em [!DNL Commerce Intelligence] permite que você trabalhe de forma mais inteligente [Gerenciador de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) e aproveitar ao máximo o [!DNL Commerce Intelligence] plataforma.

No final deste tópico, você encontrará uma **matriz de tradução** para cláusulas de consulta SQL e [!DNL Commerce Intelligence] elementos.

Comece observando uma consulta geral:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Relatório `group by` |
| `SUM(b)` | `Aggregate function` (coluna) |
| `FROM c` | `Source` tabela |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Relatório `time frame` |
| `GROUP BY a` | Relatório `group by` |

Esse exemplo abrange a maioria dos casos de tradução, mas há algumas exceções. Mergulhe, começando com a forma como o `aggregate` é traduzida.

## Funções agregadas

Funções agregadas (por exemplo, `count`, `sum`, `average`, `max`, `min`) em consultas assumem a forma de **agregações de métricas** ou **agregações de colunas** in [!DNL Commerce Intelligence]. O fator de diferenciação é se uma junção é necessária para executar a agregação.

Veja um exemplo de cada uma das opções acima.

## Agregações de métricas {#aggregate}

Uma métrica é necessária ao agregar `within a single table`. Assim, por exemplo, o `SUM(b)` função agregada da consulta acima provavelmente seria representada por uma métrica que soma a coluna `B`. 

Veja um exemplo específico de como uma `Total Revenue` a métrica pode ser definida em [!DNL Commerce Intelligence]. Observe a consulta abaixo que você tenta traduzir:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (coluna) |
| `FROM orders` | `Metric source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` (e relatórios) `time range`) |

Navegue até o construtor de métricas clicando em **[!UICONTROL Manage Data** > ** Métricas **> **Criar nova métrica]**, primeiro selecione o apropriado `source` que, neste caso, é o `orders` tabela. Em seguida, a métrica será configurada conforme mostrado abaixo:

![Agregação de métricas](../../assets/Metric_aggregation.png)

## Agregações de colunas

Uma coluna calculada é necessária ao agregar uma coluna unida a partir de outra tabela. Por exemplo, talvez você tenha uma coluna incorporada no `customer` tabela chamada `Customer LTV`, que soma o valor total de todos os pedidos associados a esse cliente na `orders` tabela.

A consulta para essa agregação pode ser semelhante ao mostrado abaixo:

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Proprietário agregado |
| `SUM(o.order_total) as "Customer LTV"` | Operação agregada (coluna) |
| `FROM customers c` | Tabela de proprietário agregada |
| `JOIN orders o` | Tabela de origem de agregação |
| `ON c.customer_id = o.customer_id` | Caminho |
| `WHERE o.status = 'success'` | Filtro agregado |

Configuração em [!DNL Commerce Intelligence] O requer o uso do gerenciador de Datas Warehouse, onde você cria um caminho entre os `orders` e `customers` tabela, crie uma coluna chamada `Customer LTV` na tabela do cliente.

Veja como estabelecer um novo caminho entre as `customers` e `orders`. O objetivo final é criar uma nova coluna agregada no `customers` tabela, então, primeiro navegue até a `customers` na Data Warehouse e clique em **[!UICONTROL Create a Column** > ** Selecionar uma definição **> **SOMA]**.

Em seguida, é necessário selecionar a tabela de origem. Se houver um caminho para o seu `orders` selecione-a na lista suspensa. No entanto, se você estiver criando um novo caminho, clique em **[!UICONTROL Create new path]** e a tela abaixo é exibida:

![Criar novo caminho](../../assets/Create_new_path.png)

Aqui, é necessário considerar cuidadosamente a relação entre as duas tabelas que você está tentando unir. Neste caso, existem `Many` pedidos associados a `One` cliente, portanto, o `orders` A tabela está listada no `Many` lado, ao passo que o `customers` tabela selecionada na `One` lado.

>[!NOTE]
>
>Entrada [!DNL Commerce Intelligence], um `path` equivale a um `Join` no SQL.

Depois que o caminho for salvo, você poderá criar o `Customer LTV` coluna! Consulte abaixo:

![](../../assets/Customer_LTV.gif)

Agora que você criou o novo `Customer LTV` coluna no seu `customers` tabela, você está pronto para criar um [agregação de métricas](#aggregate) usando essa coluna (por exemplo, para encontrar o LTV médio por cliente). Também é possível `group by` ou `filter` pela coluna calculada em um relatório usando as métricas existentes criadas no `customers` tabela.

>[!NOTE]
>
>Para a última, sempre que você criar uma nova coluna calculada, deverá [adicionar a dimensão às métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de estar disponível como um `filter` ou `group by`.

Consulte [criação de colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) com o Gerenciador de Datas Warehouse.

## `Group By` cláusulas

`Group By` as funções em consultas geralmente são representadas em [!DNL Commerce Intelligence] como uma coluna usada para segmentar ou filtrar um relatório visual. Como exemplo, vamos rever a `Total Revenue` consulta que você explorou anteriormente, mas que neste momento segmenta a receita pelo `coupon\_code` para compreender melhor quais cupons estão gerando mais receita.

Comece com a consulta abaixo:

| | |
|--- |--- |
| `SELECT coupon_code,` | Relatório `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(coluna) |
| `FROM orders` | `Metric source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` (e relatórios) `time range`) |
| `GROUP BY coupon_code` | Relatório `group by` |

>[!NOTE]
>
>A única diferença da consulta com a qual você começou antes é a adição do &quot;coupon\_code&quot; como o agrupamento._

Usar o mesmo `Total Revenue` que você criou anteriormente, agora você está pronto para criar seu relatório de receita segmentada por código de cupom! Observe o gif abaixo, que mostra como configurar este relatório visual analisando os dados de setembro a novembro:

![Receita por código de cupom](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

Às vezes, um query pode envolver várias agregações para calcular a relação entre colunas separadas. Por exemplo, você pode calcular o valor médio de pedido em um query de uma das duas formas a seguir:

* `AVG('order\_total')` OU
* `SUM('order\_total')/COUNT('order\_id')`

O método anterior envolveria a criação de uma nova métrica que executa uma média no `order\_total` coluna. No entanto, o último método pode ser criado diretamente no Report Builder, supondo que você já tenha as métricas configuradas para calcular o `Total Revenue` e `Number of orders`.

Dê um passo para trás e observe a consulta geral para `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (coluna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (coluna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (coluna) / Operação de métrica (coluna) |
| `FROM orders` | Métrica `source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Carimbo de data e hora da métrica (e intervalo de tempo do relatório) |

Agora, suponha que você já tenha métricas configuradas para calcular o `Total Revenue` e `Number of orders`. Como essas métricas existem, você pode simplesmente abrir a variável `Report Builder` e crie um cálculo sob demanda usando o `Formula` recurso:

![Fórmula de AOV](../../assets/AOV_forumula.gif)

## Encapsulamento

Se você for um usuário pesado de SQL, pensar em como as consultas traduzem [!DNL Commerce Intelligence] permite criar colunas calculadas, métricas e relatórios.

Para referência rápida, consulte a matriz abaixo. Isso mostra o equivalente de uma cláusula SQL [!DNL Commerce Intelligence] e como ele pode mapear para mais de um elemento, dependendo de como é usado na query.

## Elementos de inteligência do Commerce

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (com elementos de tempo) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
