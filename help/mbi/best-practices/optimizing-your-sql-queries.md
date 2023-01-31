---
title: Otimizando Suas Consultas SQL
description: Saiba como otimizar suas consultas SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Otimizar suas consultas SQL

O Report Builder SQL permite consultar e iterar essas consultas a qualquer momento. Isso é útil quando você precisa modificar uma consulta sem ter que aguardar a conclusão de um ciclo de atualização antes de perceber uma coluna ou relatório que você criou precisa ser atualizado.

Antes da execução de um query, [[!DNL MBI] estima seu custo](https://support.magento.com/hc/en-us/articles/360016730391). O custo leva em consideração a duração e o número de recursos necessários para executar um query. Se esse custo for considerado muito alto ou se o número de linhas retornadas exceder nossos limites, a consulta não será executada. Elaboramos uma lista de recomendações para consultar seu data warehouse, o que garantirá que você esteja gravando as consultas mais simplificadas possíveis.

## Usar SELECIONAR ou Selecionar todas as colunas

A seleção de todas as colunas não resulta em uma consulta oportuna e facilmente executada. Queries que usam `SELECT *` pode levar algum tempo para ser executado, especialmente se a tabela tiver um grande número de colunas.

Por isso, recomendamos que você evite usar `SELECT *` sempre que possível e inclua apenas as colunas necessárias:

| **Em vez disso..** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style=&quot;table-layout:auto&quot;}

## Usando associações externas completas

As associações externas selecionam a totalidade das duas tabelas que estão sendo unidas, o que aumentará o custo computacional do query. Isso significa que a consulta levará mais tempo para ser executada e terá mais probabilidade de falhar, pois pode demorar mais do que o limite de execução para retornar os resultados.

Em vez de usar esse tipo de junção, considere usar uma junção interna ou esquerda. As associações internas retornam resultados somente onde tAqui está uma correspondência em colunas entre tabelas (por exemplo, `order_id` existe em ambos os `customers` e `orders` quadro); as associações à esquerda retornarão todos os resultados da tabela à esquerda (primeira) juntamente com os resultados correspondentes na tabela à direita (segunda).

Veja como podemos reescrever uma consulta COMPLETA OUTER JOIN:

| **Em vez disso..** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style=&quot;table-layout:auto&quot;}

Como você pode ver, essas consultas são idênticas de todas as maneiras, exceto pelo tipo de JOIN que usam.

## Usando várias associações

Embora você possa incluir várias associações em seu query, lembre-se de que isso pode aumentar o custo do query. Para não atingir o limite de custo, recomendamos evitar várias associações, quando possível.

## Uso de filtros

Use filtros sempre que possível. `WHERE` e `HAVING` as cláusulas filtrarão seus resultados e fornecerão apenas os dados que você realmente deseja.

## Uso de Filtros em Cláusulas JOIN

Se estiver usando um filtro ao executar uma junção, certifique-se de aplicá-lo às duas tabelas na junção. Mesmo que seja redundante, isso reduzirá o custo computacional do query e agilizará o tempo de execução.

| **Em vez disso..** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style=&quot;table-layout:auto&quot;}

## Uso de operadores

Ao gravar queries, considere usar os operadores &quot;menos caros&quot; possível. Cada query tem um custo computacional, que é determinado pelas funções, operadores e filtros que compõem a query. Alguns operadores exigem menos esforço computacional, o que os torna menos caros que outros operadores.

Os operadores de comparação (>, &lt;, = e assim por diante) são os menos caros, seguidos de [SIM. Operadores SIMILAR TO e POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html) que são os operadores mais caros.

## Uso de EXISTENTES Versus EM

Usando `EXISTS` versus `IN` depende do tipo de resultados que você está tentando retornar. Se você estiver interessado em apenas um valor, use a variável `EXISTS` cláusula em vez de `IN`. `IN` é usada juntamente com listas de valores separados por vírgula, o que aumentará o custo computacional do query.

When `IN` queries forem executados, o sistema deverá primeiro processar o subquery (a variável `IN` ), em seguida, toda a consulta com base na relação especificada no `IN` instrução. `EXISTS` O é muito mais eficiente porque a consulta não precisa ser executada várias vezes - um valor true/false é retornado ao verificar a relação especificada na query.

Para simplificar: o sistema não precisa processar tanto ao usar `EXISTS`.

| **Em vez disso..** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style=&quot;table-layout:auto&quot;}

## Usando ORDEM POR

`ORDER BY` é uma função cara no SQL e pode aumentar significativamente o custo de um query. Se você receber uma mensagem de erro informando que o custo EXPLAIN do seu query é muito alto, tente eliminar qualquer `ORDER BY`é de sua consulta, a menos que seja absolutamente necessário.

Isto não quer dizer que `ORDER BY` não pode ser usado - apenas que só deve ser usado quando necessário.

## Usando GROUP BY e ORDER BY

Embora possa haver algumas situações em que essa abordagem não esteja em conformidade com o que você está tentando fazer, a regra geral é que se você estiver usando uma `GROUP BY` e `ORDER BY`, você deve colocar as colunas em ambas as cláusulas na mesma ordem. Por exemplo:

| **Em vez disso..** | **Experimente isto!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style=&quot;table-layout:auto&quot;}

## Quebra de linha

A melhor maneira de aprender a escrever SQL - e fazê-lo com eficiência - é por tentativa e erro. Para descobrir o que funciona melhor para você, tente recriar alguns relatórios usando apenas o editor SQL.
