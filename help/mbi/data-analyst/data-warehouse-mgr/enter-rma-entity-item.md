---
title: Tabela Enterprise_Rma_Item_Entity
description: Saiba como analisar informações sobre um item específico de uma devolução solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Tabela enterprise_rma_item_entity

Cada linha na tabela `enterprise_rma_item_entity` (geralmente chamada de `magento_rma_item_entity` no Commerce 2.x, mas o nome pode ser personalizado) contém informações sobre um item específico a partir de um retorno solicitado.

>[!NOTE]
>
>Esta tabela só é fornecida como padrão com sua conta da Commerce se você for cliente do `Enterprise Edition` ou do `Enterprise Cloud Edition`.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `entity\_id` | Identificador exclusivo da tabela. Cada `entity\_id` representa um item que foi solicitado para retorno. |
| `rma\_entity\_id` | Chave estrangeira associada à tabela `enterprise\_rma`. |
| `status` | O status da devolução do item. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. Os valores neste status podem não corresponder ao valor do status do retorno geral. |
| `qty\_requested` | A quantidade que o cliente solicita para devolução. |
| `qty\_approved` | A quantidade aprovada para devolução. |
| `qty\_returned` | A quantidade devolvida. |
| `order\_item\_id` | Chave estrangeira associada à tabela `sales\_flat\_order\_item`. |
| `product\_sku` | O SKU que está sendo retornado. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Return date\_requested` | Esta é a data em que o cliente solicitou a devolução. |
| `Item price` | O preço do item. |
| `Return item's total value (qty\_returned * price)` | Esse é o valor monetário total dos itens retornados. Isso é usado para calcular o valor total de retorno na tabela `enterprise\_rma`. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of items returned` | O número de itens retornados. | Coluna de Operação: qtd. retornada<br>Operação: Soma<br>Coluna de Carimbo de Data/Hora: Data de retorno solicitada |
| `Returned items' total value` | O valor monetário retornado. | Coluna de Operação: Retorna o valor total do item (quantidade retornada * preço)<br>Operação: Soma<br>Coluna de carimbo de data/hora: Data de devolução solicitada |

{style="table-layout:auto"}

## Conexões com Outras Tabelas

`enterprise_rma`

* Crie colunas unidas como `Return date\_requested` na tabela `enterprise_rma_item_entity` por meio da seguinte associação:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muitos) => `enterprise_rma.entity_id` (um)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (um)

`sales_flat_order_item`

* Criar colunas unidas na  Tabela `enterprise_rma_item_entity` por meio da seguinte associação:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muitos) => `sales_flat_order_item.item_id` (um)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muitos) => `sales_order_item.item_id` (um)
