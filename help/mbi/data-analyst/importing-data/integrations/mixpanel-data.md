---
title: Dados esperados do Mixpanel
description: Explore as principais tabelas de dados que você pode importar do Mixpanel para sua conta  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# Dados [!DNL Mixpanel] esperados

Depois de [conectar sua [!DNL Mixpanel] conta](../integrations/mixpanel.md), você poderá usar o [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico explora as principais tabelas de dados que você pode importar de [!DNL Mixpanel] para sua conta do [!DNL Commerce Intelligence]. As tabelas a seguir serão criadas no Data Warehouse após a conexão com [!DNL Mixpanel]. Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

>[!NOTE]
>
>Devido às limitações da API [!DNL Mixpanel], os dados históricos - dados com mais de sete (7) dias a partir da data de conexão com [!DNL Commerce Intelligence] - não são replicados.

| **Nome da Tabela** | **Descrição** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Essa tabela contém dados brutos do evento, incluindo o evento, as datas do evento e o bucket da plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Esta tabela contém dados sobre seus funis, incluindo a funnel ID, a duração do funnel (número de dias que o usuário tem para concluir o funnel) e as datas de início e término do funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Ele contém dados do People Analytics, incluindo IDs de sessão, informações de página e usuário e data/hora em que o usuário foi visto pela última vez. |

{style="table-layout:auto"}

## Documentação relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
