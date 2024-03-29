---
title: Dados esperados do Salesforce
description: Saiba mais sobre objetos compatíveis e não compatíveis nos dados do Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Esperado [!DNL Salesforce] dados

Depois que a variável [[!DNL Salesforce] configuração](../integrations/salesforce.md) estiver concluído, uma tabela para cada consulta [objeto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - nomeado `sf_/\{sobject-name}` - é criado na Data Warehouse.

>[!NOTE]
>
>A estrutura (colunas) de cada tabela depende dos campos contidos no objeto.

Para obter uma lista de objetos disponíveis para sua organização, consulte a [!DNL Salesforce] [Documentação de Obter uma lista de objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Depois de ter uma lista de objetos, confira a [Seção do Diagrama de Relacionamento de Entidade (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] para ver como as entidades se relacionam entre si.

## Objetos não suportados

Atualmente, [!DNL Salesforce] No momento, o não expõe os seguintes objetos na API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [O que é um objeto externo?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
