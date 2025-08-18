---
title: ROI de marketing
description: Saiba como configurar um painel que acompanhe sua análise de canal, incluindo o ROI agregado e por campanha.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# ROI de marketing

>[!NOTE]
>
>Este tópico contém instruções para clientes que estão usando a arquitetura original e a nova arquitetura. Você está na [nova arquitetura](../../administrator/account-management/new-architecture.md) se tiver a seção &quot;Data Warehouse Views&quot; disponível após selecionar &quot;Gerenciar Dados&quot; na barra de ferramentas principal.

Se você está gastando dinheiro em publicidade on-line, você quer monitorar seu retorno sobre esses gastos e tomar decisões orientadas por dados sobre investimentos adicionais. Este tópico demonstra como configurar um painel que controle sua análise de canal, incluindo o ROI agregado e por campanha.

![](../../assets/Marketing_dashboard_example.png)

Antes de começar, você deseja conectar suas contas do [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md), [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md) e [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) e trazer dados adicionais de gastos com anúncios online. Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelas Consolidadas

**Arquitetura original**: para reunir seus gastos de várias fontes, como [!DNL Facebook Ads] ou [!DNL Google Adwords], a Adobe recomenda criar uma **tabela consolidada** de todos os seus gastos com anúncios. Você precisa de um analista para concluir esta etapa para você. Caso contrário, [registre uma solicitação de suporte](../../guide-overview.md#Submitting-a-Support-Ticket) com o assunto `[MARKETING ROI ANALYSIS]` e um analista criará essa tabela.

**Nova arquitetura:** Você pode seguir o exemplo no tópico [esta Biblioteca de Análise](../../data-analyst/data-warehouse-mgr/create-dw-views.md). As Tabelas consolidadas agora são conhecidas como Exibições do Data Warehouse na nova arquitetura.

## Colunas calculadas

Colunas para criar

* Tabela **`Consolidated Digital Ad Spend`**
* **`Campaign name`** foi criado por um analista da Adobe como parte de seu tíquete **[ANÁLISE DO ROI DE MARKETING]**

**Arquiteturas originais e novas:**

* Tabela **`sales_flat_order`**
   * **`Order's GA campaign`**
      * Selecione uma definição: `Joined Column`
      * [!UICONTROL Create Path]:
      * &#x200B;
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Selecione uma definição: Coluna Associada
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * Selecione uma definição: Coluna Associada
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId
^

* Tabela **`customer_entity`**
* **`Customer's first order GA campaign`**
   * Selecione uma definição: `Max`
   * Selecione um [!UICONTROL table]: `sales_flat_order`
   * Selecione um [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Selecione uma definição: `Max`
   * Selecione um [!UICONTROL table]: `sales_flat_order`
   * Selecione um [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Selecione uma definição: `Max`
   * Selecione um [!UICONTROL table]: `sales_flat_order`
   * Selecione um [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* Tabela **`sales_flat_order`**
* **`Customer's first order GA campaign`**
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Selecione uma definição: Coluna Associada
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Métricas

* **Gasto de anúncios**
* Na tabela **`Consolidated Digital Ad Spend`**
* Esta métrica executa uma **Soma**
* Na coluna **`adCost`**
* Ordenado pelo carimbo de data/hora **`date`**

* **Impressões do anúncio**
* Na tabela **`Consolidated Digital Ad Spend`**
* Esta métrica executa uma **Soma**
* Na coluna **`Impressions`**
* Ordenado pelo carimbo de data/hora **`Month`**

* **Cliques no anúncio**
* Na tabela **`Consolidated Digital Ad Spend`**
* Esta métrica executa uma **Soma**
* Na coluna **`adClicks`**
* Ordenado pelo carimbo de data/hora **`Month`**

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Anúncio gasto (o tempo todo)**
   * [!UICONTROL Metric]: Gasto com anúncio

* Métrica `A`: Gasto com anúncio
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Adicionar aquisições de clientes (todas as vezes)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

* Métrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **ROI do anúncio**
   * [!UICONTROL Metric]: Gasto com anúncio

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: Receita média vitalícia
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

* Métrica `A`: `Ad Spend (hide)`
* Métrica `B`: `Ad customer acquisitions (hide)`
* Métrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Pedidos por meio do GA**
   * &#x200B;
     [!UICONTROL Métrica]: `Orders`

* Métrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]: `Area`

* **ROI do anúncio por campanha**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: Receita média vitalícia
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: Número médio de ordens vitalícias
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Formula]: `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

* Métrica `A`: `Ad Spend` (ocultar)
* Métrica `B`: `Ad customer acquisitions`
* Métrica `C`: `Average LTV`
* Métrica `D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL Fórmula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Métrica `H`: `adClicks`
* Métrica `I`: `Impressions`
* &#x200B;
  [!UICONTROL Fórmula]: `CTR`
* &#x200B;
  [!UICONTROL Fórmula]: `CPC`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Intervalo]: `None`
* &#x200B;
  [!UICONTROL Agrupar por]: `campaign` (Usar a campanha &quot;Primeiro pedido do cliente&quot; para métricas de tabela de gastos sem anúncios)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Se você tiver dúvidas ao criar esta análise, ou se quiser simplesmente envolver a equipe de Serviços Profissionais, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Relacionados

* [Práticas recomendadas para marcação UTM em  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Como funciona a atribuição  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
