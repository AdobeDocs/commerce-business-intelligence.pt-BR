---
title: Dados esperados do Mixpanel
description: Explore as principais tabelas de dados que você pode importar do Mixpanel para o [!DNL MBI] conta.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Esperado [!DNL Mixpanel] dados

Depois [você conectou o [!DNL Mixpanel] account](../integrations/mixpanel.md), você pode usar o [Gerenciador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este artigo explora as principais tabelas de dados que podem ser importadas do [!DNL Mixpanel] no seu [!DNL MBI] conta. As tabelas a seguir serão criadas na Data Warehouse após a conexão do Mixpanel. Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

>[!NOTE]
>
>Devido às limitações do [!DNL Mixpanel] API, dados históricos - dados com mais de sete (7) dias a partir da data de conexão até [!DNL MBI] - não é replicado.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Essa tabela contém dados brutos do evento, incluindo o evento, as datas do evento e o bucket da plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Essa tabela contém dados sobre seus funis, incluindo a ID do funil, a duração do funil (número de dias que o usuário tem para concluir o funil) e as datas de início e término do funil. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Ele contém dados do People Analytics, incluindo IDs de sessão, informações de página e usuário e data/hora em que o usuário foi visto pela última vez. |

{style="table-layout:auto"}

## Documentação relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
