---
title: Dados Armazenados Esperados Do Google Analytics
description: Saiba como interagir com os dados armazenados do Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Dados [!DNL Google Analytics Warehoused] esperados

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Algumas informações foram usadas com a permissão de seus amigos em [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

A integração [!DNL Google Analytics Warehoused] em [!DNL Commerce Intelligence] usa a [!DNL Google Analytics] [API de Relatórios Principais](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados ou sem sentido, confirme se as dimensões usadas são [compatíveis com uma ou mais métricas](https://ga-dev-tools.google/dimensions-metrics-explorer/) usadas na `Report Builder`.

Uma única tabela - chamada `report` - é criada no Data Warehouse.

O esquema desta tabela é composto pelas Métricas e Dimensões selecionadas durante o processo de instalação e por duas outras colunas: `start-date` e `end-date`.

Por exemplo, se você selecionou as seguintes Métricas e dimensões durante a configuração:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

A tabela seria semelhante ao exemplo abaixo.

| **Nome da coluna** | **Descrição** |
|-----|-----|
| `\_id` | Esta coluna é o `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identificador exclusivo. Esta coluna foi criada por [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Esta coluna foi criada por [!DNL Commerce Intelligence]. |
| `start-date` | Identificação do dia para o qual a linha é usada. |
| `end-date` | Identificação do dia para o qual a linha é usada. |
| `month` | Dimensão selecionada: mês da sessão, um número inteiro de dois dígitos de 01 a 12. |
| `users` | Métrica selecionada: o número total de usuários para o período solicitado. |

{style="table-layout:auto"}

## Qual é a diferença entre [!DNL Google Analytics Warehoused] e [!DNL Live Integration]

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]) e a outra não é ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação de seus dados do [!DNL Google Analytics] e oferece a capacidade de combinar o [!DNL Google Analytics] e outras fontes de dados para criar relatórios relevantes.

Veja as campanhas de anúncios [!DNL Google Analytics] para ver um exemplo do que pode ser feito do ponto de vista da manipulação. Suponha que você tenha várias campanhas de anúncios para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados, você pode criar uma coluna que localize os nomes de campanha em questão e retorne o nome da iniciativa do 4º trimestre de `Operation Dumbo`.

O aspecto de combinação permite que dados [!DNL Google Analytics] sejam unidos a outros dados para realizar análises. Por exemplo, pegue os dados de `Total Time On Site By Ad Campaign` de [!DNL Google Analytics] e junte-os aos dados de `Total Spent Per Campaign` de [!DNL Facebook Ads] para obter uma visão completa de quanto o engajamento está lhe custando.

Por outro lado, com a integração do [!DNL Google Analytics Live], cada gráfico do [!DNL Google Analytics] se parece com um pequeno silo que não está armazenado no Data Warehouse [!DNL Commerce Intelligence].

## Relacionados:

* [Conectando [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
