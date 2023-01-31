---
title: Desempenho do cupom
description: Saiba mais sobre como analisar o desempenho do seu cupom.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Análise avançada do código do cupom

Entender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e também entender melhor seus clientes. Este artigo o guiará pelas etapas para criar análises para entender quais clientes você adquire por meio do uso de cupons, como eles são executados e rastrear o uso geral do cupom.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Como primeiro passo, você precisa garantir que as colunas a seguir sejam sincronizadas com sua Data Warehouse. Caso contrário, acesse-os e rastreie-os navegando até &quot;Gerenciar dados&quot; > &quot;Data Warehouse&quot; e sincronizando o seguinte:

* **sales\_false\_order** tabela
* **cupom\_code**
* **base\_desconto\_valor**

## Colunas calculadas

Colunas a serem criadas independentemente da política de pedidos de convidado:

* `sales\_flat\_order` tabela
* **O pedido tem um cupom aplicado?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: caso em que `A` é nulo então `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - código do cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]: String
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`


* **Número de pedidos com este cupom**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Proprietário do evento:`INPUT customer_id - coupon code`
   * Classificação do evento: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` conjunto de filtros

Colunas adicionais a serem criadas se os pedidos de convidado NÃO forem suportados:

* `customer\_entity` tabela
   * **O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Selecione um [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **Cupom do primeiro pedido do cliente**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **Número vitalício do cliente de cupons usados**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **Cliente de aquisição de cupão ou cliente de aquisição sem cupão**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **caso em que A=&#39;Coupon&#39; então &#39;Coupon acquisition customer customer&#39; ou &#39;Non coupon acquisition customer customer customer&#39; termina**
   * **Porcentagem de pedidos de clientes com cupom**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]: `Decimal`
      * [!UICONTROL Calculation]: **caso em que A é nulo ou B é nulo ou B=0 então null ou o restante A/B termina**
   * **Uso do cupom do cliente**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **caso em que A é nulo então nulo quando A=0 então &#39;Nunca usou cupom&#39; quando A&lt;0.5 então &#39;Maioritariamente preço completo&#39; quando A=0.5 então &#39;50/50&#39; quando A=1 então &#39;Cupons somente&#39; quando A>0.5 então &#39;Maioritariamente cupom&#39; mais &#39;Indefinido&#39; termina**









* `sales\_flat\_order` tabela
   * **O primeiro pedido do cliente incluiu cupom? (Cupom/Sem cupom)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **Cupom do primeiro pedido do cliente**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `Customer's first order coupon?`


Colunas adicionais a serem criadas se os pedidos de convidado NÃO forem suportados:

* `sales\_flat\_order` tabela
   * **O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom)** **-** criado pelo analista como parte do tíquete \[COUPON ANALYSIS\]
   * **Cupom do primeiro pedido do cliente**{::}**-** criado pelo analista como parte do tíquete \[COUPON ANALYSIS\]

* **Número vitalício do cliente de cupons usados**{::}**-** criado pelo analista como parte do tíquete \[COUPON ANALYSIS\]
* **Cliente de aquisição de cupão ou cliente de aquisição sem cupão**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **caso em que A=&#39;Coupon&#39; então &#39;Coupon acquisition customer customer&#39; ou &#39;Non coupon acquisition customer customer customer&#39; termina**


* **Porcentagem de pedidos de clientes com cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]: `Decimal`
   * [!UICONTROL Calculation]: **caso em que A é nulo ou B é nulo ou B=0 então null ou o restante A/B termina**


* **Uso do cupom do cliente**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **caso em que A é nulo então nulo quando A=0 então &#39;Nunca usou cupom&#39; quando A&lt;0.5 então &#39;Maioritariamente preço completo&#39; quando A=0.5 então &#39;50/50&#39; quando A=1 então &#39;Cupons somente&#39; quando A>0.5 então &#39;Maioritariamente cupom&#39; mais &#39;Indefinido&#39; termina**


## Métricas

* **Valor do desconto do cupom**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* No `sales\_flat\_order` tabela
* Essa métrica executa um **Soma**
* No `discount\_amount` column
* Solicitado pela `created\_at` timestamp
* [!UICONTROL Filter]:

* **Número de cupons usados**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* No `sales\_flat\_order` tabela
* Essa métrica executa um **Contagem**
* No `entity\_id` column
* Solicitado pela `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **% de clientes adquiridos e não adquiridos com cupão**
   * [!UICONTROL Metric]: `New customers`

* Métrica `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* 

   [!UICONTROL Tipo de gráfico]: `Pie`

