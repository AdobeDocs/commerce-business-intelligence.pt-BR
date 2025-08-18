---
title: Criar visualizações de consultas SQL
description: Saiba como familiarizar você com a terminologia usada no SQL Report Builder e fornecer uma base sólida para criar visualizações SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '623'
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

![](../assets/SQL_results_table.png)

## Etapa 2: criar a visualização

Com esses resultados, *como você cria a visualização?* Para começar, clique na guia **[!UICONTROL Chart]** no painel `Results`. Isso exibe a guia `Chart settings`.

Quando uma consulta é executada pela primeira vez, o relatório pode parecer inescrutável, pois todas as colunas na consulta são representadas como uma série:

![](../assets/SQL_initial_report_results.png)

Neste exemplo, você deseja que seja um gráfico de linhas com tendência ao longo do tempo. Para criá-lo, use estas configurações:

- `Series`: Selecione a coluna `Items sold` como `Series` já que deseja medi-la. Depois de definir uma coluna `Series`, você verá uma única linha plotada no relatório.

- `Category`: Neste exemplo, você deseja exibir cada produto como uma linha diferente no relatório. Para fazer isso, você definiu `Product name` como `Category`.

- `Labels`: Use as colunas `year` e `month` como rótulos no eixo x para poder exibir `Items Sold` como tendência ao longo do tempo.

>[!NOTE]
>
>A consulta deve conter uma cláusula `ORDER BY` nos rótulos se forem colunas `date`/`time`.

Veja abaixo rapidamente como você criou essa visualização, desde a execução da consulta até a configuração do relatório:

![](../assets/SQL_report_settings.gif)

## Etapa 3: Selecionar um `Chart Type`

Este exemplo usa o tipo de gráfico `Line`. Para usar um `chart type` diferente, clique nos ícones acima da seção de opções do gráfico para alterá-lo:

![](../assets/Chart_types.png)

## Etapa 4: salvar a visualização

Se quiser usar este relatório novamente, dê um nome ao relatório e clique em **[!UICONTROL Save]** no canto superior direito.

Na lista suspensa, selecione `Chart` como `Type` e, em seguida, um painel no qual salvar o relatório.

## Encapsulamento

Quer ir um passo além? Confira as [práticas recomendadas de otimização de consulta](../best-practices/optimizing-your-sql-queries.md).
