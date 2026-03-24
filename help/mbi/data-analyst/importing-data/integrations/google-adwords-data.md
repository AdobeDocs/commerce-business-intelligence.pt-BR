---
title: Dados esperados do Google Adwords
description: Saiba como você pode usar o Data Warehouse Manager para rastrear facilmente campos de dados relevantes para análise.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iCKOCRAELybmKfHS8F7XaKpEx9blpkRK0i0e-eEYJgU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# Dados [!DNL Google Adwords] esperados

Depois de [conectar sua [!DNL Google Adwords] conta](../integrations/google-adwords.md), você poderá usar o [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Lá, você observa duas tabelas disponíveis para replicação no Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

A tabela `campaigns` *deve ser usada por padrão*, assim, você pode começar sincronizando todos os campos relevantes dessa tabela.

A tabela `adwords` contém quatro colunas que não estão na tabela `campaigns`:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Sempre que estiver interessado em executar uma análise que considere esses atributos, você deve usar a tabela `adwords`.

>[!IMPORTANT]
>
>Esta tabela exclui linhas em que todas as quatro colunas são `null`.

Veja abaixo o schema esperado para ambas as tabelas.

## Tabela [!DNL Campaigns]

A tabela `campaigns` contém as seguintes colunas:

| **Coluna** | **Descrição** |
|-----|-----|
| `\_id` | A chave primária da tabela |
| `accountId` | A ID da conta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | A data em que a campanha foi executada |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Número de impressões do dia |
| `profileId` | A ID do perfil |
| `profileName` | O nome do perfil |
| `\_updated\_at` | A data e a hora da última atualização desta linha |

{style="table-layout:auto"}

## Tabela [!DNL AdWords]

A tabela `adwords` contém as seguintes colunas:

| **Coluna** | **Descrição** |
|-----|-----|
| `\_id` | A chave primária da tabela |
| `accountId` | A ID da conta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | A data em que a campanha foi executada |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Número de impressões do dia |
| `profileId` | A ID do perfil |
| `profileName` | O nome do perfil |
| `\_updated\_at` | A data e a hora da última atualização desta linha |
| `keyword` | A palavra-chave da campanha |
| `adContent` | A primeira linha do texto para a campanha online |
| `adDestinationUrl` | A URL para a qual o [!DNL Adwords] anúncios referenciou tráfego |
| `adGroup` | O nome do grupo de publicidade [!DNL Adwords] |

{style="table-layout:auto"}

Usando estes dados, você pode começar a criar [métricas](../../../data-user/reports/ess-manage-data-metrics.md) e [relatórios](../../../tutorials/using-visual-report-builder.md) com base nos dados de gastos e [combiná-los com sua receita vitalícia para calcular o ROI](../../analysis/roi-ad-camp.md).

## Tabelas consolidadas

A [!DNL Adobe] recomenda criar uma tabela `consolidated ad spend` para combinar os dados de todas as suas várias fontes de publicidade em uma única tabela. Isso permite usar um único conjunto de métricas para análise de publicidade.

Se você não tiver uma tabela consolidada e criar um painel bonito na tabela `adwords`, precisará replicar os relatórios ou criar métricas duplicadas para comparar esses dados aos seus dados do [!DNL Facebook Ads]. Usar uma tabela consolidada permite incorporar facilmente os dados do [!DNL Facebook Ads] aos seus relatórios existentes do [!DNL Adwords]. Também é possível segmentar por plataforma de anúncios.

Se você já tiver sincronizado os campos acima, [contate-nos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para consolidar seu investimento em anúncios.
