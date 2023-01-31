---
title: Modelagem de dados do MongoDB
description: Saiba como evitar padrões de dados que colocam um problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# [!DNL MongoDB] Modelagem de dados

When [!DNL MBI] puxa [!DNL MongoDB] , esses dados são traduzidos em um modelo relacional.

As más notícias: Embora a maioria dos padrões de dados não constitua um problema, há alguns, devido à tradução para um modelo relacional, [!DNL MBI] não suporta.

A boa notícia: Todos esses padrões podem ser evitados.

## Matrizes subaninhadas {#subnested}

Se sua coleção se parece com o exemplo abaixo, [!DNL MBI] só replicará os dados na matriz de itens. Os dados da matriz de subitens não serão transferidos.

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

## Chaves de objeto de variável {#varobjectkeys}

Coleções que incluem objetos com chaves de objeto variáveis não são replicadas em [!DNL MBI]. Por exemplo:

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

Isso geralmente ocorre onde um objeto está sendo usado e uma matriz seria mais apropriada. Agora, retrabalharemos o exemplo acima:

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
