---
title: Dados  [!DNL Adobe Analytics]  esperados
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/vA-1cABpxQNwI8xTF4Elkgv2geudkp5tnBH1l6-PZiY
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 400
ht-degree: 0%

---

# Dados [!DNL Adobe Analytics] esperados

A integração [!DNL Adobe Analytics] para [!DNL Adobe Commerce Intelligence] usa a [API de relatórios do Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para garantir a obtenção dos dados esperados, primeiro você pode criar um relatório no Workspace [!DNL Adobe Analytics] com as métricas e dimensões desejadas. Isso permite verificar a compatibilidade e a disponibilidade dos dados.

Uma tabela por conjunto de relatórios conectado chamada `report-suite-<ID>` (onde `<ID>` é um identificador exclusivo gerado por [!DNL Commerce Intelligence]) é criada em sua Data Warehouse.

O esquema desta tabela é composto pelas métricas e dimensões selecionadas no processo de configuração de integração. Várias colunas adicionais também são geradas por [!DNL Commerce Intelligence], para fins de identificação.

Por exemplo, se você selecionou a seguinte métrica e dimensão durante a configuração:
- `Metric`: `Page views`
- `Dimension`: `Page`

A tabela conteria estas colunas:

| Nome da coluna | Descrição |
| --- | --- |
| `_id` | Essa coluna é a chave primária. |
| `_item_hash` | [!DNL Commerce Intelligence] identificador exclusivo. Esta coluna foi criada por [!DNL Commerce Intelligence]. |
| `_updated_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Foi criado por [!DNL Commerce Intelligence]. |
| `start_date` | Data inicial dos dados incluídos na linha. `start_date` é sempre 00:00 do mesmo dia em uma linha. |
| `end_date` | Data final dos dados incluídos na linha. `end_date` é sempre 23:59 do mesmo dia em uma linha. |
| `page_views` | Métrica selecionada: o número total de exibições de página para o período identificado. |
| `page` | Dimensão selecionada: nomes de página individuais com exibições rastreadas. |

Controle quais das métricas e dimensões selecionadas têm dados disponíveis na tabela [!DNL Commerce Intelligence] usando as opções *sincronizar* ou *dessincronizar* na página `Data Warehouse`. As colunas que não estão sendo sincronizadas no momento aparecem em cinza. Se você parar de sincronizar uma coluna, poderá começar a sincronizá-la novamente mais tarde.

## Limitações atuais

Esta seção descreve as limitações da integração do [!DNL Adobe Analytics] para [!DNL Commerce Intelligence].

| Limitação | Descrição |
| --- | --- |
| `Historical data period` | Assim como em outras integrações de terceiros, a integração do [!DNL Adobe Analytics] extrai uma quantidade limitada de dados históricos e continua a manter os dados atualizados. O período histórico é configurado para 2 semanas. |
| `Empty component combinations` | Algumas combinações de métricas e dimensões não contêm dados. Se essa combinação for selecionada para replicação, [!DNL Commerce Intelligence] excluirá a coluna da tabela replicada. Para evitar a seleção dessa combinação, primeiro crie um relatório no [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=pt-BR) para verificar se recebeu os dados esperados. |
| `Re-authorization cadence` | A reautorização da integração do [!DNL Adobe Analytics] é necessária a cada duas semanas. Para reautorizar, vá para a página Editar da integração e clique em **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fornece dados de métrica para uma dimensão de cada vez. Se você selecionar várias dimensões durante a configuração, cada linha na tabela [!DNL Commerce Intelligence] conterá um único valor de dimensão e valores nulos para cada outra dimensão. |
