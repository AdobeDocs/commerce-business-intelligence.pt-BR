---
title: Tabela enterprise_rma
description: Saiba como analisar informações sobre uma solicitação de retorno específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: ad4dda927f0b1b2eba9596d7adfd1419676cf03d
workflow-type: tm+mt
source-wordcount: 267
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
| `entity_id` | Identificador exclusivo da tabela. Cada `entity_id` representa uma solicitação de retorno. |
| `date_requested` | A data em que a devolução foi solicitada. |
| `status` | O status da devolução. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. |
| `order_id` | Chave estrangeira associada à tabela `sales_flat_order`. |
| `customer_id` | Chave estrangeira associada à tabela `customer_entity`. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order's created_at` | Esta é a data do pedido original. Isso pode ser usado para obter o tempo entre a ordem e a solicitação de devolução. |
| `Customer's order number` | É o número do pedido do cliente associado ao pedido original. |
| `Seconds between order's created_at and return's date_requested` | O número de segundos entre a data do pedido e a solicitação de devolução. |
| `Return's total value` | Esse é o valor monetário total retornado. Esta é a soma da quantia de devolução individual de cada item de devolução. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of returns` | O número de devoluções solicitadas. | `Operation` coluna: `entity_id`<br>`Operation`: `Count`<br>`Timestamp` Coluna: `date requested` |
| `Total returned amount` | O valor monetário total retornado. | `Operation `Coluna: `Return's total value`<br>`Operation`: Soma<br>`Timestamp` Coluna: data solicitada |
| `Average returned amount` | O valor monetário médio retornado. | `Operation` ` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Coluna: `date requested` |
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
