---
title: Formatação e importação de dados de comércio eletrônico
description: Conheça os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 0%

---

# Formatação e Importação de Dados

Se você estiver usando uma integração que não é suportada atualmente pelo [!DNL Adobe Commerce Intelligence], ainda poderá usar o [recurso de Carregamento de Arquivo](using-file-uploader.md) para obter seus dados na Data Warehouse. Este tópico aborda os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.

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
