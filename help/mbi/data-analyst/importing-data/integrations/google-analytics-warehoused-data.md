---
title: Dados Armazenados De Google Analytics Esperados
description: Saiba como interagir com os dados armazenados do Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Esperado [!DNL Google Analytics Warehoused] Dados

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Algumas informações foram usadas com a permissão de seus amigos em [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integração no [!DNL Commerce Intelligence] usa o [!DNL Google Analytics] [API de relatórios principais](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados ou absurdos, confirme se as dimensões usadas são [compatível com uma ou mais métricas](https://ga-dev-tools.google/dimensions-metrics-explorer/) que você usa na `Report Builder`.

Uma única tabela - chamada `report` - é criado na Data Warehouse.

O esquema desta tabela é composto pelas Métricas e Dimension selecionadas durante o processo de configuração e por duas outras colunas: `start-date` e `end-date`.

Se, por exemplo, você selecionou as seguintes métricas e Dimension durante a configuração:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

A tabela seria semelhante ao exemplo abaixo.

| **Nome da coluna** | **Descrição** |
|-----|-----|
| `\_id` | Essa coluna é a `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identificador exclusivo. Esta coluna é criada por [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Esta coluna é criada por [!DNL Commerce Intelligence]. |
| `start-date` | Identificação do dia para o qual a linha é usada. |
| `end-date` | Identificação do dia para o qual a linha é usada. |
| `month` | Dimensão selecionada: mês da sessão, um número inteiro de dois dígitos de 01 a 12. |
| `users` | Métrica selecionada: o número total de usuários para o período solicitado. |

{style="table-layout:auto"}

## Qual é a diferença entre [!DNL Google Analytics Warehoused] e [!DNL Live Integration]

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]), e o outro não ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação do [!DNL Google Analytics] dados e oferece a capacidade de combinar [!DNL Google Analytics] e outras fontes de dados para criar relatórios relevantes.

Examinar [!DNL Google Analytics] Adicione campanhas para obter um exemplo do que pode ser feito do ponto de vista da manipulação. Suponha que você tenha várias campanhas de anúncios para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados, é possível criar uma coluna que localize os nomes de campanha em questão e retorne o nome da iniciativa do quarto trimestre de `Operation Dumbo`.

O aspecto de combinação permite [!DNL Google Analytics] dados a serem unidos a outros dados para realizar análises. Por exemplo, considere `Total Time On Site By Ad Campaign` dados de [!DNL Google Analytics] e uni-lo contra `Total Spent Per Campaign` dados de [!DNL Facebook Ads] para obter uma visão completa de quanto o engajamento está custando a você.

Com o [!DNL Google Analytics Live] integração, por outro lado, cada [!DNL Google Analytics] O gráfico é como um pequeno silo que não é armazenado em seu [!DNL Commerce Intelligence] Data Warehouse.

## Relacionados:

* [Conectando [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
