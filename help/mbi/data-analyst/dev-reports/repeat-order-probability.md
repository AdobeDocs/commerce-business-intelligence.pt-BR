---
title: Relatório de Probabilidade de Repetição de Pedido
description: Saiba e entenda o Relatório de Probabilidade de Ordem de Repetição.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 0%

---

# Relatório de Probabilidade de Repetição de Pedido

## Quando a perspectiva `Incremental Event Probability` estará disponível?

A perspectiva `incremental event probability` só está disponível quando os filtros usam dimensões iguais para todas as ordens (por exemplo, `gender` do usuário, `age` do usuário ou `source` do usuário).

Isso ocorre porque essa perspectiva depende de uma dimensão chamada `User's order number` para segmentação, que numera as compras de um usuário (por exemplo, 1º, 2º e 3º pedidos de John).

Se você adicionasse um filtro que usa uma dimensão que não é igual para todas as ordens (por exemplo, `Order's Region`), a dimensão `User's order number` não seria mais precisa. Isso ocorre porque ele não leva em conta regiões específicas ao numerar os pedidos de um usuário (por exemplo, o 1º, o 2º e o 3º pedidos de João ainda são os mesmos, independentemente da região).

## Transformando uma dimensão específica de pedido em uma dimensão específica do usuário

Em certos casos, você pode transformar uma dimensão `order-specific` em uma dimensão `user-specific` para adicionar como filtro no gráfico `Repeat Order Probability`. Nesses casos, você retorna o atributo da ordem da primeira ordem de um usuário ou da ordem mais recente (por exemplo, nome da região da primeira ordem do usuário).

Para criar uma nova dimensão, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Comparando a probabilidade de repetição de ordens com atributos diferentes

Para comparar o número de compras repetidas para atributos de pedidos diferentes (por exemplo, o do pedido `region`), a Adobe recomenda criar um gráfico semelhante a `Users by lifetime number of orders`. Isso mostra o número de usuários que fizeram 1, 2, 3,... número de pedidos por vida e adiciona o filtro de nível de pedido. (em outras palavras, isso pode mostrar se os usuários fazem compras mais ou menos repetidas em uma região ou outra.)

Os números que compõem esse gráfico podem ser exportados para Excel para calcular a taxa de probabilidade de ordem de repetição. Para ver a probabilidade de clientes que fizeram `(x)` pedidos para fazer `(x+1)` pedidos, basta` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Exemplo:

| Categoria | Valor |
|---|---|
| Número de clientes que fizeram uma compra em sua vida | `90` |
| Número de clientes que fizeram duas compras durante sua vida | `30` |
| Número de clientes que fizeram 3 compras durante sua vida | `10` |
| A probabilidade de ordem repetida de clientes que fizeram uma compra em sua vida para fazer uma segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
