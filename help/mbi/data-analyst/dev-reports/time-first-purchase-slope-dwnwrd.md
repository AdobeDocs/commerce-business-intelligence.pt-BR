---
title: Tempo médio até a primeira compra do relatório
description: Saiba como usar o relatório Tempo médio até a primeira compra.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Tempo médio até a primeira compra do relatório

Muitos clientes do Adobe têm uma métrica e um gráfico chamados `Average time to first purchase`, que mostra o tempo médio entre a data de registro de um grupo de usuários e a data da primeira compra. Os dados quase invariavelmente inclinam-se para baixo à medida que o tempo se aproxima do presente.

![tempo médio para primeira solicitação](../../assets/average-time-to-first-order.png)

Isso ocorre porque esses clientes mais recentes ainda não tiveram a oportunidade de gerar compras que foram feitas por mais de um mês a partir da data de adesão. Uma vez que os usuários que nunca fizeram uma compra não são incluídos (até que façam uma compra), isso vicia a média para baixo para grupos mais recentes de clientes.

Há outras maneiras possíveis de observar essa métrica que introduzem menos viés. Explore um exemplo.

## Exemplo: executar um `cohort` análise de primeiras ordens

Você pode ter um gráfico em seu `Users` painel nomeado `Time to first order cohort`. Esse relatório utiliza o `Distinct buyers` métrica, agrupa usuários por `cohort` semanas ou meses de registro, e mostra o rácio (entre as duas `0` e `1`) de usuários que fizeram uma primeira compra nas semanas ou meses seguintes após o registro.

O gráfico pode mostrar que, para usuários registrados em dezembro de 2014, `0.56` (ou `56%`) fez um primeiro pedido até o mês 2 (por exemplo, janeiro de 2015).

Essa análise de coorte é um bom indicador da taxa de ativação do usuário ao longo do tempo. Se esse gráfico começar a nivelar ou estabilizar e você ainda não estiver perto da conversão de 100% em compradores, pode ser hora de ativar os usuários restantes por campanhas de email.
