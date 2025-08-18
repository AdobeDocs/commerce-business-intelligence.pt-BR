---
title: Dados  [!DNL Adobe Analytics]  esperados
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
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
| `Empty component combinations` | Algumas combinações de métricas e dimensões não contêm dados. Se essa combinação for selecionada para replicação, [!DNL Commerce Intelligence] excluirá a coluna da tabela replicada. Para evitar a seleção dessa combinação, primeiro crie um relatório no [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) para verificar se recebeu os dados esperados. |
| `Re-authorization cadence` | A reautorização da integração do [!DNL Adobe Analytics] é necessária a cada duas semanas. Para reautorizar, vá para a página Editar da integração e clique em **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fornece dados de métrica para uma dimensão de cada vez. Se você selecionar várias dimensões durante a configuração, cada linha na tabela [!DNL Commerce Intelligence] conterá um único valor de dimensão e valores nulos para cada outra dimensão. |
