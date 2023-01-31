---
title: Formatação e importação de dados de comércio eletrônico
description: Saiba mais sobre os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Formatação e importação de dados

Se você estiver usando uma integração que atualmente não é compatível com [!DNL MBI], você ainda pode usar o [Recurso de upload de arquivo](using-file-uploader.md) para obter seus dados no data warehouse. Neste artigo, abordamos os formatos de dados ideais a serem usados para fazer upload de dados de comércio eletrônico.

## `Orders` tabela

O `orders` deve conter uma linha para cada transação realizada pela empresa. As colunas em potencial incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order ID` | A ID do pedido deve ser exclusiva para cada linha da tabela. Além disso, essa normalmente é a chave primária para a tabela. |
| `Customer` | O cliente que fez o pedido. |
| `Order total` | O total do pedido. Pode ser uma coluna baseada em cálculo, na qual os valores em outras colunas, como subtotal e frete, compõem o total dessa coluna. |
| `Currency` | A moeda em que o pedido foi pago. Inclua, se relevante. |
| ` Order status` | O status do pedido, como `In Progress`, `Refunded`ou `Complete`. O valor dessa coluna provavelmente será alterado (se não estiver concluído). Dados novos e atualizados podem ser importados usando o [Recurso Anexar dados](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) no `File Uploads` página. |
| `Acquisition/marketing channel` | O canal de aquisição ou marketing do qual o cliente que fez o pedido foi encaminhado. |
| `Order datetime` | A data e a hora em que o pedido foi criado. |
| `Order updated at` | A data e a hora em que a última modificação no registro do pedido foi feita. |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` tabela {#itemstable}

O `order_detail / items` tabela deve conter uma linha para cada item distinto em cada ordem. As colunas em potencial incluem:

| Nome da coluna | Descrição |
|----|----|
| `Order item ID` | A ID do item de pedido deve ser exclusiva para cada linha da tabela. Além disso, normalmente é a variável `primary key` para a tabela. |
| `Order ID` | A ID do pedido. |
| `Product ID` | A ID do produto. |
| `Product name` | O nome do produto. |
| `Product's unit price` | O preço de uma única unidade do produto. |
| `Quantity` | A quantidade do produto no pedido. |

## `Customers` tabela {#customerstable}

O `customers` deve conter uma linha para cada conta de cliente. As colunas em potencial incluem:

| Nome da coluna | Descrição |
|----|----|
| `Customer ID` | A ID do cliente deve ser exclusiva para cada linha da tabela. Além disso, essa normalmente é a chave primária para a tabela. |
| `Customer created at` | A data e a hora em que a conta do cliente foi criada. |
| `Customer modified at` | A data e a hora em que a conta do cliente foi modificada pela última vez. |
| `Acquisition/marketing channel source` | O canal de aquisição ou marketing do qual o cliente foi referenciado. |
| `Demographic info` | Informações demográficas, como faixa etária e gênero, podem ser usadas para segmentar seus relatórios. |
| `Acquisition/marketing channel` | O canal de aquisição ou marketing do qual o cliente que fez o pedido foi encaminhado. |

## `Subscription payments` tabela

O `subscriptions` deve conter uma linha para cada pagamento de assinatura. As colunas em potencial incluem:

| Nome da coluna | Descrição |
|----|----|
| `Subscription ID` | A ID da assinatura deve ser exclusiva para cada linha da tabela. Além disso, essa normalmente é a chave primária para a tabela. |
| `Customer ID` | A ID do cliente que fez o pagamento. |
| `Payment amount` | A quantia do pagamento da assinatura. |
| `Start date` | A data e hora de início do período coberto pelo pagamento. |
| `End date` | A data e hora de término do período coberto pelo pagamento. |
