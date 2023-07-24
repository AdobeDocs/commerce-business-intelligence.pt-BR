---
title: Diagramas de Relacionamento de Entidade
description: Saiba mais sobre alguns diagramas de ER para ajudar a visualizar a relação entre algumas tabelas de banco de dados comuns do Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Diagrama de Relação de Entidade

O que é uma **[!UICONTROL entity relationship (ER) diagram]**? Um [!UICONTROL ER] diagrama é uma visualização de tabelas em um banco de dados e como elas estão relacionadas umas com as outras. Este tópico contém alguns [!UICONTROL ER] diagramas para ajudar a visualizar a relação entre algumas tabelas comuns do banco de dados do Adobe Commerce.

>[!NOTE]
>
>Em todo este tópico, você verá as palavras **ingressar**, **relacionamento**, e **caminho**. Todas essas palavras são usadas para descrever como duas tabelas são conectadas.

## Comércio principal [!UICONTROL ER] Diagrama

![4_Gráfico_BD](../../assets/4_DB_Chart.png)

Este `ER` O diagrama representa as relações entre as principais tabelas em um banco de dados do Commerce. Ao exibir vários relacionamentos de uma só vez, é possível ver como os dados se relacionariam em várias tabelas.

As seções abaixo contêm `ER` diagramas específicos para duas tabelas de cada vez. Para exibir um diagrama e a descrição que o acompanha, clique no cabeçalho dessa seção.

## `customer\_entity & sales\_flat\_order`

![Um Cliente e Vários Pedidos](../../assets/2_OneCustomerManyOrders.png)

Um cliente pode fazer muitos pedidos. A relação entre essas duas tabelas é `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` não é igual a `sales\_flat\_order.entity\_id`. O primeiro pode ser visto como um `customer\_id` e o segundo pode ser visto como um `order\_id.`

Dentro de [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, ele será definido da seguinte maneira:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Um pedido pode conter muitos itens. A relação entre essas duas tabelas é `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Dentro de [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, defina-o conforme demonstrado abaixo.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_UmProdutoMuitasVezes](../../assets/3_OneProductManyTimes.png)

Um produto pode ser comprado por muitos itens. A relação entre essas duas tabelas é `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Dentro de [!DNL Commerce Intelligence], se o caminho entre essas duas tabelas não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, defina-o conforme demonstrado abaixo.

![](../../assets/SFOI___CPE_path.png)
