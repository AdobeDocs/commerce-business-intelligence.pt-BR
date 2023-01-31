---
title: Análise de código de cupom (básica)
description: Saiba mais sobre o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Análise básica do código do cupom

Entender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e entender melhor os hábitos do cliente.

Documentamos as etapas necessárias para criar essa análise e entender o desempenho dos clientes adquiridos por cupom, ver tendências e rastrear o uso do código de cupom individual.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Introdução

Primeiro, uma observação sobre como os códigos de cupom são rastreados. Se um cliente aplicou um cupom a um pedido, três coisas acontecem:

* Um desconto é refletido na variável `base_grand_total` valor (seu `Revenue` métrica em MBI)
* O código do cupom é armazenado no `coupon_code` campo. Se esse campo for NULL (vazio), o pedido não terá um cupom associado.
* O valor atualizado é armazenado em `base_discount_amount`. Dependendo da configuração, esse valor pode parecer negativo ou positivo.

## Criar uma métrica

A primeira etapa será construir uma nova métrica com as seguintes etapas:

* Navegar para **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Selecione o `sales_order`.
* Essa métrica executa um **Soma** no **base_discount_amount** coluna, ordenada por **created_at**.
   * [!UICONTROL Filters]:
      * Adicione o `Orders we count` (Conjunto de filtros salvos)
      * Adicione o seguinte:
         * `coupon_code`**NÃO É**`[NULL]`
      * Dê um nome à métrica, como `Coupon discount amount`.

## Criar seu painel

* Depois que a métrica tiver sido criada:
   * Navegar para [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Dê um nome ao painel, como `_Coupon Analysis_`.

* Será aqui que criaremos e adicionaremos todos os relatórios.

## Criação de relatórios

* **Novos relatórios:**

>[!NOTE]
>
>O [!UICONTROL Time Period]** para cada relatório é listado como `All-time`. Você pode alterar isso para atender às suas necessidades de análise. Recomendamos que todos os relatórios neste painel cubram o mesmo período de tempo, como `All time`, `Year-to-date`ou `Last 365 days`.

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
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Receita líquida de ordens com cupons**
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

* **Receita média da vida útil: Clientes adquiridos por cupão**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [`A`] `Customer's first order's coupon_code` **NÃO É** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Receita média da vida útil: Clientes adquiridos sem cupons**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Detalhes de uso do cupom (pedidos pela primeira vez)**
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
   * Criar nova fórmula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * Criar nova fórmula:**% descontados**
      * Fórmula: `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * Criar nova fórmula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * 

      [!UICONTROL Tipo de gráfico]: `Table`








* **Receita média da vida útil por cupom de primeiro pedido**
   * [!UICONTROL Metric]:**Receita vitalícia média**
      * Adicionar filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Detalhes de uso do cupom (pedidos pela primeira vez)**
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
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





Depois de criar os relatórios, consulte a imagem na parte superior deste tópico para saber como organizar os relatórios no painel.
