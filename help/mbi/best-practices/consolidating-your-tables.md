---
title: Consolidar as tabelas
description: Saiba como consolidar tabelas e bancos de dados.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Consolidar as tabelas

Se você operar várias frentes de armazenamento ou em vários mercados, poderá ter bancos de dados semelhantes armazenados separadamente. Em [!DNL MBI], é fácil consolidar tabelas semelhantes de diferentes bancos de dados em conjunto.

Por exemplo, você pode ter uma `orders` tabela para `Market A`e um similar `orders` tabela para `Market B`. [!DNL MBI] pode consolidar ambas as tabelas e permitir que você veja os dados de pedidos agregados de ambos `Market A` e `B`, além de segmentá-lo por mercado específico.

Para que a consolidação de tabelas funcione, as tabelas de entrada devem ser **estruturadas de forma semelhante**. Em outras palavras, todas as tabelas de entrada devem conter as colunas de dados necessárias na tabela consolidada.

Este tópico discute alguns dos casos de uso mais comuns para tabelas consolidadas e as próximas etapas necessárias para criar suas próprias tabelas.

## Recommendations para quando usar tabelas consolidadas

O seguinte discute quando pode ser apropriado usar tabelas consolidadas em seu sistema.

### Integração de dados de vários sites

Se você vende seus produtos em diferentes marcas e sites, é provável que as tabelas de cada marca ou site estejam estruturadas de forma semelhante.

Por exemplo, você pode ter uma `orders` tabela para site `A` e um separado, mas similar, `orders` tabela para site `B`. Nessa situação, pode ser útil consolidar a `orders` tabelas do site `A` e `B` para que você possa ver a receita consolidada e o número de pedidos do site `A` e `B`, além de poder segmentar métricas por esses dois sites.

### Integração de dados herdados

Muitas empresas refateram seus bancos de dados de uma vez ou de outra, e os dados do banco de dados antigo nem sempre são convertidos para o novo sistema. Você pode usar tabelas consolidadas para unir as colunas principais das tabelas herdadas com as do sistema ativo. Isso permite que você faça uma análise unificada de seus dados ao longo do histórico.

### Combinação de eventos para análise ativa do usuário

Imagine um site em que os usuários possam fazer várias coisas: faça uma pesquisa, jogue um jogo, faça uma compra, consulte um amigo e assim por diante. Normalmente, cada um desses eventos será armazenado em sua própria tabela. Isso dificulta a análise de quantos usuários distintos tomaram pelo menos uma ação de qualquer tipo em um determinado período.

É possível utilizar tabelas consolidadas para criar uma lista unificada de todos os usuários e quando qualquer um desses eventos ocorreu. Em seguida, você pode executar queries na tabela consolidada para realizar facilmente essa análise.

Assim como em todas as outras tabelas no data warehouse, você pode adicionar colunas adicionais para potencializar diferentes tipos de gráficos e análises.

## Criando, Exibindo ou Atualizando uma Tabela Consolidada

Se estiver interessado em adicionar uma tabela consolidada ao data warehouse, entre em contato com [!DNL MBI] [suporte](../guide-overview.md).

>[!NOTE]
>
>Como as tabelas consolidadas não podem ser visualizadas na variável `Data Warehouse Manager`, visualizar e atualizar essas tabelas só pode ser feito por meio de [!DNL MBI] suporte.
