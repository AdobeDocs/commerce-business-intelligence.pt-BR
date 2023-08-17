---
title: Desempenho do cupom
description: Saiba como analisar o desempenho do cupom.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Análise Avançada Do Código Do Cupom

Compreender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e também entender melhor seus clientes. Este tópico aborda as etapas para criar análises para entender quais clientes você adquire usando cupons, como eles são executados e rastrear o uso geral do cupom.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Como primeira etapa, você precisa garantir que as seguintes colunas sejam sincronizadas com a Data Warehouse. Se não estiverem, acesse e rastreie-os navegando até `Manage Data` > `Data Warehouse`e sincronizando o seguinte:

* **sales\_flat\_order** tabela
* **coupon\_code**
* **base\_discount\_amount**

## Colunas calculadas

Colunas a serem criadas independentemente da política de ordens do convidado:

* `sales\_flat\_order` tabela
* **A ordem tem o cupom aplicado?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * 
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: caso quando `A` é nulo e depois `No coupon` else `Coupon` fim

* **\[INPUT\] customer\_id - código do cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] String
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **Número de pedidos com este cupom**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Proprietário do evento:`INPUT customer_id - coupon code`
   * Classificação do evento: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` conjunto de filtros

Colunas adicionais a serem criadas se as ordens de convidado NÃO forem suportadas:

* `customer\_entity` tabela
   * **O primeiro pedido do cliente incluiu um cupom? (Cupom/Nenhum cupom)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Selecione um [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **Cupom de primeira ordem do cliente**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **Número de cupons usados pelo cliente por toda a vida útil**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Cliente de aquisição de cupom ou cliente de aquisição que não é de cupom**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * 
        [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: **caso em que A=&#39;Coupon&#39; então o fim &#39;Coupon acquisition customer&#39; else &#39;Non-coupon acquisition customer&#39; end**

   * **Porcentagem de ordens do cliente com cupom**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * 
        [!UICONTROL Tipo de dados]: `Decimal`
      * [!UICONTROL Calculation]: **caso em que A é nulo ou B é nulo ou B=0 então nulo senão A/B termina**

   * **Uso do cupom do cliente**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * 
        [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: **caso em que A é nulo então nulo quando A=0 então &#39;Nunca usou cupom&#39; quando A&lt;0,5 então &#39;Preço quase todo&#39; quando A=0,5 então &#39;50/50&#39; quando A=1 então &#39;Cupons apenas&#39; quando A>0,5 então &#39;Principalmente cupom&#39; senão o fim &#39;Indefinido&#39;**

* `sales\_flat\_order` tabela
   * **O primeiro pedido do cliente incluiu o cupom? (Cupom/Nenhum cupom)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **Cupom de primeira ordem do cliente**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecione um [!UICONTROL column]: `Customer's first order coupon?`

Colunas adicionais a serem criadas se as ordens de convidado NÃO forem suportadas:

* `sales\_flat\_order` tabela
   * **O primeiro pedido do cliente incluiu um cupom? (Cupom/Nenhum cupom)** **-** criado pelo analista como parte do ticket \[COUPON ANALYSIS\]
   * **Cupom de primeira ordem do cliente**{::}**-** criado pelo analista como parte do ticket \[COUPON ANALYSIS\]

* **Número de cupons usados pelo cliente por toda a vida útil**{::}**-** criado pelo analista como parte do ticket \[COUPON ANALYSIS\]
* **Cliente de aquisição de cupom ou cliente de aquisição que não é de cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * 
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: **caso em que A=&#39;Coupon&#39; então o fim &#39;Coupon acquisition customer&#39; else &#39;Non-coupon acquisition customer&#39; end**

* **Porcentagem de ordens do cliente com cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * 
     [!UICONTROL Tipo de dados]: `Decimal`
   * [!UICONTROL Calculation]: **caso em que A é nulo ou B é nulo ou B=0 então nulo senão A/B termina**

* **Uso do cupom do cliente**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * 
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: **caso em que A é nulo então nulo quando A=0 então &#39;Nunca usou cupom&#39; quando A&lt;0,5 então &#39;Preço quase todo&#39; quando A=0,5 então &#39;50/50&#39; quando A=1 então &#39;Cupons apenas&#39; quando A>0,5 então &#39;Principalmente cupom&#39; senão o fim &#39;Indefinido&#39;**

