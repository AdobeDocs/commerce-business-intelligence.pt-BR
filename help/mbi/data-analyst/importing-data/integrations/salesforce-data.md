---
title: Dados esperados do Salesforce
description: Saiba mais sobre objetos compatíveis e não compatíveis com dados do Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/eBX3Y0luu60A8PSAF43H6O3fsYjJnSWzyIybSOcSELE
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 117
ht-degree: 0%

---

# Dados [!DNL Salesforce] esperados

Após a conclusão da [[!DNL Salesforce] configuração](../integrations/salesforce.md), uma tabela para cada [objeto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) consultável - denominado `sf_/\{sobject-name}` - será criada em sua Data Warehouse.

>[!NOTE]
>
>A estrutura (colunas) de cada tabela depende dos campos contidos no objeto.

Para obter uma lista de objetos disponíveis para sua organização, consulte a [!DNL Salesforce] [documentação sobre Obter uma Lista de Objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Depois de ter uma lista de objetos, verifique a [seção ERD (Diagrama de Relação de Entidade)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) da documentação [!DNL Salesforce] para ver como as entidades se relacionam entre si.

## Objetos não suportados

Atualmente, [!DNL Salesforce] não expõe os seguintes objetos em suas APIs:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [O que é um Objeto Externo?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Relacionados:

* [Conectando [!DNL Salesforce]](../integrations/salesforce.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
