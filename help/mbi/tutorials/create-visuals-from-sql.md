---
title: Criar visualizações de consultas SQL
description: Saiba como familiarizar você com a terminologia usada no SQL Report Builder e fornecer uma base sólida para criar visualizações SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Developer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/xWv7O8UJ6gXxysl6oG1t24ygF-PE4LTanwyrrvoJzQ4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---

# Criar visualizações de consultas SQL

O objetivo deste tutorial é familiarizá-lo com a terminologia usada no [!DNL SQL Report Builder] e fornecer uma base sólida para a criação do `SQL visualizations`.

O [[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) é um construtor de relatórios com opções: você pode executar uma consulta com a única finalidade de recuperar uma tabela de dados, ou pode transformar esses resultados em um relatório. Este tutorial explica como criar uma visualização de uma consulta SQL.

## Terminologia

Antes de começar este tutorial, consulte a seguinte terminologia usada no `SQL Report Builder`.

- `Series`: a coluna que você deseja medir é chamada de Série no SQL Report Builder. Exemplos comuns são `revenue`, `items sold` e `marketing spend`. Pelo menos uma coluna deve ser definida como `Series` para criar uma visualização.

- `Category`: A coluna que você deseja usar para segmentar seus dados é chamada de `Category`. É exatamente como o recurso `Group By` no [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Por exemplo, se você quiser segmentar a receita vitalícia de seus clientes pela fonte de aquisição, a coluna que contém a fonte de aquisição seria especificada como `Category`. Mais de uma coluna pode ser definida como `Category`.

>[!NOTE]
>
>Datas e carimbos de data e hora também podem ser usados como `Categories`. Eles são apenas outra coluna de dados na sua query e devem ser formatados e ordenados conforme desejado na própria query.

- `Labels`: eles são aplicados como rótulos de eixo x. Ao analisar a tendência dos dados ao longo do tempo, as colunas de ano e mês são especificadas como rótulos. Mais de uma coluna pode ser definida como Rótulo.

## Etapa 1: Gravar a consulta

Lembre-se do seguinte:

- O [!DNL SQL Report Builder] usa [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Se estiver criando um relatório com uma série temporal, certifique-se de `ORDER BY` a(s) coluna(s) de carimbo de data e hora. Isso garante que os carimbos de data e hora sejam plotados na ordem correta no relatório.

- A função `EXTRACT` é ideal para ser usada na análise do dia, semana, mês ou ano do carimbo de data e hora. Isso é útil quando o `time interval` que você deseja usar no relatório é `daily`, `weekly`, `monthly` ou `yearly`.

Para começar, abra o [!DNL SQL Report Builder] clicando em **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Como exemplo, considere esta consulta que retorna o número total mensal de itens vendidos para cada produto:

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Esta consulta retorna esta tabela de resultados:

![Tabela mostrando os resultados da consulta SQL com itens vendidos por produto, ano e mês](../assets/SQL_results_table.png)

## Etapa 2: criar a visualização

Com esses resultados, *como você cria a visualização?* Para começar, clique na guia **[!UICONTROL Chart]** no painel `Results`. Isso exibe a guia `Chart settings`.

Quando uma consulta é executada pela primeira vez, o relatório pode parecer inescrutável, pois todas as colunas na consulta são representadas como uma série:

![Relatório SQL inicial com todas as colunas plotadas como séries](../assets/SQL_initial_report_results.png)

Neste exemplo, você deseja que seja um gráfico de linhas com tendência ao longo do tempo. Para criá-lo, use estas configurações:

- `Series`: Selecione a coluna `Items sold` como `Series` já que deseja medi-la. Depois de definir uma coluna `Series`, você verá uma única linha plotada no relatório.

- `Category`: Neste exemplo, você deseja exibir cada produto como uma linha diferente no relatório. Para fazer isso, você definiu `Product name` como `Category`.

- `Labels`: Use as colunas `year` e `month` como rótulos no eixo x para poder exibir `Items Sold` como tendência ao longo do tempo.

>[!NOTE]
>
>A consulta deve conter uma cláusula `ORDER BY` nos rótulos se forem colunas `date`/`time`.

Veja abaixo rapidamente como você criou essa visualização, desde a execução da consulta até a configuração do relatório:

![Demonstração animada da definição das configurações de visualização de relatório SQL](../assets/SQL_report_settings.gif)

## Etapa 3: Selecionar um `Chart Type`

Este exemplo usa o tipo de gráfico `Line`. Para usar um `chart type` diferente, clique nos ícones acima da seção de opções do gráfico para alterá-lo:

![Ícones de tipo de gráfico disponíveis, incluindo linha, barra, área e outras opções de visualização](../assets/Chart_types.png)

## Etapa 4: salvar a visualização

Se quiser usar este relatório novamente, dê um nome ao relatório e clique em **[!UICONTROL Save]** no canto superior direito.

Na lista suspensa, selecione `Chart` como `Type` e, em seguida, um painel no qual salvar o relatório.

## Encapsulamento

Quer ir um passo além? Confira as [práticas recomendadas de otimização de consulta](../best-practices/optimizing-your-sql-queries.md).
