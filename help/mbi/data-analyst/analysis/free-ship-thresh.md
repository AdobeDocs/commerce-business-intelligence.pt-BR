---
title: Limite de frete gratuito
description: Saiba como configurar um painel que rastreará o desempenho do limite de frete grátis.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Envio gratuito

>[!NOTE]
>
>Este artigo contém instruções para clientes que utilizam a arquitetura original e a nova arquitetura. Você estará na nova arquitetura se tiver a seção &quot;Exibições de Data Warehouse&quot; disponível depois de selecionar &quot;Gerenciar dados&quot; na barra de ferramentas principal.

Neste artigo, demonstramos como configurar um painel que rastreará o desempenho do limite de frete grátis. Este painel, mostrado abaixo, é uma ótima maneira de testar A/B dois limites diferentes de frete grátis. Por exemplo, sua empresa pode não ter certeza se você deve oferecer frete grátis de US$ 50 ou US$ 100. Você deve executar um teste A/B de dois subconjuntos aleatórios de seus clientes e realizar a análise em [!DNL MBI].

Antes de começar, você deseja identificar dois períodos de tempo separados em que você teve valores diferentes para o limite de frete gratuito da loja.

![](../../assets/free_shipping_threshold.png)

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

Se você estiver na arquitetura original (por exemplo, se não tiver a variável `Data Warehouse Views` sob a `Manage Data` ), entre em contato com a equipe de suporte para criar as colunas abaixo. Na nova arquitetura, essas colunas podem ser criadas no `Manage Data > Data Warehouse` página. Abaixo são fornecidas instruções detalhadas.

* **`sales_flat_order`** tabela
   * Esse cálculo cria buckets em incrementos em relação aos tamanhos típicos do carrinho. Pode variar desde incrementos, incluindo 5, 10, 50, 100

* **`Order subtotal (buckets)`** Arquitetura original: será criado por um analista como parte de `[FREE SHIPPING ANALYSIS]` ticket
* **`Order subtotal (buckets)`** Nova arquitetura:
   * Como mencionado acima, esse cálculo cria buckets em incrementos em relação aos tamanhos típicos do carrinho. Se você tiver uma coluna de subtotal nativa como `base_subtotal`, que pode ser usada como a base dessa nova coluna. Caso contrário, pode ser uma coluna calculada que exclui o frete e os descontos da receita.
   >[!NOTE]
   >
   >Os tamanhos de &quot;bucket&quot; dependerão do que for apropriado para você como cliente. Você pode começar com seu `average order value` e criar um determinado número de buckets menor que e maior que esse valor. Ao observar o cálculo abaixo, você verá como copiar facilmente parte do query, editá-lo e criar buckets adicionais. O exemplo é feito em incrementos de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`ou `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
quando `A< 200` e `A <= 250` then `201 - 250`
when `A<251` e `A<= 300` then `251 - 300`
when `A<301` e `A<= 350` then `301 - 350`
when `A<351` e `A<=400` then `351 - 400`
when `A<401` e `A<=450` then `401 - 450`
else &#39;over 450&#39; end



## Métricas

Nenhuma métrica nova!!

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Valor médio de pedido com a regra de envio A**
   * [!UICONTROL Metric]: `Average order value`

* Métrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Número de ordens por buckets de subtotal com a regra de entrega A**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >Você pode cortar a extremidade da cauda mostrando a parte superior `X` `sorted by` `Order subtotal` (grupos) na `Show top/bottom`.

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **Porcentagem de pedidos por subtotal com a regra de entrega A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL Agrupar por]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* Métrica `A`: `Number of orders by subtotal (hide)`
* Métrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **Porcentagem de ordens com subtotal excedendo a regra de entrega A**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Agrupar por]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* Métrica `A`: `Number of orders by subtotal`
* Métrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


Repita as etapas e relatórios acima para a Entrega B e o período com a regra de envio B.

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior desta página.
