---
title: Otimização das consultas SQL
description: Saiba como otimizar suas consultas de SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Otimizar suas consultas de SQL

O [!DNL SQL Report Builder] permite consultar e iterar nessas consultas a qualquer momento. Isso é útil quando você precisa modificar uma consulta sem ter que esperar o término de um ciclo de atualização antes de perceber que uma coluna ou relatório criado precisa ser atualizado.

Antes da execução de uma consulta, [[!DNL Commerce Intelligence] estima seu custo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html?lang=pt-BR). O custo considera o tempo e o número de recursos necessários para executar uma consulta. Se esse custo for considerado muito alto ou se o número de linhas retornadas exceder os limites [!DNL Commerce Intelligence], a consulta falhará. Para consultar sua [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md), o que garante que você esteja gravando as consultas mais simples possíveis, a Adobe recomenda o seguinte.

## Utilização de SELECIONAR ou Seleção de Todas as Colunas

Selecionar todas as colunas não possibilita uma consulta oportuna e facilmente executada. As consultas que usam `SELECT *` podem demorar um pouco para serem executadas, especialmente se a tabela tiver muitas colunas.

Por isso, a Adobe recomenda que você evite usar o `SELECT *` sempre que possível e inclua apenas as colunas necessárias:

| **Em vez disso...** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## Uso de Junções Externas Completas

Junções externas selecionam a totalidade das duas tabelas sendo unidas, o que aumenta o custo computacional da consulta. Isso significa que sua consulta demora mais para ser executada e tem mais probabilidade de falha, pois pode levar mais tempo do que o limite de execução para retornar os resultados.

Em vez de usar esse tipo de junção, considere usar uma junção interna ou esquerda. As junções internas retornam resultados somente quando há uma correspondência de colunas entre tabelas (por exemplo, `order_id` existe em uma tabela `customers` e `orders` típicas). As junções à esquerda retornam todos os resultados da tabela à esquerda (primeira) juntamente com os resultados correspondentes na tabela à direita (segunda).

Veja como você pode reescrever uma consulta FULL OUTER JOIN:

| **Em vez disso...** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

Essas consultas são idênticas em todos os aspectos, exceto pelo tipo de JOIN que usam.

## Uso de Várias Associações

Embora você possa incluir várias associações em sua consulta, lembre-se de que isso pode aumentar o custo da consulta. Para não atingir o limite de custo, a Adobe recomenda evitar várias associações sempre que possível.

## Utilização de filtros

Use filtros sempre que possível. As cláusulas `WHERE` e `HAVING` filtram seus resultados e fornecem apenas os dados que você realmente deseja.

## Uso de Filtros em Cláusulas JOIN

Se estiver usando um filtro ao executar uma associação, certifique-se de aplicá-lo a ambas as tabelas na associação. Mesmo que seja redundante, isso reduz o custo computacional do query e reduz o tempo de execução.

| **Em vez disso...** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## Uso de operadores

Ao gravar consultas, considere usar os operadores &quot;mais baratos&quot; possíveis. Cada consulta tem um custo computacional, que é determinado pelas funções, operadores e filtros que compõem a consulta. Alguns operadores exigem menos esforço computacional, o que os torna mais baratos do que outros operadores.

Os operadores de comparação (>, &lt;, = e assim por diante) são os mais baratos, seguidos por [LIKE. SEMELHANTE AOS operadores POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html), que são os operadores mais caros.

## Uso de EXISTS versus IN

Usar `EXISTS` versus `IN` depende do tipo de resultados que você está tentando retornar. Se você estiver interessado apenas em um único valor, use a cláusula `EXISTS` em vez de `IN`. `IN` é usado com listas de valores separados por vírgula, o que aumenta o custo computacional da consulta.

Quando as consultas `IN` são executadas, o sistema deve primeiro processar a subconsulta (a instrução `IN`) e depois a consulta inteira com base na relação especificada na instrução `IN`. `EXISTS` é muito mais eficiente porque a consulta não precisa ser executada várias vezes - um valor verdadeiro/falso é retornado ao verificar a relação especificada na consulta.

Simplificando: o sistema não precisa processar tanto ao usar o `EXISTS`.

| **Em vez disso...** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## Usando ORDER BY

`ORDER BY` é uma função cara no SQL e pode aumentar significativamente o custo de uma consulta. Se você receber uma mensagem de erro dizendo que o custo EXPLICAR da sua consulta é muito alto, tente eliminar qualquer `ORDER BY`s da sua consulta, a menos que seja necessário.

Isso não quer dizer que `ORDER BY` não possa ser usado; apenas que ele só deve ser usado quando necessário.

## Usando GROUP BY e ORDER BY

Pode haver algumas situações em que essa abordagem não esteja em conformidade com o que você está tentando fazer. A regra geral é que, se você estiver usando um `GROUP BY` e `ORDER BY`, você deve colocar as colunas em ambas as cláusulas na mesma ordem. Por exemplo:

| **Em vez disso...** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## Encapsulamento

A melhor maneira de aprender a escrever SQL - e fazê-lo com eficiência - é por meio de tentativa e erro. Para descobrir o que funciona melhor para você, tente recriar alguns relatórios usando apenas o editor SQL.
