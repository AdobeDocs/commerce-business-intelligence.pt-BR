---
title: Dados Armazenados Esperados Do Google Analytics
description: Saiba como interagir com os dados armazenados do Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/-Pulnv7J-TmXxL0msB6nhuMKIWbCpS0163rewp9BOvc
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 355
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
