---
title: Relatório de tempo médio para a primeira compra
description: Saiba como usar o Relatório de tempo médio para a primeira compra.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Relatório de tempo médio para a primeira compra

Muitos de nossos clientes têm uma métrica e um gráfico chamado `Average time to first purchase`, que mostra o tempo médio entre a data de registro de um grupo de usuários e a data da primeira compra. Os dados quase invariavelmente descem à medida que o tempo se aproxima do presente.

![tempo médio para o primeiro pedido](../../assets/average-time-to-first-order.png)

Isso ocorre porque esses clientes mais recentes ainda não tiveram a oportunidade de gerar quaisquer compras feitas mais de um mês após a data de adesão. Como os usuários que nunca fizeram uma compra não são incluídos (até que façam uma compra), isso distorce a média para baixo em grupos de clientes mais recentes.

Há outras maneiras possíveis de observar essa métrica que apresentam menos viés. Vamos explorar um exemplo.

## Exemplo: Executar um `cohort` análise das primeiras encomendas

Você pode ter um gráfico em `Users` painel nomeado `Time to first order cohort`. Esse relatório utiliza o `Distinct buyers` métrica, agrupa usuários por `cohort` semanas ou meses de registro e mostra a proporção (entre `0` e `1`) dos usuários que fizeram uma primeira compra nas semanas ou meses seguintes após o registro.

O gráfico pode mostrar que, para usuários que se registraram em dezembro de 2014, `0.56` ou `56%`) fez um primeiro pedido pelo mês 2 (por exemplo, janeiro de 2015).

Essa análise de coorte é um bom indicador da taxa de ativação do usuário ao longo do tempo. Se esse gráfico começar a se nivelar ou nivelar e você ainda não estiver perto de 100% de conversão para compradores, pode ser hora de ativar os usuários restantes por meio de campanhas de email.
