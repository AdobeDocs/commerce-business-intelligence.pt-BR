---
title: Consolidar suas tabelas
description: Saiba como consolidar tabelas e bancos de dados.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Consolidar suas tabelas

Se você opera várias frentes de loja ou em vários mercados, você pode ter bancos de dados semelhantes armazenados separadamente. Entrada [!DNL Adobe Commerce Intelligence]No entanto, é fácil consolidar tabelas semelhantes de bancos de dados diferentes juntos.

Por exemplo, você pode ter um `orders` tabela para `Market A`, e um similar `orders` tabela para `Market B`. [!DNL Commerce Intelligence] pode consolidar ambas as tabelas e permitir que você veja os dados da ordem agregada de ambos `Market A` e `B`, além de segmentá-la por mercado específico.

Para que a consolidação das tabelas funcione, as tabelas de entrada devem ser **estruturado de forma semelhante**. Em outras palavras, todas as tabelas de entrada devem conter as colunas de dados necessárias na tabela consolidada.

Este tópico discute alguns dos casos de uso mais comuns para tabelas consolidadas e as próximas etapas necessárias para criar as suas próprias tabelas.

## Recommendations para Quando Usar Tabelas Consolidadas

O documento a seguir discute quando pode ser apropriado usar tabelas consolidadas em seu sistema.

### Integração de dados de vários sites

Se você vender seus produtos em diferentes marcas e sites, é provável que as tabelas de cada marca ou site sejam estruturadas de forma semelhante.

Por exemplo, você pode ter um `orders` tabela para site `A` e uma separada, mas semelhante, `orders` tabela para site `B`. Nesta situação, pode ser útil consolidar a `orders` tabelas do site `A` e `B`. Isso permite que você verifique a receita consolidada e o número de pedidos do site `A` e `B`, além de poder segmentar métricas por esses dois sites.

### Integração de dados herdados

Muitas empresas refatoraram seus bancos de dados de uma vez ou outra e os dados do banco de dados antigo nem sempre são convertidos para o novo sistema. Você pode usar tabelas consolidadas para unir as principais colunas das tabelas herdadas com as do sistema ativo. Isso permite realizar uma análise unificada dos dados ao longo do histórico.

### Combinando Eventos para Análise de Usuário Ativo

Imagine um site onde os usuários possam fazer várias coisas: fazer uma pesquisa, jogar, fazer uma compra, indicar um amigo e assim por diante. Normalmente, cada um desses eventos é armazenado em sua própria tabela. Isso dificulta a realização de uma análise de quantos usuários distintos executaram pelo menos uma ação de qualquer tipo em um determinado período de tempo.

Você pode usar tabelas consolidadas para criar uma lista unificada de todos os usuários e quando qualquer um desses eventos ocorreu. Em seguida, é possível executar consultas na tabela consolidada para realizar facilmente essa análise.

Como em todas as outras tabelas da Data Warehouse, é possível adicionar mais colunas para alimentar diferentes tipos de gráficos e análises.

## Criando, Exibindo ou Atualizando uma Tabela Consolidada

Se você estiver interessado em adicionar uma tabela consolidada à sua Data Warehouse, entre em contato com [!DNL Commerce Intelligence] [suporte](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Como as tabelas consolidadas não são visíveis na variável `Data Warehouse Manager`, a exibição e a atualização dessas tabelas só podem ser feitas por [!DNL Commerce Intelligence] suporte.
