---
title: Dados esperados do Google Adwords
description: Saiba como você pode usar o Gerenciador de Datas Warehouse para rastrear facilmente campos de dados relevantes para análise.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Dados [!DNL Google Adwords] esperados

Depois de [conectar sua [!DNL Google Adwords] conta](../integrations/google-adwords.md), você poderá usar o [Gerenciador de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Você verá duas tabelas disponíveis para replicação na Data Warehouse:

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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | A data em que a campanha foi executada |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impressões do dia |
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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | A data em que a campanha foi executada |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impressões do dia |
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

Se você já tiver sincronizado os campos acima, [contate-nos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) para consolidar seu investimento em anúncios.
