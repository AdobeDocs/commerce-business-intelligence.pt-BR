---
title: ROI de marketing
description: Saiba como configurar um painel que acompanhe sua análise de canal, incluindo o ROI agregado e por campanha.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# ROI de marketing

>[!NOTE]
>
>Este tópico contém instruções para clientes que estão usando a arquitetura original e a nova arquitetura. Você está no [nova arquitetura](../../administrator/account-management/new-architecture.md) se você tiver a seção &quot;Data Warehouse Views&quot; disponível após selecionar &quot;Manage Data&quot; (Gerenciar dados) na barra de ferramentas principal.

Se você está gastando dinheiro em publicidade on-line, você quer monitorar seu retorno sobre esses gastos e tomar decisões orientadas por dados sobre investimentos adicionais. Este tópico demonstra como configurar um painel que controle sua análise de canal, incluindo o ROI agregado e por campanha.

![](../../assets/Marketing_dashboard_example.png)

Antes de começar, você deseja conectar seu [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), e [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) contas e trazer dados adicionais de gastos com anúncios online. Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelas Consolidadas

**Arquitetura original:** Para reunir seus gastos de várias fontes, como [!DNL Facebook Ads] ou [!DNL Google Adwords], o Adobe recomenda a criação de um **tabela consolidada** de todo o seu investimento em anúncios. Você precisa de um analista para concluir esta etapa para você. Caso contrário, [arquivar uma solicitação de suporte](../../guide-overview.md#Submitting-a-Support-Ticket) com o assunto `[MARKETING ROI ANALYSIS]`, e um analista cria essa tabela.

**Nova arquitetura:** Você pode seguir o exemplo em [esta Biblioteca de análise](../../data-analyst/data-warehouse-mgr/create-dw-views.md) tópico. As Tabelas consolidadas agora são conhecidas como Exibições do Data Warehouse na nova arquitetura.

## Colunas calculadas

Colunas para criar

* **`Consolidated Digital Ad Spend`** tabela
* **`Campaign name`** é criado por um analista de Adobe como parte de sua **[ANÁLISE DE ROI DE MARKETING]** tíquete

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
      * Selecione uma definição: Coluna Associada
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * Selecione uma definição: Coluna Associada
      * Selecione um [!UICONTROL table]: `ecommerce####`
      * Selecione um [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId ^

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

* **`sales_flat_order`** tabela
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

* **Gasto com anúncios**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa uma **Sum**
* No **`adCost`** coluna
* Ordenado por **`date`** carimbo de data e hora

* **Impressões do anúncio**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa uma **Sum**
* No **`Impressions`** coluna
* Ordenado por **`Month`** carimbo de data e hora

* **Cliques de anúncio**
* No **`Consolidated Digital Ad Spend`** tabela
* Essa métrica executa uma **Sum**
* No **`adClicks`** coluna
* Ordenado por **`Month`** carimbo de data e hora

>[!NOTE]
>
>Verifique se [adicionar todas as novas colunas como dimensões às métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Gasto com anúncio (todo o tempo)**
   * [!UICONTROL Metric]: Gasto com anúncios

* Métrica `A`: Gasto com anúncios
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Intervalo]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Aquisições de clientes de publicidade (todo o tempo)**
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
   * [!UICONTROL Metric]: Gasto com anúncios

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: Receita média vitalícia
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

* **Pedidos por meio de ga**
   * 
     [!UICONTROL Métrica]: `Orders`

* Métrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **ROI de anúncio por campanha**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: Receita média vitalícia
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica do filtro: ([`A`] OU [`B`] OU [`C`]) E [`D`]

   * [!UICONTROL Metric]: número médio de ordens vitalícias
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
  [!UICONTROL Agrupar por]: `campaign` (Usar a campanha &quot;Primeiro pedido do cliente&quot; para métricas de tabela de gastos sem anúncios)
* 
  [!UICONTROL Chart Type]: `Table`

Se você tiver dúvidas ao criar essa análise ou se quiser simplesmente envolver a equipe de serviços profissionais, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Relacionados

* [Práticas recomendadas para marcação UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Como o [!DNL Google Analytics] A atribuição UTM funciona?](../analysis/utm-attributes.md)