* **Número de clientes adquiridos e não adquiridos por cupão**
   * [!UICONTROL Metric]: `New customers`

* Métrica A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Receita média da vida útil: Acq. Cupom (mais de 90 dias de idade)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média da vida útil: Acq sem cupom. (mais de 90 dias de idade)**
   * [!UICONTROL Metric]: Receita média da vida útil
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Nenhum cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média da vida útil por cupom de primeiro pedido**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Métrica `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL Tipo de gráfico]: `Column`

>[!NOTE]
>
>Se você tiver um grande número de códigos de cupom, como muitos de nossos clientes têm, você desejará aplicar uma opção Superior/Inferior, como os 10 principais, classificados por receita média vitalícia

* **Probabilidade de ordem repetida: Aquisições de cupão**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom
      * O último pedido do cliente é? = Não
   * 
      [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecione um número estatisticamente significativo de `Customer's by lifetime orders` gráfico. Ao observar o gráfico, como uma boa regra, geralmente procuramos números de pedido com 30 ou mais clientes no bucket. Dependendo do seu conjunto de dados, pode ser um grande número; portanto, sinta-se à vontade para adicionar 1-10.


* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilidade de ordem repetida: Aquisições sem cupons**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Nenhum Cupom
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * O primeiro pedido do cliente incluiu um cupom (Cupom/Sem Cupom) = Nenhum Cupom
      * O último pedido do cliente é? = Não
   * 
      [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecione um número estatisticamente significativo de `Customer's by lifetime orders` gráfico ou 1-5.



* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Taxa de uso de cupom dos clientes adquiridos por cupom (pedidos repetidos)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente de aquisição de cupão ou cliente de aquisição sem cupão = Aquisição de cupão
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Cupom
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Cupom
      * O pedido tem um cupom aplicado? (Cupom/Sem cupom) = Cupom
   * 
      [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Métrica `A`: `Coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Table` (pode transpor essa tabela para obter uma melhor visualização)

* **Taxa de uso de cupom dos clientes não adquiridos por cupom (pedidos repetidos)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente de aquisição de cupão ou cliente de aquisição sem cupão = Aquisição sem cupão
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Nenhum cupom
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Sem Cupom
      * O pedido tem um cupom aplicado? (Cupom/Sem cupom) = Cupom
   * 
      [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Métrica `A`: `Non-coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Table` (pode transpor essa tabela para obter uma melhor visualização)

* **Detalhes de uso do cupom (pedidos pela primeira vez)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente = 1
      * Número de pedidos com este cupom > 10
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente = 1
      * Número de pedidos com este cupom > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente = 1
      * Número de pedidos com este cupom > 10
   * [!UICONTROL Formula]: `B-C` (se C for negativo); B+C (se C for positivo)
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número do pedido do cliente = 1
      * Número de pedidos com este cupom > 10




* Métrica `A`: `First time orders (FTO)`
* Métrica `B`: `Revenue from FTO`
* Métrica `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Métrica `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL Tipo de gráfico]: `Table`
>[!NOTE]
>
>A quantidade de 10 para &quot;Número de ordens com este cupom&quot; é arbitrária. Você pode usar a quantidade mais apropriada para esse filtro.

* **Número de ordens com cupom (todo o tempo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita líquida de ordens com cupons (o tempo todo)**
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * O pedido tem um cupom aplicado? (Cupom/Sem cupom) = Cupom

* Métrica `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Descontos de cupons (o tempo todo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Número de ordens com e sem cupons**
   * [!UICONTROL Metric]: `Number of orders`

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Uso de cupom entre usuários repetidos**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Número de ordens por vida do cliente > 1

* Métrica `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL Tipo de gráfico]: `Pie`

* **Detalhes de uso do cupom**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10
   * [!UICONTROL Formula]: `B-C` (se `C` é negativo); `B+C` (se `C` é positivo)
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (se `C` é negativo); `C/(B+C)` (se `C` é positivo)
   * 

      [!UICONTROL Formato]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10
   * 
      [!UICONTROL Fórmula]: `C/A`
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10





* Métrica `A`: `Number of orders`
* Métrica `B`: `Net revenue from orders`
* Métrica `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Métrica `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Métrica `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL Tipo de gráfico]: `Table`

>[!NOTE]
>
>A quantidade de 10 para &quot;Número de ordens com este cupom&quot; é arbitrária. Você pode usar a quantidade mais apropriada para esse filtro.

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior da página.

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](../../guide-overview.md).
