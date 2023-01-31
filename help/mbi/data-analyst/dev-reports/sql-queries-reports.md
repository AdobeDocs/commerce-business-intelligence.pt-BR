---
title: Tradução de queries SQL para [!DNL MBI] relatórios
description: Saiba como as consultas SQL são traduzidas nas colunas calculadas, métricas usadas em [!DNL MBI].
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Traduzir consultas SQL no MBI

Já se perguntou como as consultas SQL são traduzidas para o [colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md)e [relatórios](../../tutorials/using-visual-report-builder.md) você usa em [!DNL MBI]? Se você for um usuário SQL pesado, compreendendo como o SQL é traduzido em [!DNL MBI] permitirá que você trabalhe de forma mais inteligente na [Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) e aproveite ao máximo [!DNL MBI] plataforma.

No final deste artigo, incluímos um **matriz de tradução** para cláusulas de consulta SQL e [!DNL MBI] elementos.

Começamos observando uma consulta geral:

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | Relatório `group by` |
| `SUM(b)` | `Aggregate function` (coluna) |
| `FROM c` | `Source` tabela |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Relatório `time frame` |
| `GROUP BY a` | Relatório `group by` |

Este exemplo abrange a maioria dos casos de tradução, mas há algumas exceções. Vamos mergulhar, começando com como a `aggregate` é traduzida.

## Funções agregadas

Funções agregadas (por exemplo, `count`, `sum`, `average`, `max`, `min`) nos queries assumem a forma de **agregações de métricas** ou **agregações de coluna** em [!DNL MBI]. O fator diferencial é se uma junção é necessária ou não para executar a agregação.

Vejamos um exemplo para cada uma das situações anteriores.

## Agregações de métrica {#aggregate}

Uma métrica é necessária ao agregar `within a single table`. Por exemplo, a variável `SUM(b)` a função de agregação do query acima provavelmente seria representada por uma métrica que soma a coluna `B`. 

Vejamos um exemplo específico de como uma `Total Revenue` pode ser definida em [!DNL MBI]. Consulte a query abaixo que tentaremos traduzir:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (coluna) |
| `FROM orders` | `Metric source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` e relatórios `time range`) |

Navegar até o construtor de métricas clicando em **[!UICONTROL Manage Data** > ** Métricas **> **Criar nova métrica]**, primeiro devemos selecionar o `source` , que neste caso é a variável `orders` tabela. Em seguida, a métrica seria configurada como mostrado abaixo:

![Agregação de métrica](../../assets/Metric_aggregation.png)

## Agregações de coluna

Uma coluna calculada é necessária ao agregar uma coluna que é unida de outra tabela. Por exemplo, você pode ter uma coluna incorporada no seu `customer` tabela chamada `Customer LTV`, que soma o valor total de todas as ordens associadas a esse cliente no `orders` tabela.

A consulta para essa agregação pode ser semelhante à abaixo:

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | Proprietário agregado |
| `SUM(o.order_total) as "Customer LTV"` | Operação agregada (coluna) |
| `FROM customers c` | Tabela de proprietários agregados |
| `JOIN orders o` | Tabela de origem de agregação |
| `ON c.customer_id = o.customer_id` | Caminho |
| `WHERE o.status = 'success'` | Filtro agregado |

Configurar isso em [!DNL MBI] requer o uso do gerente de Datas Warehouse, onde você criará um caminho entre as `orders` e `customers` em seguida, crie uma nova coluna chamada `Customer LTV` na tabela do seu cliente.

Primeiro, vejamos como estabelecer um novo caminho entre a `customers` e `orders`. Nosso objetivo final é criar uma nova coluna agregada na `customers` , portanto, primeiro navegue até a tabela `customers` na sua Data Warehouse, em seguida, clique em **[!UICONTROL Create a Column** > ** Selecione uma definição **> **SUM]**.

Em seguida, é necessário selecionar a tabela de origem. Se um caminho já existir para sua `orders` , basta selecioná-la na lista suspensa. No entanto, se você estiver criando um novo caminho, clique em **[!UICONTROL Create new path]** e você verá a tela abaixo:

