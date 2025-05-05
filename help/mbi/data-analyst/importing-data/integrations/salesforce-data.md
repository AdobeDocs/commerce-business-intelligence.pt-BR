---
title: Dados esperados do Salesforce
description: Saiba mais sobre objetos compatíveis e não compatíveis nos dados do Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Dados [!DNL Salesforce] esperados

Após a conclusão da [[!DNL Salesforce] configuração](../integrations/salesforce.md), uma tabela para cada [objeto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) consultável - denominado `sf_/\{sobject-name}` - será criada na sua Data Warehouse.

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
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
