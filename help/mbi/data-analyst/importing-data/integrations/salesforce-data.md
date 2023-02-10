---
title: Dados esperados do Salesforce
description: Saiba mais sobre objetos suportados e não suportados em dados do Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Esperado [!DNL Salesforce] dados

[Depois que a variável [!DNL Salesforce] configuração concluída](../integrations/salesforce.md), uma tabela para cada queryable [objeto](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - nomeado `sf_/\{sobject-name}` - será criado no data warehouse.

>[!NOTE]
>
>A estrutura (colunas) de cada tabela depende dos campos contidos no objeto .

Para obter uma lista de objetos disponíveis para sua organização, consulte [!DNL Salesforce] [Obter uma documentação da Lista de objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Depois de ter uma lista de objetos, verifique o [Seção Diagrama de Relacionamento de Entidade (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] documentação para ver como as entidades se relacionam entre si.

## Objetos não suportados

Nesse momento, [!DNL Salesforce] no momento, não expõe os seguintes objetos em sua API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [O que é um objeto externo?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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

## Relacionadas:

* [Conexão [!DNL Salesforce]](../integrations/salesforce.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
