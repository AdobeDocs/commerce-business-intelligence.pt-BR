---
title: Diagramas de Relacionamento de Entidade
description: Conheça alguns diagramas de ER para ajudar a visualizar a relação entre algumas tabelas comuns do banco de dados do Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Diagrama de Relação de Entidade

O que é um **[!UICONTROL entity relationship (ER) diagram]**? Um diagrama [!UICONTROL ER] é uma visualização de tabelas em um banco de dados e como elas se relacionam entre si. Este tópico contém alguns diagramas [!UICONTROL ER] para ajudá-lo a visualizar a relação entre algumas tabelas comuns do banco de dados do Adobe Commerce.

>[!NOTE]
>
>Neste tópico, você verá as palavras **ingressar**, **relacionamento** e **caminho**. Todas essas palavras são usadas para descrever como duas tabelas são conectadas.

## Diagrama [!UICONTROL ER] do Core Commerce

![4_Gráfico_de_BD](../../assets/4_DB_Chart.png)

Este diagrama `ER` representa as relações entre as tabelas principais em um banco de dados do Commerce. Ao exibir vários relacionamentos de uma só vez, é possível ver como os dados se relacionariam em várias tabelas.

As seções abaixo contêm `ER` diagramas específicos para duas tabelas de cada vez. Para exibir um diagrama e a descrição que o acompanha, clique no cabeçalho dessa seção.

## `customer\_entity & sales\_flat\_order`

![Vários Pedidos De Um Cliente](../../assets/2_OneCustomerManyOrders.png)

Um cliente pode fazer muitos pedidos. A relação entre essas duas tabelas é `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` não é igual a `sales\_flat\_order.entity\_id`. O primeiro pode ser pensado como um `customer\_id` e o segundo como um `order\_id.`

Em [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, ele será definido da seguinte maneira:

![Diagrama de relacionamento da entidade mostrando o caminho de sales_flat_order para customer_entity](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Um pedido pode conter muitos itens. A relação entre essas duas tabelas é `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Em [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, defina-o conforme demonstrado abaixo.

![Diagrama de relacionamento da entidade mostrando o caminho de sales_flat_order_item para sales_flat_order](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Um produto pode ser comprado por muitos itens. A relação entre essas duas tabelas é `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Em [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, defina-o conforme demonstrado abaixo.

![Diagrama de relacionamento da entidade mostrando o caminho de sales_flat_order_item para catalog_product_entity](../../assets/SFOI___CPE_path.png)
