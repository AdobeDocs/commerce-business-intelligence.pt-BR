---
title: ROI de marketing
description: Saiba como configurar um painel que rastreará sua análise de canal, incluindo o ROI na agregação e por campanha.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# ROI de marketing

>[!NOTE]
>
>Este artigo contém instruções para clientes que utilizam a arquitetura original e a nova arquitetura. Você está no [nova arquitetura](../../administrator/account-management/new-architecture.md) se você tiver a seção &quot;Visualizações de Data Warehouse&quot; disponível depois de selecionar &quot;Gerenciar dados&quot; na barra de ferramentas principal.

Se você estiver gastando dinheiro em publicidade on-line, inevitavelmente vai querer acompanhar seu retorno sobre esse gasto e tomar decisões orientadas por dados sobre outros investimentos. Neste artigo, demonstramos como configurar um painel que rastreará sua análise de canal, incluindo o ROI na agregação e por campanha.

![](../../assets/Marketing_dashboard_example.png)

Antes de começar, você deseja se conectar [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)e [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) , bem como trazer outros dados de gastos com anúncios online. Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelas Consolidadas

**Arquitetura original:** Para reunir os gastos de várias fontes (como [!DNL Facebook Ads] ou [!DNL Google Adwords]), recomendamos criar uma **tabela consolidada** de todos os gastos com anúncios. Você precisará de um analista para concluir esta etapa para você. Se ainda não tiver, [arquivar uma solicitação de suporte](../../guide-overview.md) com o assunto `[MARKETING ROI ANALYSIS]`e um analista criará essa tabela.

**Nova arquitetura:** Você pode seguir o exemplo estabelecido em [esta biblioteca de análise](../../data-analyst/data-warehouse-mgr/create-dw-views.md) tópico. Tabelas consolidadas agora são conhecidas como Exibições de Data Warehouse na nova arquitetura.

## Colunas calculadas

Colunas a serem criadas

* **`Consolidated Digital Ad Spend`** tabela
* **`Campaign name`** será criado por um analista como parte de **[ANÁLISE DE ROI DE MARKETING]** ticket

>[!NOTE]
>
>Consulte acima para ver as novas diferenças de arquitetura.

**Arquiteturas originais e novas:**

* **`sales_flat_order`** tabela
   * **`Order's GA campaign`**
      * Selecione uma definição: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Selecione uma definição: Coluna unida
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_apartamento_order.incestment_id = ecommerce####.transactionId
   * **`Order's GA source`**
      * Selecione uma definição: Coluna unida
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_apartamento_order.incestment_id = ecommerce####.transactionId ^




* **`customer_entity`** tabela
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
   * [!UICONTROL Path]: sales_plain_order.customer_id = customer_entity.entity_id
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

* **`sales_flat_order`** tabela
* **`Customer's first order GA campaign`**
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Selecione uma definição: Coluna unida
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Métricas

* **Gasto com anúncios**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa um **Soma**
* No **`adCost`** column
* Solicitado pela **`date`** timestamp

* **Impressões do anúncio**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa um **Soma**
* No **`Impressions`** column
* Solicitado pela **`Month`** timestamp

* **Cliques no anúncio**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa um **Soma**
* No **`adClicks`** column
* Solicitado pela **`Month`** timestamp

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Despesa com anúncios (o tempo todo)**
   * [!UICONTROL Metric]: Gasto com anúncio

* Métrica `A`: Gasto com anúncio
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Aquisições de anúncios de clientes (o tempo todo)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

* Métrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **ROI do anúncio**
   * [!UICONTROL Metric]: Gasto com anúncio

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]
   * [!UICONTROL Metric]: Receita média da vida útil
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Métrica `A`: `Ad Spend (hide)`
* Métrica `B`: `Ad customer acquisitions (hide)`
* Métrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Pedidos por meio de gás**
   * 

      [!UICONTROL Métrica]: `Orders`

* Métrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **ROI do anúncio por campanha**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]
   * [!UICONTROL Metric]: Receita média da vida útil
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]
   * [!UICONTROL Metric]: Número médio de ordens por vida
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* Métrica `A`: `Ad Spend` (ocultar)
* Métrica `B`: `Ad customer acquisitions`
* Métrica `C`: `Average LTV`
* Métrica `D`: `Average lifetime # of orders`
* 
   [!UICONTROL Fórmula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Métrica `H`: `adClicks`
* Métrica `I`: `Impressions`
* 
   [!UICONTROL Fórmula]: `CTR`
* 
   [!UICONTROL Fórmula]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalo]: `None`
* 
   [!UICONTROL Agrupar por]: `campaign` (Use a campanha &quot;Primeiro pedido do cliente&quot; para métricas de tabela de gastos não relacionados a anúncios)
* 

   [!UICONTROL Chart Type]: `Table`

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](../../guide-overview.md).

### Relacionado

* [Práticas recomendadas para marcação de UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Como [!DNL Google Analytics] A atribuição de UTM funciona?](../analysis/utm-attributes.md)
