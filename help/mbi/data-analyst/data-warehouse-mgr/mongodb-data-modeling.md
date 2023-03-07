---
title: Modelagem de dados do MongoDB
description: Saiba como evitar padrões de dados que representam um problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] Modelagem de dados

Quando [!DNL MBI] extrai [!DNL MongoDB] dados, esses dados são convertidos em um modelo relacional.

A má notícia: embora a maioria dos padrões de dados não represente um problema, há alguns que, devido à tradução para um modelo relacional, [!DNL MBI] não oferece suporte a.

A boa notícia: Todos esses padrões podem ser evitados.

## Matrizes Subaninhadas {#subnested}

Se sua coleção for semelhante ao exemplo abaixo, [!DNL MBI] replica somente os dados na matriz de itens. Os dados da matriz de subitens não são extraídos.

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

As coleções que incluem objetos com chaves de objeto variáveis não são replicadas no [!DNL MBI]. Por exemplo:

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
