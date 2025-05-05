---
title: Tradução de consultas SQL em relatórios do Commerce Intelligence
description: Saiba como as consultas SQL são convertidas nas colunas calculadas e nas métricas usadas no Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Traduzir consultas SQL no Commerce Intelligence

Você já se perguntou como as consultas SQL são traduzidas nas [colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md) e [relatórios](../../tutorials/using-visual-report-builder.md) usados em [!DNL Commerce Intelligence]? Se você for um usuário de SQL pesado, entender como o SQL é traduzido no [!DNL Commerce Intelligence] permite que você trabalhe de forma mais inteligente no [Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) e aproveite ao máximo a plataforma [!DNL Commerce Intelligence].

No final deste tópico, você encontrará uma **matriz de tradução** para cláusulas de consulta SQL e elementos [!DNL Commerce Intelligence].

Comece observando uma consulta geral:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Relatório `group by` |
| `SUM(b)` | `Aggregate function` (coluna) |
| `FROM c` | Tabela `Source` |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Relatório `time frame` |
| `GROUP BY a` | Relatório `group by` |

Esse exemplo abrange a maioria dos casos de tradução, mas há algumas exceções. Aprofunde-se, começando com a forma como a função `aggregate` é traduzida.

## Funções agregadas

As funções agregadas (por exemplo, `count`, `sum`, `average`, `max`, `min`) nas consultas assumem a forma de **agregações de métrica** ou **agregações de coluna** em [!DNL Commerce Intelligence]. O fator de diferenciação é se uma junção é necessária para executar a agregação.

Veja um exemplo de cada uma das opções acima.

## Agregações de métricas {#aggregate}

Uma métrica é necessária ao agregar `within a single table`. Por exemplo, a função de agregação `SUM(b)` da consulta acima provavelmente seria representada por uma métrica que soma a coluna `B`. 

Veja um exemplo específico de como uma métrica `Total Revenue` pode ser definida em [!DNL Commerce Intelligence]. Observe a consulta abaixo que você tenta traduzir:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (coluna) |
| `FROM orders` | Tabela `Metric source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` (e relatórios `time range`) |

Navegue até o construtor de métricas clicando em **[!UICONTROL Manage Data** > **&#x200B; Métricas &#x200B;**> **Criar nova métrica]**, primeiro selecione a tabela `source` apropriada, que, nesse caso, é a tabela `orders`. Em seguida, a métrica será configurada conforme mostrado abaixo:

![Agregação de métrica](../../assets/Metric_aggregation.png)

## Agregações de colunas

Uma coluna calculada é necessária ao agregar uma coluna unida a partir de outra tabela. Por exemplo, você pode ter uma coluna incorporada na tabela `customer` chamada `Customer LTV`, que soma o valor total de todos os pedidos associados a esse cliente na tabela `orders`.

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

A configuração no [!DNL Commerce Intelligence] requer o uso do gerenciador de Datas Warehouse, no qual você cria um caminho entre a tabela `orders` e a tabela `customers` e, em seguida, cria uma coluna chamada `Customer LTV` na tabela do cliente.

Veja como estabelecer um novo caminho entre `customers` e `orders`. O objetivo final é criar uma nova coluna agregada na tabela `customers`, portanto, primeiro navegue até a tabela `customers` em sua Data Warehouse e clique em **[!UICONTROL Create a Column** > **&#x200B; Selecionar uma definição &#x200B;**> **SOMA]**.

Em seguida, é necessário selecionar a tabela de origem. Se existir um caminho para a tabela `orders`, basta selecioná-lo na lista suspensa. No entanto, se você estiver criando um novo caminho, clique em **[!UICONTROL Create new path]** e a tela abaixo será exibida para você:

![Criar novo caminho](../../assets/Create_new_path.png)

Aqui, é necessário considerar cuidadosamente a relação entre as duas tabelas que você está tentando unir. Nesse caso, há potencialmente `Many` pedidos associados ao cliente `One`, portanto, a tabela `orders` está listada no lado `Many`, enquanto a tabela `customers` está selecionada no lado `One`.

>[!NOTE]
>
>Em [!DNL Commerce Intelligence], um `path` é equivalente a um `Join` no SQL.

Depois que o caminho for salvo, você poderá criar a coluna `Customer LTV`! Consulte abaixo:

![](../../assets/Customer_LTV.gif)

Agora que você criou a nova coluna `Customer LTV` na tabela `customers`, está pronto para criar uma [agregação de métrica](#aggregate) usando essa coluna (por exemplo, para encontrar o LTV médio por cliente). Você também pode `group by` ou `filter` pela coluna calculada em um relatório usando as métricas existentes criadas na tabela `customers`.

>[!NOTE]
>
>Para a última, sempre que você criar uma nova coluna calculada, deverá [adicionar a dimensão às métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes que ela esteja disponível como `filter` ou `group by`.

Consulte [criando colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) com seu Gerenciador de Datas Warehouse.

## `Group By` cláusulas

`Group By` funções em consultas geralmente são representadas em [!DNL Commerce Intelligence] como uma coluna usada para segmentar ou filtrar um relatório visual. Como exemplo, vamos rever a consulta `Total Revenue` explorada anteriormente, mas dessa vez segmentar a receita por `coupon\_code` para obter uma melhor compreensão de quais cupons estão gerando mais receita.

Comece com a consulta abaixo:

| | |
|--- |--- |
| `SELECT coupon_code,` | Relatório `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(coluna) |
| `FROM orders` | Tabela `Metric source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` (e relatórios `time range`) |
| `GROUP BY coupon_code` | Relatório `group by` |

>[!NOTE]
>
>A única diferença da consulta com a qual você começou antes é a adição do &quot;coupon\_code&quot; como o agrupamento._

Usando a mesma métrica `Total Revenue` criada anteriormente, você está pronto para criar seu relatório de receita segmentada por código de cupom! Observe o gif abaixo, que mostra como configurar este relatório visual analisando os dados de setembro a novembro:

![Receita por código de cupom](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

Às vezes, um query pode envolver várias agregações para calcular a relação entre colunas separadas. Por exemplo, você pode calcular o valor médio de pedido em um query de uma das duas formas a seguir:

* `AVG('order\_total')` OU
* `SUM('order\_total')/COUNT('order\_id')`

O método anterior envolveria a criação de uma nova métrica que executa uma média na coluna `order\_total`. No entanto, o último método pode ser criado diretamente no construtor de relatórios, assumindo que você já tem métricas configuradas para calcular o `Total Revenue` e `Number of orders`.

Recue um passo e examine a consulta geral para `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (coluna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (coluna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (coluna) / Operação de métrica (coluna) |
| `FROM orders` | Tabela de métrica `source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Carimbo de data e hora da métrica (e intervalo de tempo do relatório) |

Agora suponha que você já tenha métricas configuradas para calcular o `Total Revenue` e o `Number of orders`. Como essas métricas existem, você pode simplesmente abrir o `Report Builder` e criar um cálculo sob demanda usando o recurso `Formula`:

![Fórmula de AOV](../../assets/AOV_forumula.gif)

## Encapsulamento

Se você for um usuário de SQL pesado, pensar em como as consultas são traduzidas no [!DNL Commerce Intelligence] permite que você crie colunas calculadas, métricas e relatórios.

Para referência rápida, consulte a matriz abaixo. Isso mostra um elemento [!DNL Commerce Intelligence] equivalente da cláusula SQL e como ele pode mapear para mais de um elemento, dependendo de como ele é usado na consulta.

## Elementos do Commerce Intelligence

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (com elementos de tempo) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
