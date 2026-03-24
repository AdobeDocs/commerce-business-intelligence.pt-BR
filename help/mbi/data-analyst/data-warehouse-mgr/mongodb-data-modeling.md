---
title: Modelagem de dados do MongoDB
description: Saiba como evitar padrões de dados que representam um problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/L9xlGE4hAQssTHJzzxQD9EGUVaIZFY-2-ALOLM9vym4
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
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 129
ht-degree: 1%

---

# Modelagem de dados [!DNL MongoDB]

Quando [!DNL Adobe Commerce Intelligence] extrai dados [!DNL MongoDB], esses dados são convertidos em um modelo relacional.

A má notícia: embora a maioria dos padrões de dados não represente um problema, há alguns que não têm suporte no [!DNL Commerce Intelligence], devido à conversão em um modelo relacional.

A boa notícia: Todos esses padrões podem ser evitados.

## Matrizes Subaninhadas {#subnested}

Se sua coleção se parece com o exemplo abaixo, o [!DNL Commerce Intelligence] replica somente os dados na matriz de itens. Os dados da matriz de subitens não são extraídos.

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

As coleções que incluem objetos com chaves de objeto variável não são replicadas em [!DNL Commerce Intelligence]. Por exemplo:

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
