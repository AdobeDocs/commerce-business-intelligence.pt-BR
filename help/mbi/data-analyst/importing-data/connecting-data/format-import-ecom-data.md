---
title: Formatação e importação de dados de comércio eletrônico
description: Conheça os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Formatação e Importação de Dados

Se você estiver usando uma integração que não é suportada atualmente pelo [!DNL Adobe Commerce Intelligence], ainda poderá usar o [recurso de Carregamento de Arquivo](using-file-uploader.md) para colocar seus dados em sua Data Warehouse. Este tópico aborda os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.

## Tabela `Orders`

A tabela `orders` deve conter uma linha para cada transação conduzida pela empresa. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order ID` | A ID do pedido deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer` | O cliente que fez o pedido. |
| `Order total` | O total do pedido. Pode ser uma coluna baseada em cálculo, em que os valores em outras colunas — como subtotal e envio — compõem o total dessa coluna. |
| `Currency` | A moeda em que o pedido foi pago. Inclua, se relevante. |
| ` Order status` | O status do pedido, como `In Progress`, `Refunded` ou `Complete`. O valor dessa coluna é alterado (se não estiver completo). Dados novos e atualizados podem ser importados usando o [recurso Acrescentar Dados](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) na página `File Uploads`. |
| `Acquisition/marketing channel` | A aquisição ou canal de marketing do qual o cliente que fez o pedido foi referenciado. |
| `Order datetime` | A data e a hora em que o pedido foi criado. |
| `Order updated at` | A data e a hora em que a última modificação no registro de pedido foi feita. |

{style="table-layout:auto"}

## Tabela `Order detail/items` {#itemstable}

A tabela `order_detail / items` deve conter uma linha para cada item distinto em cada ordem. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order item ID` | A ID do item do pedido deve ser exclusiva para cada linha da tabela. Além disso, geralmente é o `primary key` para a tabela. |
| `Order ID` | A ID do pedido. |
| `Product ID` | A ID do produto. |
| `Product name` | O nome do produto. |
| `Product's unit price` | O preço de uma única unidade do produto. |
| `Quantity` | A quantidade do produto no pedido. |

## Tabela `Customers` {#customerstable}

A tabela `customers` deve conter uma linha para cada conta de cliente. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Customer ID` | A ID do cliente deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer created at` | A data e a hora em que a conta do cliente foi criada. |
| `Customer modified at` | A data e a hora em que a conta do cliente foi modificada pela última vez. |
| `Acquisition/marketing channel source` | A aquisição ou canal de marketing do qual o cliente foi encaminhado. |
| `Demographic info` | Informações demográficas, como faixa etária e gênero, podem ser usadas para segmentar seus relatórios. |
| `Acquisition/marketing channel` | A aquisição ou canal de marketing do qual o cliente que fez o pedido foi referenciado. |

## Tabela `Subscription payments`

A tabela `subscriptions` deve conter uma linha para cada pagamento de assinatura. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Subscription ID` | A ID da assinatura deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer ID` | A ID do cliente que fez o pagamento. |
| `Payment amount` | O valor do pagamento da assinatura. |
| `Start date` | A data/hora inicial do período coberto pelo pagamento. |
| `End date` | A data/hora final do período coberto pelo pagamento. |
