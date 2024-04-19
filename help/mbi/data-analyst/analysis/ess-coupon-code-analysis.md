---
title: Análise do código do cupom (básica)
description: Saiba mais sobre o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Análise Básica De Código De Cupom

Compreender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.

Este tópico documenta as etapas necessárias para criar essa análise para entender como os clientes de cupom adquiridos se saem, ver tendências e rastrear o uso individual do código do cupom.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Introdução

Primeiro, uma observação sobre como os códigos de cupom são rastreados. Se um cliente aplicou um cupom a um pedido, acontecem três coisas:

* Um desconto é refletido na `base_grand_total` quantidade (seu `Revenue` no Commerce Intelligence)
* O código do cupom é armazenado na variável `coupon_code` campo. Se esse campo for NULL (vazio), a ordem não terá um cupom associado a ela.
* O valor com desconto é armazenado em `base_discount_amount`. Dependendo da sua configuração, esse valor pode parecer negativo ou positivo.

A partir do Commerce 2.4.7, um cliente pode aplicar mais de um código de cupom a um pedido. Neste caso:

* Todos os códigos de cupom aplicados são armazenados no `coupon_code` campo de `sales_order_coupons`. O primeiro código de cupom aplicado também é armazenado no `coupon_code` campo de `sales_order`. Se esse campo for NULL (vazio), a ordem não terá um cupom associado a ela.

## Criar uma métrica

A primeira etapa é criar uma nova métrica com as seguintes etapas:

* Navegue até **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Selecione o `sales_order`.
* Essa métrica executa uma **Sum** no **base_discount_amount** coluna, ordenada por **created_at**.
   * [!UICONTROL Filters]:
      * Adicione o `Orders we count` (Conjunto de filtros salvos)
      * Adicione o seguinte:
         * `coupon_code`**NÃO É**`[NULL]`
      * Nomeie a métrica, como `Coupon discount amount`.

## Criar seu painel

* Depois que a métrica é criada:
   * Navegue até [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Nomeie o painel como `_Coupon Analysis_`.

* É aqui que você cria e adiciona todos os relatórios.

## Criação de relatórios

* **Novos relatórios:**

>[!NOTE]
>
>A variável [!UICONTROL Time Period]** para cada relatório é listado como `All-time`. Altere isso para atender às suas necessidades de análise. Adobe recomenda que todos os relatórios desse painel cubram o mesmo período, como `All time`, `Year-to-date`ou `Last 365 days`.

* **Pedidos com cupons**
   * 
     [!UICONTROL Métrica]: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO É** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Pedidos sem cupons**
   * 
     [!UICONTROL Métrica]: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **É** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Receita líquida de pedidos com cupons**
   * 
     [!UICONTROL Métrica]: `Revenue`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO É** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Descontos de cupons**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Receita média da vida útil: clientes adquiridos do cupom**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO É** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Receita média do tempo de vida: clientes adquiridos sem cupom**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [A] `Customer's first order's coupon_code` **É**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * Métrica `1`: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO É**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

   * Métrica `2`: `Revenue`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO É**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

      * Renomear:  `Net revenue`

   * Métrica `3`: `Coupon discount amount`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO É**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

   * Criar fórmula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * Criar fórmula:**% descontado**
      * Fórmula: `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * Criar fórmula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * 
     [!UICONTROL Tipo de gráfico]: `Table`

* **Receita média vitalícia por cupom de primeira ordem**
   * [!UICONTROL Metric]:**Receita vitalícia média**
      * Adicionar filtro:
         * [`A`] `coupon_code` **É**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO É** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
     [!UICONTROL Tipo de gráfico]: **Column**

* **Novos clientes por aquisição de cupom/não cupom**
   * Métrica `1`: `New customers`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO É** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * Métrica `2`: `New customers`
      * Adicionar filtro:
         * [`A`] `coupon_code` **É**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

Depois de criar os relatórios, consulte a imagem na parte superior deste tópico para saber como organizar os relatórios em seu painel.

>[!NOTE]
>
>A partir do Adobe Commerce 2.4.7, os clientes podem usar o **quote_coupons** e **sales_order_coupons** tabelas para obter insights sobre como o cliente usa vários cupons.

![](../../assets/multicoupon_relationship_tables.png)
