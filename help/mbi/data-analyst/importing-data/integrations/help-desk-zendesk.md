---
title: Relatórios de Help Desk para o Zendesk
description: Saiba mais sobre os seus canais de referência mais importantes.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Relatórios de Help Desk para [!DNL Zendesk]

>[!NOTE]
>
>Isso só está disponível para clientes que estão no plano `Pro` e estão usando a nova arquitetura. Você está na nova arquitetura se tiver a seção `Data Warehouse Views` disponível após selecionar `Manage Data` na barra de ferramentas principal.

Consolidar os dados do [!DNL Zendesk] com o banco de dados transacional é uma excelente maneira de entender melhor como os clientes estão interagindo com as equipes de vendas ou de sucesso do cliente. Ela também ajuda você a saber que tipo de cliente está usando sua plataforma de suporte. Este tópico demonstra como configurar um painel para obter relatórios detalhados sobre o desempenho e o tempo do [!DNL Zendesk] em seus clientes transacionais.

Antes de começar, você deseja conectar seu [[!DNL Zendesk]](../integrations/zendesk.md). Esta análise contém [colunas calculadas avançadas](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Introdução

### Colunas a serem rastreadas

* Tabela `audits`
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* Tabela `audits_~_events`
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* Tabela `tickets`
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* Tabela `users`
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Conjuntos de filtros a serem criados

* Tabela `[!DNL Zendesk] Tickets`
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Colunas calculadas

### Colunas para criar

* Tabela **`[!DNL Zendesk] user's`**
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `nulo` and `A!=`end-user` então `Yes` quando `B` não é `null` e `B` como `%@magento.com` então `Yes` mais `No` termina

      * Substituir `@magento.com` pelo seu domínio

      * `Datatype` - `String`

* Tabela **`[!DNL Zendesk] audits_~_events`**
   * Selecione uma definição: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecione um [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* Tabela **`[!DNL Zendesk] audits`**
   * Selecione uma definição: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Selecione uma definição: `Exists`
   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* Tabela **`[!DNL Zendesk] Tickets`**
   * Selecione uma definição: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecione um [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecione um [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selecione uma definição: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Selecione um [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` alterado para `solved = 1`

   * Selecione uma definição: `Min`
   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Selecione um [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` menos `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` menos `created_at`

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

* Tabela **`customer_entity`**
   * Selecione uma definição: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL Um]: `customer_entity.email`

   * Selecione um [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Mesma Tabela > Cálculo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* Tabela **`[!DNL Zendesk] Tickets`**
   * Selecione uma definição: `Joined Column`
   * Selecione um [!UICONTROL table]: `customer_entity`
   * Selecione um [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Métricas

* **[!DNL Zendesk]Novos tíquetes**
   * `Tickets we count`

* Na tabela **`[!DNL Zendesk] tickets`**
* Esta métrica executa uma **Contagem**
* Na coluna **`id`**
* Ordenado pelo carimbo de data/hora **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tíquetes resolvidos**
   * `Tickets we count`
   * status EM `closed, solved`

* Na tabela **`[!DNL Zendesk] tickets`**
* Esta métrica executa uma **Contagem**
* Na coluna **`id`**
* Ordenado pelo carimbo de data/hora **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Usuários distintos preenchendo tíquetes**
   * `Tickets we count`

* Na tabela **`[!DNL Zendesk] tickets`**
* Esta métrica executa uma **Contagem distinta**
* Na coluna **`requester_id`**
* Ordenado pelo carimbo de data/hora **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo médio/mediano de resolução do tíquete**
   * `Tickets we count`
   * status EM `closed, solved`

* Na tabela **`[!DNL Zendesk] tickets`**
* Esta métrica executa uma **Média (ou Mediana)**
* Na coluna **`Seconds to resolution`**
* Ordenado pelo carimbo de data/hora **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo médio/mediano até a primeira resposta**
   * Tíquetes contados
   * status IN fechado, resolvido

* Na tabela **`[!DNL Zendesk] tickets`**
* Esta métrica executa uma **Média (ou Mediana)**
* Na coluna **`Seconds to first response`**
* Ordenado pelo carimbo de data/hora **`created_at`**
* [!UICONTROL Filter]:

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

### Relatórios

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status EM `new, open, pending`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status EM `solved, closed`

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
   * status EM `solved, closed`

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
   * status EM `solved, closed`

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
