---
title: Tabela enterprise_rma
description: Saiba como analisar informações sobre uma solicitação de retorno específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Tabela enterprise_rma

Cada linha na tabela `enterprise_rma` (geralmente chamada de `magento_rma` no Adobe Commerce 2.x, mas o nome pode ser personalizado) contém informações sobre uma solicitação de retorno específica.

>[!NOTE]
>
>Esta tabela só é fornecida como padrão com sua conta da Adobe Commerce se você for cliente do `Enterprise Edition` ou do `Enterprise Cloud Edition`.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `entity\_id` | Identificador exclusivo da tabela. Cada `entity\_id` representa uma solicitação de retorno. |
| `date\_requested` | A data em que a devolução foi solicitada. |
| `status` | O status da devolução. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. |
| `order\_id` | Chave estrangeira associada à tabela `sales\_flat\_order`. |
| `customer\_id` | Chave estrangeira associada à tabela `customer\_entity`. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order's created\_at` | Esta é a data do pedido original. Isso pode ser usado para obter o tempo entre a ordem e a solicitação de devolução. |
| `Customer's order number` | É o número do pedido do cliente associado ao pedido original. |
| `Seconds between order's created\_at and return's date\_requested` | O número de segundos entre a data do pedido e a solicitação de devolução. |
| `Return's total value` | Esse é o valor monetário total retornado. Esta é a soma da quantia de devolução individual de cada item de devolução. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of returns` | O número de devoluções solicitadas. | `Operation` coluna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Coluna: `date requested` |
| `Total returned amount` | O valor monetário total retornado. | `Operation `Coluna: `Return's total value`<br>`Operation`: Soma<br>`Timestamp` Coluna: data solicitada |
| `Average returned amount` | O valor monetário médio retornado. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Coluna: `date requested` |
| `Average time to return` | O tempo médio desde a ordem até a devolução. | `Operation` Coluna: Segundos entre a criação do pedido na data de retorno solicitada<br>`Operation`: `Average`<br>`Timestamp` Coluna: `date requested` |

{style="table-layout:auto"}

## Conexões com Outras Tabelas

`sale_flat_order`

* Crie colunas unidas para segmentar e filtrar por atributos em nível de ordem na tabela `enterprise_rma` por meio da seguinte associação:
   * Commerce 1.x: `enterprise_rma.order_id` (muitos) => `sales_flat_order.entity_id` (um)
   * Commerce 2.x: `magento_rma.order_id` (muitos) => `sales_order.entity_id` (um)

`enterprise_rma_item_entity`

* Crie colunas muitos para um, como `Return's total value` na tabela `enterprise_rma`, por meio da seguinte associação:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (muitos) => `enterprise_rma.entity_id` (um)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (um)
