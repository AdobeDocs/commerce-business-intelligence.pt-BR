---
title: Tabela Enterprise_Rma_Item_Entity
description: Saiba como analisar informações sobre um item específico de um retorno solicitado.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Tabela enterprise_rma_item_entity

Cada linha no `enterprise_rma_item_entity` tabela (muitas vezes chamada de `magento_rma_item_entity` no Commerce 2.x, mas o nome pode ser personalizado) contém informações sobre um item específico de uma devolução solicitada.

>[!NOTE]
>
>Esta tabela só vem com padrão sua conta do Commerce se você for um `Enterprise Edition` ou `Enterprise Cloud Edition` cliente.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `entity\_id` | Identificador exclusivo para a tabela. Cada `entity\_id` representa um item que foi solicitado para devolução. |
| `rma\_entity\_id` | Chave externa associada à `enterprise\_rma` tabela. |
| `status` | O status do retorno do item. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. Os valores neste status não corresponderão necessariamente ao valor do status do retorno geral. |
| `qty\_requested` | A quantidade que o cliente solicita para retorno. |
| `qty\_approved` | A quantidade aprovada para devolução. |
| `qty\_returned` | A quantidade efetivamente devolvida. |
| `order\_item\_id` | Chave externa associada à `sales\_flat\_order\_item` tabela. |
| `product\_sku` | O sku sendo devolvido. |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Return date\_requested` | Esta é a data em que o cliente solicitou o retorno. |
| `Item price` | O preço do item. |
| `Return item's total value (qty\_returned * price)` | Este é o valor monetário total dos itens que são retornados. Isso será usado para calcular o valor total de retorno no `enterprise\_rma` tabela. |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of items returned` | O número de itens que são retornados. | Coluna da Operação: qty retornado<br>Operação: Soma<br>Coluna Carimbo de Data e Hora: Data de devolução solicitada |
| `Returned items' total value` | O valor monetário retornado. | Coluna da Operação: Valor total do item de devolução (qty return * price)<br>Operação: Soma<br>Coluna Carimbo de Data e Hora: Data de devolução solicitada |

{style=&quot;table-layout:auto&quot;}

## Conexões a outras tabelas

`enterprise_rma`

* Criar colunas unidas como `Return date\_requested` no `enterprise_rma_item_entity` tabela por meio da seguinte associação:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muitos) => `enterprise_rma.entity_id` (1)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* Criar colunas unidas no  `enterprise_rma_item_entity` tabela por meio da seguinte associação:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muitos) => `sales_flat_order_item.item_id` (1)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muitos) => `sales_order_item.item_id` (1)
