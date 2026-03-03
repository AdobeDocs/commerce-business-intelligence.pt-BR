---
title: Analisando Níveis de Inventário
description: Saiba como analisar níveis de inventário.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Developer, User
feature: Dashboards, Reports
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Analisar Níveis de Inventário

Este tópico demonstra como configurar um painel que fornece informações sobre o inventário atual e contém instruções para clientes sobre a arquitetura herdada ou a nova arquitetura. Você está na arquitetura herdada se não tem a opção **[!UICONTROL Data Warehouse Views]** no menu **[!UICONTROL Manage Data]**. Se você estiver na arquitetura herdada, envie uma [nova solicitação de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) com o assunto **[!UICONTROL INVENTORY ANALYSIS]** assim que chegar à seção designada nas _Colunas calculadas_ instruções abaixo.

## Colunas a rastrear:

### Colunas para rastrear instruções

* Tabela **[!UICONTROL cataloginventory_stock_item]**:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* Tabela **[!UICONTROL catalog_product_entity]**:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colunas calculadas:

+++ Nova arquitetura

* Tabela **[!UICONTROL catalog_product_entity]**:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Selecionar [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * R: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Definição:
         * caso em que A é nulo ou B é nulo, senão nulo round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* Tabela **[!UICONTROL cataloginventory_stock_item]**:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * R: `qty`
         * B: `Avg products sold per week (all time)`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Definição:
         * caso em que A é nulo ou B é nulo ou B = 0.0, então nulo senão round(A::decimal/B,2) end

+++
+++ Arquitetura herdada

* Tabela **[!UICONTROL catalog_product_entity]**:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Selecionar coluna DATETIME: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Selecione um [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Criado por um analista quando você envia sua solicitação de suporte da **[ANÁLISE DE INVENTÁRIO]**

* Tabela **[!UICONTROL cataloginventory_stock_item]**:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecione um [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Criado por um analista quando você arquiva e envia sua solicitação de suporte do **[!UICONTROL INVENTORY ANALYSIS]**

+++

## Métricas

### Instruções de métricas

* Tabela **[!UICONTROL cataloginventory_stock_item]**:
   * **`Inventory on hand`**: essa métrica executa uma
      * **Soma** em
      * **`qty`** coluna ordenada por
      * Coluna [Nenhuma]

## Relatórios

### Instruções do relatório

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * &#x200B;
     [!UICONTROL Agrupar por]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * Intervalo de tempo: `None`
   * &#x200B;
     [!UICONTROL Agrupar por]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

Se você tiver dúvidas ao criar esta análise, ou se quiser simplesmente envolver a equipe de Serviços Profissionais, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).
