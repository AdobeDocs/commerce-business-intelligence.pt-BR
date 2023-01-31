---
title: Analisando pedidos retornados
description: Saiba como configurar um painel que forneça uma análise detalhada dos retornos de sua loja.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Pedidos retornados

Neste artigo, saiba como configurar um painel que forneça uma análise detalhada do retorno da sua loja.

![](../../assets/detailed-returns-dboard.png)

Antes de começar, você deve ser um [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) cliente e deve certificar-se de que sua empresa esteja usando a variável `enterprise\_rma` tabela para retornos.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Colunas a serem rastreadas

* **`enterprise_rma`** ou **`rma`** tabela
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** ou **`rma_item_entity`** tabela
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Conjuntos de filtros para criar

* **`enterprise_rma`** tabela
* Nome do conjunto de filtros: `Returns we count`
* Lógica do conjunto de filtros:
   * Espaço reservado - insira sua lógica personalizada aqui

* **`enterprise_rma_item_entity`** tabela
* Nome do conjunto de filtros: `Returns items we count`
* Lógica do conjunto de filtros:
   * Espaço reservado - insira sua lógica personalizada aqui

### Colunas calculadas

Colunas a serem criadas

* **`enterprise_rma`** tabela
* **`Order's created at`**
* Selecione uma definição: `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Selecione uma definição: `Joined Column`
* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** é criado por um analista como parte de seu `[RETURNS ANALYSIS]` ticket

* **`enterprise_rma_item_entity`** tabela
* **`return_date_requested`**
* Selecione uma definição: `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* Selecione um [!UICONTROL table]: `enterprise_rma`
* Selecione um [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** é criado por um analista como parte de seu `[RETURNS ANALYSIS]` ticket

* **`sales_flat_order`** tabela
* **`Order contains a return? (1=yes/0=No)`**
* Selecione uma definição: `Exists`
* Selecione um [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** é criado por um analista como parte de seu `[RETURNS ANALYSIS]` ticket
* **`Customer's previous order contains return? (1=yes/0=no)`** é criado por um analista como parte de seu `[RETURNS ANALYSIS]` ticket

>[!NOTE]
>
>Se você estiver interessado em analisar apenas o horário comercial de segundos para resolução ou segundos para a primeira resposta, informe o analista ao solicitar o tíquete.

### Métricas

* **Devoluções**
* No **`enterprise_rma`** tabela
* Essa métrica executa um **Contagem**
* No **`entity_id`** column
* Solicitado pela **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Itens retornados**
* No **`enterprise_rma_item_entity`** tabela
* Essa métrica executa um **Soma**
* No **`qty_approved`** column
* Solicitado pela **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valor total do item retornado**
* No **`enterprise_rma_item_entity`** tabela
* Essa métrica executa um **Soma**
* No **`Returned item total value (qty_returned * price)`** column
* Solicitado pela **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tempo médio entre pedido e retorno**
* No **`enterprise_rma`** tabela
* Essa métrica executa uma **Média**
* No **`Time between order's created_at and date_requested`** column
* Solicitado pela **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

### Relatórios

* **Probabilidade de ordem repetida depois de fazer um retorno**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Métrica `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Fórmula: Probabilidade de ordem repetida
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL Tipo de gráfico]: `Bar`

* **Tempo médio para retornar (o tempo todo)**
* Métrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Number`

* **Porcentagem de pedidos com um retorno**
* Métrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Métrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Fórmula: % de pedidos com devolução
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Receita devolvida por mês**
* Métrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL Tipo de gráfico]: `Line`

* **Clientes que fizeram um retorno e não compraram novamente**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 
   [!UICONTROL Agrupar por]: `Customer_email`
* 

   [!UICONTROL Tipo de gráfico]: `Table`

* **Taxa de retorno por item**
* Métrica `A`: `Returned items` (Ocultar)
* [!UICONTROL Metric]: Itens retornados

* Métrica `B`: `Items sold` (Ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL Tipo de gráfico]: `Table`

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado pode ser semelhante ao painel de amostra acima.

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver a equipe de Serviços Profissionais, [entrar em contato com o suporte](../../guide-overview.md).
