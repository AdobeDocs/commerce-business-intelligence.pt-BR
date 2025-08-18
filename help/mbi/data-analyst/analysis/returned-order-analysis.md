---
title: Analisando Ordens Devolvidas
description: Saiba como configurar um painel que forneça uma análise detalhada dos retornos da sua loja.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Ordens Devolvidas

Este tópico demonstra como configurar um painel que fornece uma análise detalhada dos retornos da loja.

![](../../assets/detailed-returns-dboard.png)

Antes de começar, você deve ser um cliente do [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) e verificar se sua empresa está usando a tabela `enterprise\_rma` para devoluções.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Colunas a serem rastreadas

* Tabela **`enterprise_rma`** ou **`rma`**
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* Tabela **`enterprise_rma_item_entity`** ou **`rma_item_entity`**
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Conjuntos de filtros a serem criados

* Tabela **`enterprise_rma`**
* Nome do conjunto de filtros: `Returns we count`
* Lógica do conjunto de filtros:
   * Espaço reservado - insira sua lógica personalizada aqui

* Tabela **`enterprise_rma_item_entity`**
* Nome do conjunto de filtros: `Returns items we count`
* Lógica do conjunto de filtros:
   * Espaço reservado - insira sua lógica personalizada aqui

### Colunas calculadas

Colunas para criar

* Tabela **`enterprise_rma`**
* **`Order's created at`**
* Selecione uma definição: `Joined Column`
* [!UICONTROL Create Path]:
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Selecione uma definição: `Joined Column`
* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** foi criado por um analista como parte do seu tíquete `[RETURNS ANALYSIS]`

* Tabela **`enterprise_rma_item_entity`**
* **`return_date_requested`**
* Selecione uma definição: `Joined Column`
* [!UICONTROL Create Path]:
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Selecione um [!UICONTROL table]: `enterprise_rma`
* Selecione um [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** foi criado por um analista como parte do seu tíquete `[RETURNS ANALYSIS]`

* Tabela **`sales_flat_order`**
* **`Order contains a return? (1=yes/0=No)`**
* Selecione uma definição: `Exists`
* Selecione um [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** foi criado por um analista como parte do seu tíquete `[RETURNS ANALYSIS]`
* **`Customer's previous order contains return? (1=yes/0=no)`** foi criado por um analista como parte do seu tíquete `[RETURNS ANALYSIS]`

>[!NOTE]
>
>Se você estiver interessado em analisar apenas o horário comercial para Segundos até a resolução ou Segundos até a primeira resposta, informe o analista ao solicitar o ticket.

### Métricas

* **Devoluções**
* Na tabela **`enterprise_rma`**
* Esta métrica executa uma **Contagem**
* Na coluna **`entity_id`**
* Encomendado por **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Itens retornados**
* Na tabela **`enterprise_rma_item_entity`**
* Esta métrica executa uma **Soma**
* Na coluna **`qty_approved`**
* Encomendado por **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valor total do item retornado**
* Na tabela **`enterprise_rma_item_entity`**
* Esta métrica executa uma **Soma**
* Na coluna **`Returned item total value (qty_returned * price)`**
* Encomendado por **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tempo médio entre a ordem e o retorno**
* Na tabela **`enterprise_rma`**
* Esta métrica executa uma **Média**
* Na coluna **`Time between order's created_at and date_requested`**
* Encomendado por **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

### Relatórios

* **Repetir probabilidade de ordem depois de fazer um retorno**
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

* Fórmula: probabilidade de ordem repetida
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Bar`

* **Tempo médio para retornar (o tempo todo)**
* Métrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Number`

* **Porcentagem de pedidos com retorno**
* Métrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Métrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Fórmula: % de ordens com devolução
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Receita retornada por mês**
* Métrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Line`

* **Clientes que fizeram uma devolução e não compraram novamente**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Agrupar por]: `Customer_email`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table`

* **Taxa de devolução por item**
* Métrica `A`: `Returned items` (Ocultar)
* [!UICONTROL Metric]: Itens retornados

* Métrica `B`: `Items sold` (Ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table`

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode se parecer com o painel de amostra acima.

Se você tiver dúvidas ao criar esta análise ou quiser envolver a equipe de Serviços Profissionais, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
