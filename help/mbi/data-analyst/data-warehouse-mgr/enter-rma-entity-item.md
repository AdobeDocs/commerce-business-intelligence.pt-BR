---
title: Tabela Enterprise_Rma_Item_Entity
description: Saiba como analisar informações sobre um item específico de uma devolução solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# Tabela enterprise_rma_item_entity

Cada linha no `enterprise_rma_item_entity` tabela (geralmente chamada de `magento_rma_item_entity` no Commerce 2.x, mas o nome pode ser personalizado) contém informações sobre um item específico de uma devolução solicitada.

>[!NOTE]
>
>Essa tabela só vem como padrão com sua conta do Commerce se você for um `Enterprise Edition` ou `Enterprise Cloud Edition` cliente.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `entity\_id` | Identificador exclusivo da tabela. Each `entity\_id` representa um item que foi solicitado para devolução. |
| `rma\_entity\_id` | Chave estrangeira associada à `enterprise\_rma` tabela. |
| `status` | O status da devolução do item. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. Os valores neste status podem não corresponder ao valor do status do retorno geral. |
| `qty\_requested` | A quantidade que o cliente solicita para devolução. |
| `qty\_approved` | A quantidade aprovada para devolução. |
| `qty\_returned` | A quantidade devolvida. |
| `order\_item\_id` | Chave estrangeira associada à `sales\_flat\_order\_item` tabela. |
| `product\_sku` | O SKU que está sendo retornado. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Return date\_requested` | Esta é a data em que o cliente solicitou a devolução. |
| `Item price` | O preço do item. |
| `Return item's total value (qty\_returned * price)` | Esse é o valor monetário total dos itens retornados. Isso é usado para calcular o valor total do retorno no `enterprise\_rma` tabela. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of items returned` | O número de itens retornados. | Coluna Operação: qtd. devolvida<br>Operação: Soma<br>Coluna de carimbo de data/hora: data de retorno solicitada |
| `Returned items' total value` | O valor monetário retornado. | Coluna de Operação: Valor total do item de devolução (qtd. devolvida * preço)<br>Operação: Soma<br>Coluna de carimbo de data/hora: data de retorno solicitada |

{style="table-layout:auto"}

## Conexões com Outras Tabelas

`enterprise_rma`

* Criar colunas associadas, como `Return date\_requested` no `enterprise_rma_item_entity` tabela por meio da seguinte associação:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muitos) => `enterprise_rma.entity_id` (um)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (um)

`sales_flat_order_item`

* Criar colunas unidas na  `enterprise_rma_item_entity` tabela por meio da seguinte associação:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muitos) => `sales_flat_order_item.item_id` (um)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muitos) => `sales_order_item.item_id` (um)
