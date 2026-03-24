---
title: Consolidar suas tabelas
description: Saiba como consolidar tabelas e bancos de dados.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
TQID: https://experienceleague.adobe.com/HC5REx483htdfFigZPxcrZeD5byyJKk-beQqnEARt1E
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---

# Consolidar suas tabelas

Se você opera várias frentes de loja ou em vários mercados, você pode ter bancos de dados semelhantes armazenados separadamente. No [!DNL Adobe Commerce Intelligence], é fácil consolidar tabelas semelhantes de bancos de dados diferentes.

Por exemplo, você pode ter uma tabela `orders` para `Market A` e uma tabela `orders` semelhante para `Market B`. O [!DNL Commerce Intelligence] pode consolidar ambas as tabelas e permitir que você veja os dados de ordem de agregação de `Market A` e `B`, além de segmentá-los por mercado específico.

Para que a consolidação de tabelas funcione, as tabelas de entrada devem ser **estruturadas de forma semelhante**. Em outras palavras, todas as tabelas de entrada devem conter as colunas de dados necessárias na tabela consolidada.

Este tópico discute alguns dos casos de uso mais comuns para tabelas consolidadas e as próximas etapas necessárias para criar as suas próprias tabelas.

## Recomendações para Quando Usar Tabelas Consolidadas

O documento a seguir discute quando pode ser apropriado usar tabelas consolidadas em seu sistema.

### Integração de dados de vários sites

Se você vender seus produtos em diferentes marcas e sites, é provável que as tabelas de cada marca ou site sejam estruturadas de forma semelhante.

Por exemplo, você pode ter uma tabela `orders` para o site `A` e uma tabela `orders` separada, mas semelhante, para o site `B`. Nessa situação, pode ser útil consolidar as tabelas `orders` do site `A` e `B`. Isso permite que você observe a receita consolidada e o número de pedidos dos sites `A` e `B`, além de poder segmentar as métricas por esses dois sites.

### Integração de dados herdados

Muitas empresas refatoraram seus bancos de dados de uma vez ou outra e os dados do banco de dados antigo nem sempre são convertidos para o novo sistema. Você pode usar tabelas consolidadas para unir as principais colunas das tabelas herdadas com as do sistema ativo. Isso permite realizar uma análise unificada dos dados ao longo do histórico.

### Combinando Eventos para Análise de Usuário Ativo

Imagine um site onde os usuários possam fazer várias coisas: fazer uma pesquisa, jogar, fazer uma compra, indicar um amigo e assim por diante. Normalmente, cada um desses eventos é armazenado em sua própria tabela. Isso dificulta a realização de uma análise de quantos usuários distintos executaram pelo menos uma ação de qualquer tipo em um determinado período de tempo.

Você pode usar tabelas consolidadas para criar uma lista unificada de todos os usuários e quando qualquer um desses eventos ocorreu. Em seguida, é possível executar consultas na tabela consolidada para realizar facilmente essa análise.

Como em todas as outras tabelas do Data Warehouse, é possível adicionar mais colunas para alimentar diferentes tipos de gráficos e análises.

## Criando, Exibindo ou Atualizando uma Tabela Consolidada

Se você estiver interessado em adicionar uma tabela consolidada à sua Data Warehouse, contate o [!DNL Commerce Intelligence] [suporte](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Como as tabelas consolidadas não são visíveis no `Data Warehouse Manager`, a exibição e a atualização dessas tabelas só pode ser feita pelo suporte [!DNL Commerce Intelligence].
