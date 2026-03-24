---
title: Tempo médio até a primeira compra do relatório
description: Saiba como usar o relatório Tempo médio até a primeira compra.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 0%

---

# Tempo médio até a primeira compra do relatório

Muitos clientes da Adobe têm uma métrica e um gráfico chamado `Average time to first purchase`, que mostra o tempo médio entre a data de registro de um grupo de usuários e a data da primeira compra. Os dados quase invariavelmente inclinam-se para baixo à medida que o tempo se aproxima do presente.

![tempo médio até a primeira solicitação](../../assets/average-time-to-first-order.png)

Isso ocorre porque esses clientes mais recentes ainda não tiveram a oportunidade de gerar compras que foram feitas por mais de um mês a partir da data de adesão. Uma vez que os usuários que nunca fizeram uma compra não são incluídos (até que façam uma compra), isso vicia a média para baixo para grupos mais recentes de clientes.

Há outras maneiras possíveis de observar essa métrica que introduzem menos viés. Explore um exemplo.

## Exemplo: executar uma análise `cohort` das primeiras ordens

Você pode ter um gráfico no painel `Users` chamado `Time to first order cohort`. Este relatório usa a métrica `Distinct buyers`, agrupa usuários por `cohort` semanas ou meses de registro e mostra a proporção (entre `0` e `1`) de usuários que fizeram uma primeira compra nas semanas ou meses seguintes após o registro.

O gráfico pode mostrar que, para usuários registrados em dezembro de 2014, `0.56` (ou `56%`) fez um primeiro pedido pelo mês 2 (por exemplo, janeiro de 2015).

Essa análise de coorte é um bom indicador da taxa de ativação do usuário ao longo do tempo. Se esse gráfico começar a nivelar ou estabilizar e você ainda não estiver perto da conversão de 100% em compradores, pode ser hora de ativar os usuários restantes por campanhas de email.
