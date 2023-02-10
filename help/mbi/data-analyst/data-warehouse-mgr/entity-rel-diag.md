---
title: Diagramas de Relação de Entidade
description: Saiba mais sobre alguns diagramas ER para ajudá-lo a visualizar a relação entre algumas tabelas de banco de dados comuns do Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Diagrama de Relacionamento da Entidade

O que é um **[!UICONTROL entity relationship (ER) diagram]**? Um `ER` diagrama é uma visualização de tabelas em um banco de dados e como elas se relacionam entre si. Este artigo contém alguns diagramas ER para ajudá-lo a visualizar a relação entre um punhado de tabelas comuns de banco de dados do Commerce.

>[!NOTE]
>
>Ao longo deste artigo, você verá as palavras **join**, **relação** e **caminho**. Todas essas palavras são usadas para descrever como duas tabelas estão conectadas.

## Comércio principal `ER` Diagrama

![4_DB_Chart](../../assets/4_DB_Chart.png)

Essa `ER` O diagrama representa as relações entre as tabelas principais em um banco de dados do Commerce. Ao visualizar várias relações de uma só vez, você pode ver como os dados se relacionariam entre muitas tabelas.

As seções abaixo contêm `ER` diagramas específicos de duas tabelas de cada vez. Para exibir um diagrama e sua descrição acompanhante, clique no cabeçalho dessa seção.

## `customer\_entity & sales\_flat\_order`

![Um cliente para muitos pedidos](../../assets/2_OneCustomerManyOrders.png)

Um cliente pode fazer muitos pedidos. A relação entre essas duas tabelas é `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` não é igual `sales\_flat\_order.entity\_id`. O primeiro pode ser pensado como um `customer\_id` e o segundo pode ser pensado como um `order\_id.`

Within [!DNL MBI], se o caminho entre essas duas tabelas ainda não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, ele será definido da seguinte maneira:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Um pedido pode conter muitos itens. A relação entre essas duas tabelas é `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL MBI], se o caminho entre essas duas tabelas ainda não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, ele será definido da seguinte maneira:

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Um produto pode ser comprado com muitos itens. A relação entre essas duas tabelas é `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL MBI], se o caminho entre essas duas tabelas ainda não existir, você poderá [criar o caminho](../data-warehouse-mgr/create-paths-calc-columns.md) na guia Data Warehouse. Quando estiver pronto para criar o caminho, ele será definido da seguinte maneira:

![](../../assets/SFOI___CPE_path.png)