![Criar novo caminho](../../assets/Create_new_path.png)

Aqui você precisa considerar cuidadosamente a relação entre as duas tabelas que você está tentando unir. Nesse caso, há `Many` ordens associadas a `One` cliente, portanto, o `orders` está listada na `Many` considerando que `customers` tabela selecionada na `One` lado.

>[!NOTE]
>
>Em [!DNL MBI], a *caminho* é equivalente a `Join` em SQL.

Depois que o caminho tiver sido salvo, você será configurado para criar o novo `Customer LTV` coluna! Consulte o tópico abaixo:

![](../../assets/Customer_LTV.gif)

Agora que você construiu o novo `Customer LTV` na sua coluna `customers` está pronto para criar uma [agregação de métricas](#aggregate) usando essa coluna (por exemplo, para localizar o LTV médio por cliente) ou simplesmente `group by` ou `filter` pela coluna calculada em um relatório que usa métricas existentes criadas no `customers` tabela.

>[!NOTE]
>
>No último caso, sempre que você criar uma nova coluna calculada, será necessário [adicionar a dimensão às métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes que esteja disponível como um `filter` ou `group by`.

Consulte [criação de colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) com seu gerente de Datas Warehouse.

## `Group By` cláusulas

`Group By` funções em queries geralmente são representadas em [!DNL MBI] como uma coluna usada para segmentar ou filtrar um relatório visual. Como exemplo, voltemos ao `Total Revenue` query explorada anteriormente, mas desta vez Vamos segmentar a receita pelo `coupon\_code` para obter uma melhor compreensão de quais cupons estão gerando mais receita.

Primeiro, começamos com a query abaixo:

|  |  |
|--- |--- |
| `SELECT coupon_code,` | Relatório `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(coluna) |
| `FROM orders` | `Metric source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` e relatórios `time range`) |
| `GROUP BY coupon_code` | Relatório `group by` |

>[!NOTE]
>
>A única diferença da consulta com a qual começamos antes é a adição do &#39;cupom\_code&#39; como o grupo por._

Usar o mesmo `Total Revenue` métrica criada anteriormente, agora estamos prontos para criar nosso relatório de receita segmentado por código de cupom! Dê uma olhada no gif abaixo, que mostra como configurar este relatório visual observando dados de setembro a novembro:

![Receita por código de cupom](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

Em alguns casos, um query pode envolver várias agregações para calcular a relação entre colunas separadas. Por exemplo, você pode calcular o valor médio de pedido em uma query de uma das duas maneiras:

* `AVG('order\_total')` OU
* `SUM('order\_total')/COUNT('order\_id')`

O método anterior envolveria a criação de uma nova métrica que realiza uma média no `order\_total` coluna. No entanto, o último método pode ser criado diretamente no construtor de relatórios, supondo que você já tenha métricas configuradas para calcular o valor da variável `Total Revenue` e `Number of orders`.

Vamos dar um passo atrás e olhar para a consulta geral de `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (coluna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (coluna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (coluna) / Operação de métrica (coluna) |
| `FROM orders` | Métrica `source` tabela |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Carimbo de data e hora da métrica (e intervalo de tempo do relatório) |

E suponhamos também que já tenhamos métricas configuradas para calcular o valor da variável `Total Revenue` e `Number of orders`. Como essas métricas já existem, podemos simplesmente abrir o `Report Builder` e criar um cálculo ad hoc usando o `Formula` recurso:

![Forumula AOV](../../assets/AOV_forumula.gif)

## Quebra de linha

Como mencionamos no início deste artigo, se você for um usuário SQL pesado, pensando em como as consultas são traduzidas em [!DNL MBI] permitirá que você crie colunas calculadas, métricas e relatórios.

Para uma referência rápida, confira a matriz abaixo. Mostra o equivalente de uma cláusula SQL [!DNL MBI] e como ele pode mapear para mais de um elemento, dependendo de como é usado no query.

## Elementos de MBI

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—|—|—|—|—|—| |`SELECT`|X|-|X|-|-|X|-| |`FROM`|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-| |`WHERE` (com elementos de tempo)|-|-|X|-|-|-| |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|
