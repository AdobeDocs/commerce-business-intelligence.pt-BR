---
title: Dados esperados do Mixpanel
description: Explore as principais tabelas de dados que você pode importar do Mixpanel para sua conta  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '187'
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
