---
title: Formatação e importação de dados de comércio eletrônico
description: Conheça os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Formatação e Importação de Dados

Se você estiver usando uma integração não compatível com o [!DNL MBI], você ainda poderá usar o [Recurso de carregamento de arquivo](using-file-uploader.md) para inserir seus dados na Data Warehouse. Este artigo aborda os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.

## `Orders` tabela

A variável `orders` A tabela deve conter uma linha para cada transação que a empresa realizou. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order ID` | A ID do pedido deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer` | O cliente que fez o pedido. |
| `Order total` | O total do pedido. Pode ser uma coluna baseada em cálculo, em que os valores em outras colunas — como subtotal e envio — compõem o total dessa coluna. |
| `Currency` | A moeda em que o pedido foi pago. Inclua, se relevante. |
| ` Order status` | O status do pedido, como `In Progress`, `Refunded`ou `Complete`. O valor dessa coluna é alterado (se não estiver completo). Dados novos e atualizados podem ser importados usando o [Recurso Acrescentar Dados](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) no `File Uploads` página. |
| `Acquisition/marketing channel` | A aquisição ou canal de marketing do qual o cliente que fez o pedido foi referenciado. |
| `Order datetime` | A data e a hora em que o pedido foi criado. |
| `Order updated at` | A data e a hora em que a última modificação no registro de pedido foi feita. |

{style="table-layout:auto"}

## `Order detail/items` tabela {#itemstable}

A variável `order_detail / items` a tabela deve conter uma linha para cada item distinto em cada ordem. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order item ID` | A ID do item do pedido deve ser exclusiva para cada linha da tabela. Além disso, geralmente é o `primary key` para a tabela. |
| `Order ID` | A ID do pedido. |
| `Product ID` | A ID do produto. |
| `Product name` | O nome do produto. |
| `Product's unit price` | O preço de uma única unidade do produto. |
| `Quantity` | A quantidade do produto no pedido. |

## `Customers` tabela {#customerstable}

A variável `customers` A tabela deve conter uma linha para cada conta de cliente. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Customer ID` | A ID do cliente deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer created at` | A data e a hora em que a conta do cliente foi criada. |
| `Customer modified at` | A data e a hora em que a conta do cliente foi modificada pela última vez. |
| `Acquisition/marketing channel source` | A aquisição ou canal de marketing do qual o cliente foi encaminhado. |
| `Demographic info` | Informações demográficas, como faixa etária e gênero, podem ser usadas para segmentar seus relatórios. |
| `Acquisition/marketing channel` | A aquisição ou canal de marketing do qual o cliente que fez o pedido foi referenciado. |

## `Subscription payments` tabela

A variável `subscriptions` A tabela deve conter uma linha para cada pagamento de assinatura. As possíveis colunas incluem:

| Nome da coluna | Descrição |
|----|----|
| `Subscription ID` | A ID da assinatura deve ser exclusiva para cada linha na tabela. Além disso, geralmente é a chave primária da tabela. |
| `Customer ID` | A ID do cliente que fez o pagamento. |
| `Payment amount` | O valor do pagamento da assinatura. |
| `Start date` | A data/hora inicial do período coberto pelo pagamento. |
| `End date` | A data/hora final do período coberto pelo pagamento. |
