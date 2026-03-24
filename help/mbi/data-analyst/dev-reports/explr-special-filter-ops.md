---
title: Operadores de filtro especiais
description: Saiba mais sobre alguns operadores especiais usados em filtros ao criar um relatório ou uma métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 143
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
