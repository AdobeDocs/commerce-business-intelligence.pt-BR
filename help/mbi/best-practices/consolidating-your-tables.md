---
title: Consolidar suas tabelas
description: Saiba como consolidar tabelas e bancos de dados.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
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
