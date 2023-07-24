---
title: Limite de frete gratuito
description: Saiba como configurar um painel que rastreie o desempenho do seu limite de frete gratuito.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Envio gratuito

>[!NOTE]
>
>Este tópico contém instruções para clientes que estão usando a arquitetura original e a nova arquitetura. Você está na nova arquitetura se tiver o `Data Warehouse Views` seção disponível após selecionar `Manage Data` na barra de ferramentas principal.

Este tópico demonstra como configurar um painel que acompanha o desempenho do limite de frete gratuito. Esse painel, mostrado abaixo, é uma ótima maneira de testar dois limites de frete gratuito A/B. Por exemplo, sua empresa pode não ter certeza se você deve oferecer frete gratuito a US$ 50 ou US$ 100. Você deve executar um teste A/B de dois subconjuntos aleatórios de seus clientes e executar a análise em [!DNL Commerce Intelligence].

Antes de começar, você deseja identificar dois períodos separados nos quais havia valores diferentes para o limite de frete gratuito da sua loja.

![](../../assets/free_shipping_threshold.png)

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

Se você estiver na arquitetura original (por exemplo, se não tiver o `Data Warehouse Views` opção no campo `Manage Data` ), entre em contato com a equipe de suporte para criar as colunas abaixo. Na nova arquitetura, essas colunas podem ser criadas no `Manage Data > Data Warehouse` página. As instruções detalhadas são fornecidas abaixo.

* **`sales_flat_order`** tabela
   * Esse cálculo cria períodos em incrementos relativos aos tamanhos típicos do carrinho. Isso pode variar de incrementos, incluindo, 5, 10, 50, 100

* **`Order subtotal (buckets)`** Arquitetura original: criada por um analista como parte de sua `[FREE SHIPPING ANALYSIS]` tíquete
* **`Order subtotal (buckets)`** Nova arquitetura:
   * Como mencionado acima, esse cálculo cria intervalos em incrementos relativos aos tamanhos típicos do carrinho. Se você tiver uma coluna de subtotal nativa, como `base_subtotal`, que pode ser usada como base para essa nova coluna. Caso contrário, pode ser uma coluna calculada que exclui frete e descontos da receita.

  >[!NOTE]
  >
  >Os tamanhos do &quot;balde&quot; dependem do que é apropriado para você como cliente. Você pode começar com seu `average order value` e criar alguns compartimentos menores e maiores que essa quantidade. Ao observar o cálculo abaixo, você vê como copiar facilmente parte da query, editá-la e criar compartimentos adicionais. O exemplo é feito em incrementos de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`ou `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
quando `A< 200` e `A <= 250` depois `201 - 250`
quando `A<251` e `A<= 300` depois `251 - 300`
quando `A<301` e `A<= 350` depois `301 - 350`
quando `A<351` e `A<=400` depois `351 - 400`
quando `A<401` e `A<=450` depois `401 - 450`
fim do else &#39;acima de 450&#39;


## Métricas

Nenhuma métrica nova!!!

>[!NOTE]
>
>Verifique se [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Valor médio de pedido com regra de entrega A**
   * [!UICONTROL Metric]: `Average order value`

* Métrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Número de ordens por períodos de subtotal com regra de entrega A**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >Você pode cortar a extremidade da cauda mostrando o topo `X` `sorted by` `Order subtotal` (compartimentos) no `Show top/bottom`.

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **Porcentagem de ordens por subtotal com a regra de entrega A**
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

* **Percentual de ordens com subtotal excedendo a regra de entrega A**
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


Repita as etapas e relatórios acima para a Entrega B e o período com a regra de entrega B.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior desta página.
