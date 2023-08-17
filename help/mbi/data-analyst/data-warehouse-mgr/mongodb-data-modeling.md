---
title: Modelagem de dados do MongoDB
description: Saiba como evitar padrões de dados que representam um problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# [!DNL MongoDB] Modelagem de dados

Quando [!DNL Adobe Commerce Intelligence] extrai [!DNL MongoDB] dados, esses dados são convertidos em um modelo relacional.

A má notícia: embora a maioria dos padrões de dados não represente um problema, há algumas que não são compatíveis com o [!DNL Commerce Intelligence], devido à tradução para um modelo relacional.

A boa notícia: Todos esses padrões podem ser evitados.

## Matrizes Subaninhadas {#subnested}

Se sua coleção for semelhante ao exemplo abaixo, [!DNL Commerce Intelligence] replica somente os dados na matriz de itens. Os dados da matriz de subitens não são extraídos.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Chaves de objeto variável {#varobjectkeys}

As coleções que incluem objetos com chaves de objeto variáveis não são replicadas no [!DNL Commerce Intelligence]. Por exemplo:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Isso geralmente ocorre onde um objeto está sendo usado e uma matriz seria mais apropriada. Agora, retrabalhe o exemplo acima:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
