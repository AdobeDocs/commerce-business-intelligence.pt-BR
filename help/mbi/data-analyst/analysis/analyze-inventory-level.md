---
title: Analisando níveis de inventário
description: Saiba como analisar níveis de inventário.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Analisar níveis de inventário

Este tópico demonstra como configurar um painel que fornecerá insights do inventário atual. Este tópico contém instruções para os clientes sobre a arquitetura herdada ou a nova arquitetura. Você está na arquitetura herdada se não tiver a variável **[!UICONTROL Data Warehouse Views]** sob a **[!UICONTROL Manage Data]** ). Se você estiver na arquitetura herdada, envie um [nova solicitação de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) com o assunto **[!UICONTROL INVENTORY ANALYSIS]** depois de acessar a seção designada no _Colunas calculadas_ instruções abaixo.

## Colunas a serem rastreadas:

### Colunas para rastrear instruções

* **[!UICONTROL cataloginventory_stock_item]** tabela:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** tabela:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colunas calculadas:

### Nova arquitetura

* **[!UICONTROL catalog_product_entity]** tabela:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Selecionar [!UICONTROL DATETIME column]: `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Definição:
         * caso em que A é nulo ou B é nulo então null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end





* **[!UICONTROL cataloginventory_stock_item]** tabela:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Definição:
         * caso em que A é nulo ou B é nulo ou B = 0,0 então null else round(A::decimal/B,2) termina





### Arquitetura herdada

* **[!UICONTROL catalog_product_entity]** tabela:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Selecione a coluna DATETIME: **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Selecione um [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * Será criado por um analista quando você enviar o arquivo **[ANÁLISE DE INVENTÁRIO]** solicitação de suporte





* **[!UICONTROL cataloginventory_stock_item]** tabela:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * Será criado por um analista quando você enviar o arquivo **[!UICONTROL INVENTORY ANALYSIS]** solicitação de suporte





## Métricas

### Instruções de métricas

* **[!UICONTROL cataloginventory_stock_item]** tabela:
   * **`Inventory on hand`**: essa métrica executa um
      * **Soma** no
      * **`qty`** coluna ordenada pela
      * [Nenhum] column

## Relatórios

### Instruções do relatório

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 

      [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`
   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * 
      [!UICONTROL Agrupar por]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * 
      [!UICONTROL Agrupar por]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
