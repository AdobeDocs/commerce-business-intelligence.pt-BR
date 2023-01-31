---
title: Esperado [!DNL Adobe Analytics] Dados
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Esperado [!DNL Adobe Analytics] Dados

O [!DNL Adobe Analytics] integração para [!DNL MBI] usa a variável [API em relatórios do Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para garantir que você obtenha os dados esperados, é possível primeiro criar um relatório no [!DNL Adobe Analytics] Espaço de trabalho com as métricas e dimensões desejadas. Isso permite verificar a compatibilidade e disponibilidade dos dados.

Uma tabela por conjunto de relatórios conectado - chamada de `report-suite-<ID>`, onde `<ID>` é uma ID exclusiva gerada por [!DNL MBI] - será criado na sua Data Warehouse.

O esquema desta tabela é composto pelas métricas e dimensões selecionadas no processo de configuração da integração. Várias colunas adicionais também são geradas por [!DNL MBI]para efeitos de identificação.

Por exemplo, se você selecionou a seguinte métrica e dimensão durante a configuração:
- `Metric`: `Page views`
- `Dimension`: `Page`

A tabela conteria estas colunas:

| Nome da coluna | Descrição |
| --- | --- |
| `_id` | Essa coluna é a chave primária. |
| `_item_hash` | [!DNL MBI] identificador exclusivo. Essa coluna é criada por [!DNL MBI]. |
| `_updated_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Ele é criado por [!DNL MBI]. |
| `start_date` | Data de início dos dados incluídos para a linha. `start_date` sempre será 00:00 do mesmo dia em uma linha. |
| `end_date` | Data final dos dados incluídos para a linha. `end_date` sempre será 23:59 do mesmo dia em uma linha. |
| `page_views` | Métrica selecionada: O número total de exibições de página para o período de tempo identificado. |
| `page` | Dimensão selecionada: Nomes de página individuais com exibições rastreadas. |

Controlar quais das métricas e dimensões selecionadas têm dados disponíveis em [!DNL MBI] usando a *sincronizar* ou *unsync* nas opções da `Data Warehouse` página. As colunas que não estão sendo sincronizadas aparecem em cinza. Se você parar de sincronizar uma coluna, poderá iniciá-la novamente mais tarde.

## Limitações atuais

Esta seção descreve as limitações do [!DNL Adobe Analytics] integração para [!DNL MBI].

| Limitação | Descrição |
| --- | --- |
| `Historical data period` | Assim como em outras integrações de terceiros, a variável [!DNL Adobe Analytics] a integração extrai uma quantidade limitada de dados históricos e, em seguida, continua a manter os dados atualizados. O período histórico é configurado para 2 semanas. |
| `Empty component combinations` | Algumas combinações de métricas e dimensões não contêm dados. Se essa combinação for selecionada para replicação, [!DNL MBI] exclui a coluna da tabela replicada. Para evitar selecionar essa combinação, primeiro você pode criar um relatório no [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) para verificar, você obterá os dados esperados. |
| `Re-authorization cadence` | Reautorização da [!DNL Adobe Analytics] no momento, a integração é necessária a cada duas semanas. Para autorizar novamente, acesse a página Editar da integração e clique em **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] O fornece dados de métrica para uma dimensão de cada vez. Se você selecionar várias dimensões durante a configuração, cada linha em seu [!DNL MBI] tabela conterá um único valor de dimensão e valores nulos para cada outra dimensão. |
