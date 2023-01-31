---
title: Dados esperados do painel misto
description: Explore as principais tabelas de dados que você pode importar do Mixpanel para o [!DNL MBI] conta.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Esperado [!DNL Mixpanel] dados

Depois [você conectou seu [!DNL Mixpanel] account](../integrations/mixpanel.md), você pode usar o [Gerenciador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise.

Neste artigo, exploramos as principais tabelas de dados que podem ser importadas de [!DNL Mixpanel] em seu [!DNL MBI] conta. As tabelas a seguir serão criadas no data warehouse após conectar o Mixpanel. Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

>[!NOTE]
>
>Devido às limitações da variável [!DNL Mixpanel] API, dados históricos - dados anteriores a sete (7) dias a partir da data de conexão com o [!DNL MBI] - não serão replicados.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Esta tabela contém dados brutos do evento, incluindo o evento, as datas do evento e o bucket da plataforma. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Esta tabela contém dados sobre seus funis, incluindo a ID do funil, o comprimento do funil (# de dias que o usuário precisa concluir o funil) e as datas inicial e final do funil. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Ele contém dados do People Analytics, incluindo IDs de sessão, informações de página e usuário e a data/hora em que o usuário foi visto pela última vez. |

{style=&quot;table-layout:auto&quot;}

## Documentação relacionada

* [Conexão [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
