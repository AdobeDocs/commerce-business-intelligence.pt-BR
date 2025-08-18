---
title: Operadores de filtro especiais
description: Saiba mais sobre alguns operadores especiais usados em filtros ao criar um relatório ou uma métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Opções de filtro

Este tópico explora alguns `operators` especiais usados em `filters` ao [criar um relatório](../../tutorials/using-visual-report-builder.md){: target="_blank"} ou [criar uma métrica](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` para correspondência de padrão. Isso deve ser usado com os caracteres curinga % (para um curinga com um número variável de letras) ou _ (para uma única letra curinga).  Por exemplo, a restrição `LIKE \_ake%` retornaria true para `Jake Stein`, `Jake Smith` ou `Fake Smith`.  Retornaria falso para `Drake Smith`.

* `NOT LIKE` é semelhante à correspondência de padrões acima, mas verifica quais padrões não correspondem.

* `IS` verifica se a coluna é `NULL` ou está vazia.

* `IS NOT` é semelhante ao operador `IS` acima, mas verifica se há colunas não-NULL.

* `IN` verifica a presença de um valor em uma lista separada por vírgulas. (por exemplo, &quot;Cor `IN` vermelho,laranja&quot; é o equivalente à cor `equal to` vermelho OU cor `equal to` laranja).

* `NOT IN` é semelhante a `IN` acima, mas verifica a ausência de um valor.
