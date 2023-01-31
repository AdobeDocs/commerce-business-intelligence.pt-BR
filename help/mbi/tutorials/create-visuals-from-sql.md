---
title: Criar Visualizações de Consultas SQL
description: Saiba como familiarizar você com a terminologia usada no SQL Report Builder e fornecer uma base sólida para a criação de visualizações SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Criar Visualizações de Consultas SQL

O objetivo deste tutorial é familiarizar você com a terminologia usada na variável `SQL Report Builder` e dar-lhe uma base sólida para criar `SQL visualizations`.

O [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) O é um construtor de relatórios com opções: você pode executar um query com o único objetivo de recuperar uma tabela de dados, ou pode transformar esses resultados em um relatório. Este tutorial explica como criar uma visualização a partir de uma consulta SQL.

## Terminologia

Antes de começar este tutorial, consulte a seguinte terminologia usada na variável `SQL Report Builder`.

- `Series`: A coluna que você deseja medir é chamada de Série no Report Builder SQL. Exemplos comuns são `revenue`, `items sold`e `marketing spend`. Pelo menos uma coluna deve ser definida como `Series` para criar uma visualização.

- `Category`: A coluna que deseja usar para segmentar seus dados é chamada de `Category` É como o `Group By` no [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Por exemplo, se você deseja segmentar a receita vitalícia de seus clientes pela fonte de aquisição, a coluna que contém a fonte de aquisição seria especificada como `Category`. É possível definir mais de uma coluna como uma `Category`.

>[!NOTE]
>
>Datas e carimbos de data e hora também podem ser usados como `Categories`. Eles são apenas outra coluna de dados em seu query e devem ser formatados e ordenados conforme desejado no próprio query.

- `Labels`: Elas são aplicadas como rótulos de eixo x. Ao analisar tendências de dados ao longo do tempo, as colunas de ano e mês geralmente são especificadas como rótulos. Mais de uma coluna pode ser definida como Rótulo.

## Etapa 1: Escreva a consulta

Lembre-se do seguinte:

- O `SQL Report Builder` uses [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Se você estiver criando um relatório com uma série de tempo, certifique-se de `ORDER BY` a(s) coluna(s) de carimbo de data e hora. Isso garantirá que os carimbos de data e hora sejam representados na ordem correta no relatório.

- O `EXTRACT` é ideal para usar na análise do dia, semana, mês ou ano do carimbo de data e hora. Isso é útil quando a variável `time interval` você deseja usar no relatório `daily`, `weekly`, `monthly`ou `yearly`.

Para começar, abra o `SQL Report Builder` clicando em **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Como exemplo, considere essa query que retorna o número total mensal de itens vendidos para cada produto:

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

## Etapa 2: Criar a visualização

Com esses resultados, *como criar a visualização?* Para começar, clique no botão **[!UICONTROL Chart]** na guia no `Results` painel. Isso exibirá a variável `Chart settings` guia .

Quando um query é executado pela primeira vez, o relatório pode parecer intrincável porque todas as colunas no query são plotadas como uma série:

![](../assets/SQL_initial_report_results.png)

Para este exemplo, queremos que este seja um gráfico de linhas que apresente tendências ao longo do tempo. Para criá-lo, use estas configurações:

- `Series`: Selecione o `Items sold` coluna como `Series` já que queremos medir. Depois de definir uma `Series` , você verá uma única linha plotada no relatório.

- `Category`: Neste exemplo, queremos exibir cada produto como uma linha diferente no relatório. Para fazer isso, definimos `Product name` como `Category`.

- `Labels`: Usar as colunas `year` e `month` como rótulos no eixo x para poder visualizar `Items Sold` como tendência ao longo do tempo.

>[!NOTE]
>
>O query deve conter um `ORDER BY` nos rótulos, se estiverem `date`/`time` colunas.

Veja a seguir uma rápida visão de como criamos essa visualização, da execução do query à configuração do relatório:

![](../assets/SQL_report_settings.gif)

## Etapa 3: Selecione um `Chart Type`

Esse exemplo usa a variável `Line` tipo de gráfico. Para usar um `chart type`, clique nos ícones acima da seção de opções do gráfico para alterá-lo:

![](../assets/Chart_types.png)

## Etapa 4: Salvar a visualização

Se quiser usar este relatório novamente, dê um nome a ele e clique em **[!UICONTROL Save]** no canto superior direito.

Na lista suspensa , selecione `Chart` como `Type` e, em seguida, um painel para salvar o relatório.

## Parabéns! Você terminou.

Quer dar um passo além? Confira o [práticas recomendadas de otimização de consulta](../best-practices/optimizing-your-sql-queries.md).
