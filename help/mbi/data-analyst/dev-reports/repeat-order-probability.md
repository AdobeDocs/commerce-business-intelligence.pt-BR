---
title: Relatório de probabilidade da ordem repetida
description: Saiba e entenda o Relatório de probabilidade de repetição de pedido.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Relatório de probabilidade da ordem repetida

## Quando é a variável `Incremental Event Probability` perspectiva disponível?

O `incremental event probability` a perspectiva só está disponível quando filtros usam dimensões iguais para todos os pedidos (por exemplo, `gender`, do usuário `age` ou do usuário `source`)

Isso ocorre porque essa perspectiva depende de uma dimensão chamada `User's order number` para segmentação, que numera as compras de um usuário (por exemplo, 1º, 2º e 3º pedidos de John).

Se adicionarmos um filtro que usa uma dimensão que não é igual a todos os pedidos (por exemplo, `Order's Region`), `User's order number` não seria mais precisa, pois não conta para regiões específicas ao numerar os pedidos de um usuário (por exemplo, os primeiros, segundo e terceiro pedidos de John ainda são os mesmos, independentemente de sua região).

## Transformar uma dimensão específica do pedido em uma dimensão específica do usuário

Em certos casos, podemos ser capazes de transformar uma `order-specific` em uma `user-specific` dimensão para adicionar como filtro na `Repeat Order Probability` gráfico. Nesses casos, retornaremos o atributo de pedido do primeiro pedido de um usuário ou do pedido mais recente (por exemplo, o nome da região do primeiro pedido do usuário).

Se quiser criar essa nova dimensão, [entrar em contato com o suporte](../../guide-overview.md).

## Comparação da probabilidade de repetição de pedidos com atributos diferentes

Para comparar o número de compras repetidas de diferentes atributos da ordem (por exemplo, `region`), recomendamos criar um gráfico semelhante a `Users by lifetime number of orders` que mostra o número de usuários que fizeram 1, 2, 3,... número de pedidos por vida e adicionou o filtro de nível de pedido. (em outras palavras, isso pode mostrar se os usuários fazem mais ou menos compras repetidas em uma região ou outra.)

Os números que compõem esse gráfico podem então ser exportados para o excel para calcular a taxa de probabilidade de ordem repetida. Para ver a probabilidade dos clientes que fizeram o `(x)` ordens para `(x+1)` pedidos, simplesmente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Exemplo:

|  |  |
|---|---|
| Número de clientes que efetuaram uma compra durante toda a vida | `90` |
| Número de clientes que efetuaram duas compras durante sua vida | `30` |
| Número de clientes que efetuaram três compras durante sua vida | `10` |
| A probabilidade de ordem repetida de clientes que fizeram uma compra em sua vida para fazer uma segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
