---
title: Tabela Enterprise_Rma_Item_Entity
description: Saiba como analisar informações sobre um item específico de uma devolução solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: 'https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '271'
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
| `entity_id` | Identificador exclusivo da tabela. Cada `entity_id` representa um item que foi solicitado para retorno. |
| `rma_entity_id` | Chave estrangeira associada à tabela `enterprise_rma`. |
| `status` | O status da devolução do item. Os valores incluem &quot;recebido&quot;, &quot;pendente&quot;, &quot;autorizado&quot;, entre outros. Os valores neste status podem não corresponder ao valor do status do retorno geral. |
| `qty_requested` | A quantidade que o cliente solicita para devolução. |
| `qty_approved` | A quantidade aprovada para devolução. |
| `qty_returned` | A quantidade devolvida. |
| `order_item_id` | Chave estrangeira associada à tabela `sales_flat_order_item`. |
| `product_sku` | O SKU que está sendo retornado. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Return date_requested` | Esta é a data em que o cliente solicitou a devolução. |
| `Item price` | O preço do item. |
| `Return item's total value (qty_returned * price)` | Esse é o valor monetário total dos itens retornados. Isso é usado para calcular o valor total de retorno na tabela `enterprise_rma`. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of items returned` | O número de itens retornados. | Coluna de Operação: qtd. retornada<br>Operação: Soma<br>Coluna de Carimbo de Data/Hora: Data de retorno solicitada |
| `Returned items' total value` | O valor monetário retornado. | Coluna de Operação: Retorna o valor total do item (quantidade retornada * preço)<br>Operação: Soma<br>Coluna de carimbo de data/hora: Data de devolução solicitada |

{style="table-layout:auto"}

## Conexões com Outras Tabelas

`enterprise_rma`

* Crie colunas unidas como `Return date_requested` na tabela `enterprise_rma_item_entity` por meio da seguinte associação:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muitos) => `enterprise_rma.entity_id` (um)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muitos) => `magento_rma.entity_id` (um)

`sales_flat_order_item`

* Criar colunas unidas na tabela `enterprise_rma_item_entity` por meio da seguinte associação:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muitos) => `sales_flat_order_item.item_id` (um)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muitos) => `sales_order_item.item_id` (um)
