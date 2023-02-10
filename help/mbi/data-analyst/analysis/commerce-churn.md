---
title: Churn de comércio
description: Saiba como gerar e analisar sua taxa de churn do Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Taxa de abandono

Neste tópico, demonstramos como calcular um valor de **taxa de churn** para seu **clientes comerciais**. Ao contrário de SaaS ou empresas tradicionais de assinatura, os clientes comerciais normalmente não têm um **&quot;evento churn&quot;** para mostrar que eles não devem mais contar para seus clientes ativos. Por esse motivo, as instruções abaixo permitem definir um cliente como &quot;encurtado&quot; com base em um determinado período de tempo decorrido desde o último pedido.

![](../../assets/Churn_rate_image.png)

Muitos clientes desejam obter assistência para começar a conceber o que **período** eles devem usar com base em seus dados. Se desejar usar o comportamento histórico do cliente para definir isso **intervalo de tempo de churn**, você pode querer se familiarizar com o [definindo churn](../analysis/define-cust-churn.md) artigo 10. o Em seguida, você pode usar os resultados na fórmula para a taxa de churn nas instruções abaixo.

## Colunas calculadas

Colunas a serem criadas

* **`customer_entity`** tabela
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
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Métricas

* **Novos clientes (por data do primeiro pedido)**
   * Clientes que contamos

>[!NOTE]
>
>Essa métrica pode já existir em sua conta.

* No **`customer_entity`** tabela
* Essa métrica executa um **Contagem**
* No **`entity_id`** column
* Solicitado pela **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Novos clientes (por data do último pedido)**
   * Clientes que contamos

>[!NOTE]
>
>Essa métrica pode já existir em sua conta.

* No **`customer_entity`** tabela
* Essa métrica executa um **Contagem**
* No **`entity_id`** column
* Solicitado pela **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Taxa de abandono**
   * [!UICONTROL Metric]: Novos clientes (por data do primeiro pedido)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Segundos desde a última data do pedido do cliente >= [Seu corte autodefinido para clientes com rotatividade ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *Métrica `A`:`New customers cumulative`*
* *Métrica `B`:`Churned customers by last order date`*
* *Métrica `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Abaixo estão alguns meses comuns > segunda conversões, mas o google fornece outros valores, incluindo semana > segundos de conversão para quaisquer valores personalizados que você esteja procurando.

| **Months** | **Seconds** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com o painel de amostra acima.
