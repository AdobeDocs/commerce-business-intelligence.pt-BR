---
title: Operadores de filtro especiais
description: Saiba mais sobre alguns operadores especiais usados em filtros ao criar um relatório ou uma métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Opções de filtro

Este artigo explora alguns tópicos `operators` usado em `filters` quando [criação de um relatório](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} ou [criação de uma métrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` para correspondência de padrões. Isso deve ser usado com os caracteres curinga % (para um curinga com um número variável de letras) ou _ (para uma única letra curinga).  Por exemplo, a restrição `LIKE \_ake%` retornaria verdadeiro para `Jake Stein`, `Jake Smith`ou `Fake Smith`.  Retornaria falso por `Drake Smith`.

* `NOT LIKE` é semelhante à correspondência de padrões acima, mas verifica quais padrões não correspondem.

* `IS` verifica se a coluna é `NULL`ou em branco.

* `IS NOT` é semelhante ao `IS` operador acima, mas verifica se há colunas não-NULL.

* `IN` verifica a presença de um valor em uma lista separada por vírgulas. (por exemplo, &quot;Cor `IN` vermelho, laranja&quot; é o equivalente a cor `equal to` cor OR vermelha `equal to` laranja).

* `NOT IN` é semelhante a `IN` acima, mas verifica a ausência de um valor.
