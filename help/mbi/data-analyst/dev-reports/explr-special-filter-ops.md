---
title: Operadores de filtro especiais
description: Saiba mais sobre alguns operadores especiais usados em filtros ao criar um relatório ou uma métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Opções de filtro

Neste artigo, vamos explorar algumas `operators` usado em `filters` when [criação de um relatório](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} ou [criação de uma métrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` para correspondência de padrões. Isso deve ser usado junto com os caracteres curingas % (para um curinga com um número variável de letras) ou _ (para uma única letra curinga).  Por exemplo, a restrição `LIKE \_ake%` retornará true para `Jake Stein`, `Jake Smith`ou `Fake Smith`.  Isso retornaria false para `Drake Smith`.

* `NOT LIKE` é semelhante à correspondência de padrões acima, mas verifica quais padrões não correspondem.

* `IS` verifica se a coluna é `NULL`ou vazio.

* `IS NOT` é semelhante a `IS` operador acima, mas verifica se há colunas não NULL.

* `IN` verifica a presença de um valor em uma lista separada por vírgulas. (por exemplo, &quot;Cor `IN` vermelho,laranja&quot; é o equivalente da cor `equal to` vermelho OU cor `equal to` laranja).

* `NOT IN` é semelhante a `IN` acima, mas verifica a ausência de um valor.
