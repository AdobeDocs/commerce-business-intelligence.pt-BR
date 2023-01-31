---
title: Dados de palavras-chave do Google esperados
description: Saiba como você pode usar o Gerenciador de Datas Warehouse para rastrear facilmente campos de dados relevantes para análise.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Dados de palavras-chave do Google esperados

Depois [você conectou seu [!DNL Google Adwords] account](../integrations/google-adwords.md), você pode usar o [Gerenciador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise.

Lá, você notará duas tabelas disponíveis para replicação em seu data warehouse: `campaigns[account-id]` e `adwords[account-id]`.

O `campaigns` tabela *deve ser usada por padrão*, para começar, sincronize todos os campos relevantes da tabela.

O `adwords` a tabela contém quatro colunas que não estão no `campaigns` tabela:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

Sempre que você estiver interessado em executar uma análise que considere esses atributos, deverá usar o `adwords` tabela.

>[!IMPORTANT]
>
>Esta tabela excluirá linhas nas quais todas as quatro colunas são `null`.

Veja a seguir o schema esperado para ambas as tabelas:

## `Campaigns` tabela

O `campaigns` a tabela contém as seguintes colunas:

| **Coluna** | **Descrição** |
|-----|-----|
| `\_id` | A chave primária para a tabela |
| `accountId` | A ID da conta |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | A data de execução da campanha |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impressões do dia |
| `profileId` | A ID do perfil |
| `profileName` | O nome do perfil |
| `\_updated\_at` | A data e a hora da última atualização desta linha |

{style=&quot;table-layout:auto&quot;}

## Tabela AdWords

O `adwords` a tabela contém as seguintes colunas:

| **Coluna** | **Descrição** |
|-----|-----|
| `\_id` | A chave primária para a tabela |
| `accountId` | A ID da conta |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de cliques do dia |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Custo total da campanha do dia |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID da campanha |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome da campanha (por exemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | A data de execução da campanha |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impressões do dia |
| `profileId` | A ID do perfil |
| `profileName` | O nome do perfil |
| `\_updated\_at` | A data e a hora da última atualização desta linha |
| `keyword` | A palavra-chave da campanha |
| `adContent` | A primeira linha do texto para a campanha online |
| `adDestinationUrl` | O URL para o qual a variável [!DNL Adwords] tráfego de anúncios |
| `adGroup` | O nome do [!DNL Adwords] grupo de publicidade |

{style=&quot;table-layout:auto&quot;}

Com esses dados, você pode começar a criar [métricas ](../../../data-user/reports/ess-manage-data-metrics.md) e [relatórios](../../../tutorials/using-visual-report-builder.md) com base nos dados de gastos e [associe-a à sua receita vitalícia para calcular o ROI](../../analysis/roi-ad-camp.md).

## Tabelas consolidadas

Sempre recomendamos criar um `consolidated ad spend` tabela para combinar os dados de todas as suas várias fontes de publicidade em uma única tabela. Isso permite que você use um único conjunto de métricas para análise de publicidade.

Sem uma tabela consolidada, se você criar um belo painel na `adwords` , é necessário replicar os relatórios ou criar métricas duplicadas para comparar esses dados com a sua [!DNL Facebook Ads] dados. O uso de uma tabela consolidada permite a incorporação perfeita [!DNL Facebook Ads] com seus [!DNL Adwords] relatórios. (Não se preocupe - você também pode segmentar por plataforma de anúncio!)

Se você já sincronizou os campos acima, entre em contato conosco para consolidar o seu investimento em anúncios.
