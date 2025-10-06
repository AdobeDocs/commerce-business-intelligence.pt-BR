---
title: Desempenho do cupom
description: Saiba como analisar o desempenho do cupom.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# Análise Avançada Do Código Do Cupom

Compreender o desempenho do cupom de sua empresa é uma maneira interessante de segmentar seus pedidos e também entender melhor seus clientes. Este tópico aborda as etapas para criar análises para entender quais clientes você adquire usando cupons, como eles são executados e rastrear o uso geral do cupom.

![Análise do código do cupom da biblioteca de análises mostrando as métricas principais](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Como primeira etapa, é necessário garantir que as seguintes colunas sejam sincronizadas com o Data Warehouse. Se não estiverem, vá em frente e rastreie-os navegando até `Manage Data` > `Data Warehouse` e sincronizando o seguinte:

* tabela **sales\_flat\_order**
* **cupom\_código**
* **base\_desconto\_valor**

## Colunas calculadas

Colunas a serem criadas independentemente da política de ordens do convidado:

* Tabela `sales\_flat\_order`
* **A ordem tem um cupom aplicado?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * &#x200B;
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: caso quando `A` é nulo então `No coupon` mais `Coupon` termina

* **\[INPUT\] customer\_id - código do cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * Cadeia de caracteres [!UICONTROL Datatype]
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **Número de pedidos com este cupom**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Proprietário do Evento:`INPUT customer_id - coupon code`
   * Classificação do Evento: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` conjunto de filtros

Colunas adicionais a serem criadas se as ordens de convidado NÃO forem suportadas:

* Tabela `customer\_entity`
   * **A primeira ordem do cliente incluiu um cupom? (Cupom/Nenhum cupom)**
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

   * **Número de cupons usados durante a vida útil do cliente**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Cliente de aquisição de cupom ou cliente de aquisição que não seja de cupom**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;
        [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: **caso quando A=&#39;Cupom&#39; então &#39;Cliente de aquisição de cupom&#39; senão &#39;Cliente de aquisição de não cupom&#39; fim**

   * **Percentual de pedidos do cliente com cupom**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * &#x200B;
        [!UICONTROL Tipo de dados]: `Decimal`
      * [!UICONTROL Calculation]: **caso quando A é nulo ou B é nulo ou B=0, então nulo senão A/B termina**

   * **Uso do cupom do cliente**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * &#x200B;
        [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: **caso em que A é nulo e depois nulo quando A=0 e depois &#39;Nunca usou cupom&#39; quando A&lt;0,5 e depois &#39;Preço quase todo&#39; quando A=0,5 e depois &#39;50/50&#39; quando A=1 e depois &#39;Apenas cupons&#39; quando A>0,5 e depois &#39;Principalmente cupom&#39; senão &#39;Indefinido&#39; termina**

* Tabela `sales\_flat\_order`
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

* Tabela `sales\_flat\_order`
   * **A primeira ordem do cliente incluiu um cupom? (Cupom/Nenhum cupom)** **-** criado pelo analista como parte do seu tíquete \[COUPON ANALYSIS\]
   * **Cupom do primeiro pedido do cliente &#x200B;**{::}**-** criado pelo analista como parte do seu tíquete \[COUPON ANALYSIS\]

* **O número de cupons usados pelo cliente &#x200B;**{::}**-** criados pelo analista como parte do seu tíquete \[COUPON ANALYSIS\]
* **Cliente de aquisição de cupom ou cliente de aquisição que não seja de cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: **caso quando A=&#39;Cupom&#39; então &#39;Cliente de aquisição de cupom&#39; senão &#39;Cliente de aquisição de não cupom&#39; fim**

* **Percentual de pedidos do cliente com cupom**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * &#x200B;
     [!UICONTROL Tipo de dados]: `Decimal`
   * [!UICONTROL Calculation]: **caso quando A é nulo ou B é nulo ou B=0, então nulo senão A/B termina**

* **Uso do cupom do cliente**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * &#x200B;
     [!UICONTROL Tipo de dados]: `String`
   * [!UICONTROL Calculation]: **caso em que A é nulo e depois nulo quando A=0 e depois &#39;Nunca usou cupom&#39; quando A&lt;0,5 e depois &#39;Preço quase todo&#39; quando A=0,5 e depois &#39;50/50&#39; quando A=1 e depois &#39;Apenas cupons&#39; quando A>0,5 e depois &#39;Principalmente cupom&#39; senão &#39;Indefinido&#39; termina**

## Métricas

* **Valor do desconto do cupom**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Na tabela `sales\_flat\_order`
* Esta métrica executa uma **Soma**
* Na coluna `discount\_amount`
* Ordenado pelo carimbo de data/hora `created\_at`
* [!UICONTROL Filter]:

* **Número de cupons usados**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Na tabela `sales\_flat\_order`
* Esta métrica executa uma **Contagem**
* Na coluna `entity\_id`
* Ordenado pelo carimbo de data/hora `created\_at`
* [!UICONTROL Filter]:

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **% de clientes com e sem cupons adquiridos**
   * [!UICONTROL Metric]: `New customers`

* Métrica `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Pie`

* **Número de clientes adquiridos e não adquiridos com cupom**
   * [!UICONTROL Metric]: `New customers`

* Métrica A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Receita média vitalícia: cupom Acq. (mais de 90 dias)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média vitalícia: não cupom Acq. (mais de 90 dias)**
   * [!UICONTROL Metric]: Receita média vitalícia
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem cupom

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita média vitalícia por cupom de primeira ordem**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Métrica `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Column`

>[!NOTE]
>
>Se você tiver muitos códigos de cupom, como muitos clientes, desejará aplicar um Superior/Inferior, como Os 10 principais classificados pela receita vitalícia média

* **Probabilidade de repetição de pedido: Aquisições de cupom**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Cupom
      * O último pedido do cliente? = Não
   * &#x200B;
     [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecione um número estatisticamente significativo do gráfico `Customer's by lifetime orders`. Ao observar o gráfico, como uma boa regra é procurar números de pedido com 30 ou mais clientes no intervalo. Dependendo do conjunto de dados, esse número pode ser grande, portanto, fique à vontade para adicionar de 1 a 10.

* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilidade de ordem repetida: aquisições sem cupom**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem Cupom

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * A primeira ordem do cliente incluiu um cupom (Cupom/Sem Cupom) = Sem Cupom
      * O último pedido do cliente? = Não

   * &#x200B;
     [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Selecione um número estatisticamente significativo do gráfico `Customer's by lifetime orders` ou 1-5.

* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Taxa de uso de cupom de clientes adquiridos com cupom (pedidos repetidos)**
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

   * &#x200B;
     [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Métrica `A`: `Coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table` (pode transpor esta tabela para uma melhor visualização)

* **Taxa de uso de cupom de clientes que não foram adquiridos com o cupom (pedidos repetidos)**
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

   * &#x200B;
     [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Métrica `A`: `Non-coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table` (pode transpor esta tabela para uma melhor visualização)

* **Detalhes de uso do cupom (ordens pela primeira vez)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * &#x200B;
     [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número da ordem do cliente = 1
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Formula]: `B-C` (se C for negativo); B+C (se C for positivo)
   * &#x200B;
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
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table`
>[!NOTE]
>
>A quantidade de 10 para &quot;Número de pedidos com este cupom&quot; é arbitrária. Sinta-se à vontade para usar a quantidade mais apropriada para esse filtro.

* **Número de pedidos com cupom (o tempo todo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Receita líquida de pedidos com cupons (o tempo todo)**
   * &#x200B;
     [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * A ordem tem o cupom aplicado? (Cupom/Nenhum cupom) = Cupom

* Métrica `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Descontos de cupons (o tempo todo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Número de pedidos com e sem cupons**
   * [!UICONTROL Metric]: `Number of orders`

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Uso do cupom entre usuários repetidos**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Número de ordens vitalícias do cliente > 1

* Métrica `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Pie`

* **Detalhes de uso do cupom**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10

   * &#x200B;
     [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10

   * [!UICONTROL Formula]: `B-C` (se `C` for negativo); `B+C` (se `C` for positivo)
   * &#x200B;
     [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (se `C` for negativo); `C/(B+C)` (se `C` for positivo)
   * &#x200B;
     [!UICONTROL Formato]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número de pedidos com este cupom > 10

   * &#x200B;
     [!UICONTROL Fórmula]: `C/A`
   * &#x200B;
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
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL Tipo de gráfico]: `Table`

>[!NOTE]
>
>A quantidade de 10 para &quot;Número de pedidos com este cupom&quot; é arbitrária. Sinta-se à vontade para usar a quantidade mais apropriada para esse filtro.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior da página.

Se você tiver dúvidas ao criar esta análise, ou se quiser simplesmente envolver a equipe de Serviços Profissionais, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).

>[!NOTE]
>
>A partir do Adobe Commerce 2.4.7, os clientes podem usar as tabelas **quote_coupons** e **sales_order_coupons** para obter informações sobre como os clientes usam vários cupons.

![Diagrama de relacionamento de tabela para análise de vários cupons](../../assets/multicoupon_relationship_tables.png)
