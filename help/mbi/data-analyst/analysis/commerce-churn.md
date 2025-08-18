---
title: Churn Commerce
description: Saiba como gerar e analisar a taxa de churn do Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Taxa de churn

Este tópico demonstra como calcular uma **taxa de churn** para seus **clientes comerciais**. Ao contrário do SaaS ou de empresas de assinatura tradicionais, os clientes comerciais normalmente não têm um **&quot;evento de churn&quot;** concreto para mostrar que eles não devem mais contar para seus clientes ativos. Por esse motivo, as instruções abaixo permitem definir um cliente como &quot;rotativo&quot; com base em uma determinada quantidade de tempo decorrido desde o último pedido.

![](../../assets/Churn_rate_image.png)

Muitos clientes desejam assistência para começar a conceituar o **período** que devem usar com base em seus dados. Se você quiser usar o comportamento histórico do cliente para definir este **período de churn**, familiarize-se com o tópico [definindo churn](../analysis/define-cust-churn.md). Em seguida, você pode usar os resultados na fórmula para taxa de churn nas instruções abaixo.

## Colunas calculadas

Colunas para criar

* Tabela **`customer_entity`**
* **`Customer's last order date`**
   * Selecione um [!UICONTROL definition]: `Max`
   * Selecionar [!UICONTROL table]: `sales_flat_order`
   * Selecionar [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Selecione um [!UICONTROL definition]: `Age`
   * Selecionar [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Métricas

* **Novos clientes (por data de primeiro pedido)**
   * Clientes que são contados

>[!NOTE]
>
>Essa métrica pode existir em sua conta.

* Na tabela **`customer_entity`**
* Esta métrica executa uma **Contagem**
* Na coluna **`entity_id`**
* Ordenado pelo carimbo de data/hora **`Customer's first order date`**
* [!UICONTROL Filter]:

* **Novos clientes (por data do último pedido)**
   * Clientes que são contados

  >[!NOTE]
  >
  >Essa métrica pode existir em sua conta.

* Na tabela **`customer_entity`**
* Esta métrica executa uma **Contagem**
* Na coluna **`entity_id`**
* Ordenado pelo carimbo de data/hora **`Customer's last order date`**
* [!UICONTROL Filter]:

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Taxa de churn**
   * [!UICONTROL Metric]: Novos clientes (por data de primeiro pedido)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Segundos desde a última data do pedido do cliente >= [Seu limite autodefinido para clientes com churn ]&#x200B;**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * &#x200B;
     [!UICONTROL Format]: Percentage

* *Métrica `A`:`New customers cumulative`*
* *Métrica `B`:`Churned customers by last order date`*
* *Métrica `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Abaixo estão alguns meses comuns > segundas conversões, mas o google fornece outros valores, incluindo semana > segundos de conversões para quaisquer valores personalizados que você possa estar procurando.

| **Meses** | **Segundos** |
|---|---|
| 3 | 7.776.000 |
| 6 | 15.552.000 |
| 9 | 23.328.000 |
| 12 | 31.104.000 |

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode se parecer com o painel de amostra acima.
