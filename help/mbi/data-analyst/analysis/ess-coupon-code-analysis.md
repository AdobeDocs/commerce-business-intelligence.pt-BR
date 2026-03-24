---
title: Análise do código do cupom (básica)
description: Saiba mais sobre o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Wr-Lx6N-regGfzW3olk2hya-AybetR0w4Z2yFTWHeDM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 532
ht-degree: 0%

---

# Análise Básica De Código De Cupom

Compreender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.

Este tópico documenta as etapas necessárias para criar essa análise para entender como os clientes de cupom adquiridos se saem, ver tendências e rastrear o uso individual do código do cupom.

![Painel de análise do código do cupom mostrando as métricas de uso e desempenho](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Introdução

Primeiro, uma observação sobre como os códigos de cupom são rastreados. Se um cliente aplicou um cupom a um pedido, acontecem três coisas:

* Um desconto é refletido no valor `base_grand_total` (sua métrica `Revenue` no Commerce Intelligence)
* O código do cupom é armazenado no campo `coupon_code`. Se esse campo for NULL (vazio), a ordem não terá um cupom associado a ela.
* O valor com desconto está armazenado em `base_discount_amount`. Dependendo da sua configuração, esse valor pode parecer negativo ou positivo.

A partir do Commerce 2.4.7, um cliente pode aplicar mais de um código de cupom a um pedido. Neste caso:

* Todos os códigos de cupom aplicados são armazenados no campo `coupon_code` de `sales_order_coupons`. O primeiro código de cupom aplicado também é armazenado no campo `coupon_code` de `sales_order`. Se esse campo for NULL (vazio), a ordem não terá um cupom associado a ela.

## Criar uma métrica

A primeira etapa é criar uma nova métrica com as seguintes etapas:

* Navegue até **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Selecione o `sales_order`.
* Esta métrica executa uma **Soma** na coluna **base_discount_amount**, ordenada por **created_at**.
   * [!UICONTROL Filters]:
      * Adicionar o `Orders we count` (Conjunto de Filtros Salvos)
      * Adicione o seguinte:
         * `coupon_code`**NÃO**`[NULL]`
      * Nomeie a métrica, como `Coupon discount amount`.

## Criar seu painel

* Depois que a métrica é criada:
   * Navegue até [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Nomeie o painel como `_Coupon Analysis_`.

* É aqui que você cria e adiciona todos os relatórios.

## Criação de relatórios

* **Novos Relatórios:**

>[!NOTE]
>
>O [!UICONTROL Time Period]** para cada relatório está listado como `All-time`. Altere isso para atender às suas necessidades de análise. A Adobe recomenda que todos os relatórios deste painel abranjam o mesmo período de tempo, como `All time`, `Year-to-date` ou `Last 365 days`.

* **Pedidos com cupons**
   * &#x200B;
     [!UICONTROL Métrica]: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Pedidos sem cupons**
   * &#x200B;
     [!UICONTROL Métrica]: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Receita líquida de pedidos com cupons**
   * &#x200B;
     [!UICONTROL Métrica]: `Revenue`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Descontos de cupons**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Receita média vitalícia: cupom adquirido aos clientes**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Receita média vitalícia: clientes não adquiridos com cupom**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * Métrica `1`: `Orders`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

   * Métrica `2`: `Revenue`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

      * Renomear: `Net revenue`

   * Métrica `3`: `Coupon discount amount`
      * Adicionar filtro:
         * [`A`] `coupon_code` **NÃO**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`

   * Criar fórmula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * &#x200B;
        [!UICONTROL Format]: `Currency`

   * Criar fórmula:**% com desconto**
      * Fórmula: `(C / (B - C))`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * Criar fórmula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * &#x200B;
     [!UICONTROL Tipo de gráfico]: `Table`

* **Receita média vitalícia por cupom de primeira ordem**
   * [!UICONTROL Metric]:**Receita vitalícia média**
      * Adicionar filtro:
         * [`A`] `coupon_code` **É**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * &#x200B;
     [!UICONTROL Tipo de gráfico]: **Column**

* **Novos clientes por aquisição de cupom/não-cupom**
   * Métrica `1`: `New customers`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO** `[NULL]`

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
>A partir do Adobe Commerce 2.4.7, os clientes podem usar as tabelas **quote_coupons** e **sales_order_coupons** para obter informações sobre como os clientes usam vários cupons.

![Diagrama de relacionamento de tabela para análise de vários cupons](../../assets/multicoupon_relationship_tables.png)
