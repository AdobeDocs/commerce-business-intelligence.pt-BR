---
title: Dados esperados do Google Adwords
description: Saiba como você pode usar o Gerenciador de Datas Warehouse para rastrear facilmente campos de dados relevantes para análise.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Esperado [!DNL Google Adwords] dados

Depois [você conectou o [!DNL Google Adwords] account](../integrations/google-adwords.md), você pode usar o [Gerenciador de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Você verá duas tabelas disponíveis para replicação na Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

A variável `campaigns` tabela *deve ser usado por padrão*, para que você possa começar sincronizando todos os campos relevantes dessa tabela.

A variável `adwords` A tabela contém quatro colunas que não estão na `campaigns` tabela:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Sempre que estiver interessado em executar uma análise que considere esses atributos, você deverá usar o `adwords` tabela.

>[!IMPORTANT]
>
>Esta tabela exclui linhas em que todas as quatro colunas são `null`.

Veja abaixo o schema esperado para ambas as tabelas.

## [!DNL Campaigns] tabela

A variável `campaigns` A tabela contém as seguintes colunas:

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

## [!DNL AdWords] tabela

A variável `adwords` A tabela contém as seguintes colunas:

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
| `adDestinationUrl` | O URL para o qual o [!DNL Adwords] tráfego de anúncios referenciados |
| `adGroup` | O nome do [!DNL Adwords] grupo de publicidade |

{style="table-layout:auto"}

Com esses dados, você pode começar a criar [métricas](../../../data-user/reports/ess-manage-data-metrics.md) e [relatórios](../../../tutorials/using-visual-report-builder.md) com base em dados de gastos e [associe-a à sua receita vitalícia para calcular o ROI](../../analysis/roi-ad-camp.md).

## Tabelas consolidadas

[!DNL Adobe] A recomenda a criação de `consolidated ad spend` para combinar os dados de todas as suas várias fontes de publicidade em uma única tabela. Isso permite usar um único conjunto de métricas para análise de publicidade.

Se você não tiver uma tabela consolidada e construir um belo painel no `adwords` você precisa replicar os relatórios ou criar métricas duplicadas para comparar esses dados com seus [!DNL Facebook Ads] dados. O uso de uma tabela consolidada permite incorporar facilmente [!DNL Facebook Ads] dados com seus existentes [!DNL Adwords] relatórios. Também é possível segmentar por plataforma de anúncios.

Se você já tiver sincronizado os campos acima, [entre em contato](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para consolidar seu investimento em anúncios.
