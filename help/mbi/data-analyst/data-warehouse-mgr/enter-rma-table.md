---
title: Tabela enterprise_rma
description: Saiba como analisar informações sobre uma solicitação de retorno específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Tabela enterprise_rma

Cada linha no `enterprise_rma` tabela (muitas vezes chamada de `magento_rma` no Commerce 2.x, mas o nome pode ser personalizado) contém informações sobre uma solicitação de retorno específica.

>[!NOTE]
>
>Esta tabela só vem com padrão sua conta do Commerce se você for um `Enterprise Edition` ou `Enterprise Cloud Edition` cliente.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `entity\_id` | Identificador exclusivo para a tabela. Cada `entity\_id` representa uma solicitação de retorno. |
| `date\_requested` | A data em que a devolução foi solicitada. |
| `status` | O status do retorno. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. |
| `order\_id` | Chave externa associada à `sales\_flat\_order` tabela. |
| `customer\_id` | Chave externa associada à `customer\_entity` tabela. |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order's created\_at` | Esta é a data do pedido original. Isso pode ser usado para obter o tempo entre pedido e solicitação de retorno. |
| `Customer's order number` | Esse é o número do pedido do cliente associado ao pedido original. |
| `Seconds between order's created\_at and return's date\_requested` | O número de segundos desde a data do pedido até a solicitação de retorno. |
| `Return's total value` | Este é o valor monetário total retornado. Essa será a soma do valor de retorno individual de cada item de retorno. |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of returns` | O número de devoluções solicitadas. | `Operation` coluna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Coluna: `date requested` |
| `Total returned amount` | O valor monetário total retornado. | `Operation `Coluna: `Return's total value`<br>`Operation`: Soma<br>`Timestamp` Coluna: data solicitada |
| `Average returned amount` | O valor monetário médio retornado. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Coluna: `date requested` |
| `Average time to return` | O tempo médio desde o pedido até o retorno. | `Operation` Coluna: Segundos entre a data de criação do pedido e a data de retorno solicitada<br>`Operation`: `Average`<br>`Timestamp` Coluna: `date requested` |

{style=&quot;table-layout:auto&quot;}

## Conexões a outras tabelas

`sale_flat_order`

* Criar colunas unidas para segmentar e filtrar por atributos no nível da ordem na `enterprise_rma` tabela por meio da seguinte associação:
   * Commerce 1.x: `enterprise_rma.order_id` (muitos) => `sales_flat_order.entity_id` (1)
   * Commerce 2.x: `magento_rma.order_id` (muitos) => `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* Crie colunas de muitas para uma, como `Return's total value` no `enterprise_rma` tabela por meio da seguinte associação:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (muitos) => `enterprise_rma.entity_id` (1)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (1)