## Métricas

* **Valor do desconto do cupom**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* No `sales\_flat\_order` tabela
* Essa métrica executa uma **Sum**
* No `discount\_amount` coluna
* Ordenado por `created\_at` carimbo de data e hora
* [!UICONTROL Filter]:

* **Número de cupons usados**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* No `sales\_flat\_order` tabela
* Essa métrica executa uma **Contagem**
* No `entity\_id` coluna
* Ordenado por `created\_at` carimbo de data e hora
* [!UICONTROL Filter]:

>[!NOTE]
>
>Verifique se [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **% de clientes com e sem cupões adquiridos**
   * [!UICONTROL Metric]: `New customers`

* Métrica `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* 
  [!UICONTROL Tipo de gráfico]: `Pie`

* **Número de clientes com e sem cupons adquiridos**
   * [!UICONTROL Metric]: `New customers`

* Métrica A `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Receita média da vida útil: cupom Acq. (mais de 90 dias de idade)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média do ciclo de vida: não cupom Acq. (mais de 90 dias de idade)**
   * [!UICONTROL Metric]: receita média ao longo da vida
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média vitalícia por cupom de primeira ordem**
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
>Se você tiver muitos códigos de cupom, como muitos clientes, desejará aplicar um Superior/Inferior, como Os 10 principais classificados pela receita vitalícia média

* **Probabilidade de ordem repetida: Aquisições de cupom**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom
      * O último pedido do cliente? = Não
   * 
     [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecionar número estatisticamente significativo de `Customer's by lifetime orders` gráfico. Ao observar o gráfico, como uma boa regra é procurar números de pedido com 30 ou mais clientes no intervalo. Dependendo do conjunto de dados, esse número pode ser grande, portanto, fique à vontade para adicionar de 1 a 10.

* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilidade de ordem repetida: Aquisições sem cupom**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem Cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem Cupom
      * O último pedido do cliente? = Não

   * 
     [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecionar número estatisticamente significativo de `Customer's by lifetime orders` ou 1-5.

* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Taxa de uso de cupom dos clientes adquiridos com cupom (ordens repetidas)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente de aquisição de cupom ou cliente de aquisição sem cupom = Aquisição de cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Nenhum cupom) = Cupom

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Nenhum cupom) = Cupom
      * A ordem tem o cupom aplicado? (Cupom/Nenhum cupom) = Cupom

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
  [!UICONTROL Tipo de gráfico]: `Table` (pode transpor esta tabela para uma melhor visualização)

* **Taxa de uso de cupom de clientes não adquiridos (ordens repetidas)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente de aquisição de cupom ou cliente de aquisição sem cupom = Aquisição sem cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Sem cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente > 1
      * O primeiro pedido do cliente incluiu um cupom? (Cupom/Sem cupom) = Sem Cupom
      * A ordem tem o cupom aplicado? (Cupom/Nenhum cupom) = Cupom

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
  [!UICONTROL Tipo de gráfico]: `Table` (pode transpor esta tabela para uma melhor visualização)

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * 
     [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Formula]: `B-C` (se C é negativo); B+C (se C é positivo)
   * 
     [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
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
>A quantidade de 10 para &quot;Número de pedidos com este cupom&quot; é arbitrária. Sinta-se à vontade para usar a quantidade mais apropriada para esse filtro.

* **Número de pedidos com cupom (todo o tempo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita líquida de pedidos com cupons (todo o tempo)**
   * 
     [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * A ordem tem o cupom aplicado? (Cupom/Nenhum cupom) = Cupom

* Métrica `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Descontos de cupons (todo o tempo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Número de pedidos com e sem cupons**
   * [!UICONTROL Metric]: `Number of orders`

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Uso do cupom entre usuários repetidos**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Número de ordens vitalícias do cliente > 1

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
>A quantidade de 10 para &quot;Número de pedidos com este cupom&quot; é arbitrária. Sinta-se à vontade para usar a quantidade mais apropriada para esse filtro.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior da página.

Se você tiver dúvidas ao criar essa análise ou se quiser simplesmente envolver a equipe de serviços profissionais, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
