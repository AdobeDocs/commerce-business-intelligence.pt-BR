---
title: Esperado [!DNL Adobe Analytics] Dados
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Esperado [!DNL Adobe Analytics] Dados

A variável [!DNL Adobe Analytics] integração para [!DNL MBI] usa o [API de relatórios do Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para garantir a obtenção dos dados esperados, primeiro crie um relatório no [!DNL Adobe Analytics] Espaço de trabalho com as métricas e dimensões desejadas. Isso permite verificar a compatibilidade e a disponibilidade dos dados.

Uma tabela por conjunto de relatórios conectado - chamada `report-suite-<ID>`, onde `<ID>` é uma ID exclusiva gerada pelo [!DNL MBI] - é criado na Data Warehouse.

O esquema desta tabela é composto pelas métricas e dimensões selecionadas no processo de configuração de integração. Várias colunas adicionais também são geradas pelo [!DNL MBI], para fins de identificação.

Por exemplo, se você selecionou a seguinte métrica e dimensão durante a configuração:
- `Metric`: `Page views`
- `Dimension`: `Page`

A tabela conteria estas colunas:

| Nome da coluna | Descrição |
| --- | --- |
| `_id` | Essa coluna é a chave primária. |
| `_item_hash` | [!DNL MBI] identificador exclusivo. Esta coluna é criada por [!DNL MBI]. |
| `_updated_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Ele é criado por [!DNL MBI]. |
| `start_date` | Data inicial dos dados incluídos na linha. `start_date` é sempre 00:00 do mesmo dia em uma linha. |
| `end_date` | Data final dos dados incluídos na linha. `end_date` é sempre 23:59 do mesmo dia em uma linha. |
| `page_views` | Métrica selecionada: o número total de exibições de página para o período identificado. |
| `page` | Dimensão selecionada: nomes de página individuais com exibições rastreadas. |

Controle quais das métricas e dimensões selecionadas têm dados disponíveis em sua [!DNL MBI] tabela usando o *sincronizar* ou *dessincronizar* opções no `Data Warehouse` página. As colunas que não estão sendo sincronizadas no momento aparecem em cinza. Se você parar de sincronizar uma coluna, poderá começar a sincronizá-la novamente mais tarde.

## Limitações atuais

Esta seção descreve as limitações do [!DNL Adobe Analytics] integração para [!DNL MBI].

| Limitação | Descrição |
| --- | --- |
| `Historical data period` | Assim como em outras integrações de terceiros, a variável [!DNL Adobe Analytics] a integração extrai uma quantidade limitada de dados históricos e continua a manter os dados atualizados. O período histórico é configurado para 2 semanas. |
| `Empty component combinations` | Algumas combinações de métricas e dimensões não contêm dados. Se essa combinação for selecionada para replicação, [!DNL MBI] exclui a coluna da tabela replicada. Para evitar selecionar essa combinação, primeiro você pode criar um relatório no [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) para verificar se você obtém os dados esperados. |
| `Re-authorization cadence` | Reautorização do [!DNL Adobe Analytics] A integração do é necessária a cada duas semanas. Para reautorizar, vá para a página Editar da integração e clique em **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] O fornece dados de métrica para uma dimensão por vez. Se você selecionar várias dimensões durante a configuração, cada linha em seu [!DNL MBI] a tabela contém um único valor de dimensão e nulos para cada outra dimensão. |
