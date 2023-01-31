---
title: Relatórios do Help Desk para o Zendesk
description: Saiba mais sobre seus canais de referência mais valiosos.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Relatórios do Help Desk para [!DNL Zendesk]

>[!NOTE]
>
>Isso só está disponível para clientes que estão no `Pro` planejar e usar a nova arquitetura. Você está no [nova arquitetura](https://support.magento.com/hc/en-us/articles/360016503052-New-Architecture-FAQ) se você tiver o `Data Warehouse Views` seção disponível após a seleção `Manage Data` na barra de ferramentas principal.

Consolidação do [!DNL Zendesk] os dados com seu banco de dados transacional são uma excelente maneira de entender melhor como seus clientes interagem com suas equipes de vendas ou de sucesso do cliente e que tipo de cliente está utilizando sua plataforma de suporte. Neste artigo, demonstramos como configurar um painel para obter relatórios granulares sobre o [!DNL Zendesk] desempenho e vinculação aos clientes transacionais.

Antes de começar, você desejará se conectar [[!DNL Zendesk]](../integrations/zendesk.md). Esta análise contém [colunas calculadas avançadas](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Introdução

### Colunas a serem rastreadas

* `audits` tabela
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` tabela
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` tabela
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` tabela
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Conjuntos de filtros para criar

* `[!DNL Zendesk] Tickets` tabela
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Colunas calculadas

### Colunas a serem criadas

* **`[!DNL Zendesk] user's`** tabela
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` when `B` não é `null` e `B` like `%@magento.com` then `Yes` else `No` end

      * Substituir `@magento.com` com seu domínio

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** tabela
   * Selecione uma definição: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Selecione um [!UICONTROL table]: `[Zendesk] users`
   * Selecione um [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** tabela
   * Selecione uma definição: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * Selecione um [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Selecione uma definição: `Exists`
   * Selecione um [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[Zendesk] Tickets`** tabela
   * Selecione uma definição: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Selecione um [!UICONTROL table]: `[Zendesk] users`
   * Selecione um [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `[Zendesk] users`
   * Selecione um [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Selecione uma definição: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * Selecione um [!UICONTROL table]: `[Zendesk] audits`
   * Selecione um [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` alterado para `solved = 1`

   * Selecione uma definição: `Min`
   * Selecione um [!UICONTROL table]: `[Zendesk] audits`
   * Selecione um [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` minus `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` minus `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Mesma Tabela > Cálculo&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Número inteiro

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Mesma Tabela > Cálculo&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` - `String`


* **`customer_entity`** tabela
   * Selecione uma definição: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.email`
   * 

      [!UICONTROL Um]: `customer_entity.email`

   * Selecione um [!UICONTROL table]: `[Zendesk] tickets`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Mesma Tabela > Cálculo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[Zendesk] Tickets`** tabela
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Métricas

* **[!DNL Zendesk]Novos ingressos**
   * `Tickets we count`

* No **`[Zendesk] tickets`** tabela
* Essa métrica executa um **Contagem**
* No **`id`** column
* Solicitado pela **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tíquetes resolvidos**
   * `Tickets we count`
   * status IN `closed, solved`

* No **`[Zendesk] tickets`** tabela
* Essa métrica executa um **Contagem**
* No **`id`** column
* Solicitado pela **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Usuários distintos preenchendo tíquetes**
   * `Tickets we count`

* No **`[Zendesk] tickets`** tabela
* Essa métrica executa um **Contagem distinta**
* No **`requester_id`** column
* Solicitado pela **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo médio/mediano de resolução do tíquete**
   * `Tickets we count`
   * status IN `closed, solved`

* No **`[Zendesk] tickets`** tabela
* Essa métrica executa uma **Média (ou Média)**
* No **`Seconds to resolution`** column
* Solicitado pela **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Média/tempo mediano até à primeira resposta**
   * Tíquetes que contamos
   * status EM fechado, resolvido

* No **`[Zendesk] tickets`** tabela
* Essa métrica executa uma **Média (ou Média)**
* No **`Seconds to first response`** column
* Solicitado pela **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

### Relatórios

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Métrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* Métrica `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Métrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Métrica `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Métrica `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [!UICONTROL Métrica]: Users

* Métrica `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
