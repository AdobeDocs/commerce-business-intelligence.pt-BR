---
title: Dimensões da compilação [!DNL Google ECommerce]
description: Aprenda a build dimensões que link seus dados de comércio eletrônico com seus pedidos e dados de clientes.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Dimensões da compilação [!DNL Google ECommerce]

>[!NOTE]
>
>Requer [ permissões ](../../administrator/user-management/user-management.md) de administrador.

Agora que você concluiu [ a conexão do [!DNL Google ECommerce] conta ](../../data-analyst/importing-data/integrations/google-ecommerce.md) , o que você pode fazer com esses dados [!DNL Commerce Intelligence] ? Este tópico aborda a criação de dimensões que vinculam os dados de comércio eletrônico aos seus pedidos e aos dados do cliente.

As dimensões cobertas oferecem a capacidade de criar análises que [responda a perguntas vitais sobre seus canais e campanhas de marketing](../../data-analyst/analysis/most-value-source-channel.md). Que porcentagem da receita vem de cada origem? Como funciona o valor vitalício de [!DNL Facebook] os clientes adquiridos se comparam aos de [!DNL Google]?

## Pré-requisitos e visão geral

Para criar as dimensões neste tópico, você precisa de uma [!DNL Google ECommerce] tabela, uma `orders` tabela e uma `customers` tabela. Essas tabelas devem ser [ sincronizadas com o data warehouse ](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes que as dimensões possam ser criadas.Tables sincronizadas são exibidas na `Synced Tables` seção do `Data Warehouse Manager` .

Esta é uma visão rápida da sincronização de tabelas e colunas se você precisar de uma atualização:

![](../../assets/Syncing_New_Columns.gif)

Após criar uma associação da `orders` tabela à [!DNL Google eCommerce] tabela, crie as três primeiras dimensões na lista abaixo. Próximo, você usa essas dimensões para criar três dimensões de usuário/cliente na `customers` tabela. Para concluir, você associa essas colunas à `orders` tabela.

Estas são as dimensões abordadas:

* **Tabela de pedidos**

* Origem do [!DNL Google Analytics] pedido
* Médio da [!DNL Google Analytics] ordem
* A campanha do [!DNL Google Analytics] pedido
* Fonte do [!DNL Google Analytics] primeiro solicitar do cliente
* Média do [!DNL Google Analytics] primeiro solicitar do cliente
* Campanha do [!DNL Google Analytics] primeiro solicitar do cliente

* **Tabela Clientes**

* do primeiro pedido do cliente [!DNL Google Analytics] origem
* do primeiro pedido do cliente [!DNL Google Analytics] médio
* do primeiro pedido do cliente [!DNL Google Analytics] campaign

## Criação de dimensões

Para criar dimensões, abra o [Gerenciador de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) clicando em **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabela de pedidos, rodada 1

Este exemplo cria a variável **do pedido [!DNL Google Analytics] Origem** dimensão.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `orders`) que contém as informações do pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecionar `Joined Column` do [lista suspensa definição](../data-warehouse-mgr/calc-column-types.md). Este exemplo funciona com um [relação um para um](../data-warehouse-mgr/table-relationships.md), correspondendo a `eCommerce.transactionID` para exatamente uma linha do `orders` tabela.
1. Em seguida, é necessário definir o caminho ou como a tabela e a coluna que estão sendo usadas são conectadas. Clique em `Select a table and column` lista suspensa.
1. O caminho necessário não está disponível, portanto, é necessário criar um novo. Clique em **[!UICONTROL Create new Path]**.
1. Na janela exibida, defina a variável `Many` lado a `orders.order\_id`ou a coluna no campo `orders` tabela que contém a ID do pedido.
1. No `One` lado, localize o `Google ECommerce` e defina a coluna como `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Clique em **[!UICONTROL Save]** para criar o caminho.
1. Depois que o caminho for adicionado, clique no link **[!UICONTROL Select table and column]** lista suspensa novamente.
1. Localize o `ECommerce` e, em seguida, clique na guia `Source` coluna. Isso vincula os pedidos às informações de origem.
1. Depois de voltar ao esquema de tabela, clique em **[!UICONTROL Save]** novamente para criar a dimensão.

Veja a seguir uma olhada em todo o processo:

![](../../assets/help_center.gif)

Próximo, tente criar **a mídia** do [!DNL Google Analytics] pedido e `campaign` . Não são muitas alterações para essas dimensões, portanto, experimente. Mas se você ficar preso, poderá verificar [ o final deste artigo ](#stuck) para ver o que é diferente.

### Tabela clientes {#customers}

Este exemplo cria o **dimensão de origem** do [!DNL Google Analytics] primeiro solicitar do cliente.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `customers`) que contém as informações do cliente.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Para este exemplo, selecione a variável `is MAX` definição do [lista suspensa definição](../../data-analyst/data-warehouse-mgr/calc-column-types.md). A variável `is MIN` a definição também pode funcionar se aplicada a uma coluna de texto com apenas um valor possível. A parte importante é garantir que os filtros adequados sejam definidos, o que você fará posteriormente.
1. Clique em **[!UICONTROL Select a table and column]** e selecione a `orders` , depois a variável `Order's [!DNL Google Analytics] source` coluna.
1. Clique em **[!UICONTROL Save]**.
1. Depois de voltar ao esquema de tabela, clique no link `Options` , depois `Filters`.
1. Clique em **[!UICONTROL Add Filter Set]** e, em seguida, selecione a `Orders we count` definido. Você deseja que apenas os pedidos incluídos no conjunto de filtros de pedidos contados sejam incluídos, portanto, é importante que esse conjunto de filtros seja selecionado.
1. Clique em **[!UICONTROL Add Filter]**. Você deseja encontrar o do primeiro pedido do cliente [!DNL Google Analytics] , portanto, é necessário adicionar um filtro:

   _Ordens. Número de solicitar do cliente = 1

   _
1. Clique **[!UICONTROL Save]** em para criar a dimensão.

Próximo, tente criar **a mídia** do primeiro solicitar do [!DNL Google Analytics] cliente e `campaign` . Não são muitas alterações para essas dimensões, portanto, experimente. Mas se você ficar preso, poderá verificar [ o final deste artigo ](#stuck) para ver o que é diferente.

### Bônus: tabela pedidos, redondo 2

Você pode parar aqui se desejar, mas esta seção permite uma análise mais detalhada trazendo a **do primeiro pedido do cliente [!DNL Google Analytics] dimensões** você criou na [última seção](#customers) no `orders` tabela. A criação de dimensões nesta seção permite analisar todas as métricas criadas no `orders` tabela - `Revenue`, `Number of orders`, `Distinct buyers`e assim por diante - usando o [!DNL Google Analytics] atributos da primeira ordem de um cliente.

Este exemplo une a `Customer's first order's [!DNL Google Analytics] source` dimensão à `orders` tabela.

1. No lista de tabelas no data warehouse, clique na tabela (neste caso, `orders` ) que contém suas informações de solicitar.
1. Clique em **[!UICONTROL Create a Column]** .
1. Nomeie a coluna.
1. Selecione `Joined Column` na lista suspensa definição. Isso une as dimensões do cliente criadas na seção anterior à `orders` tabela.
1. Clique na **[!UICONTROL Select a table and column]** lista suspensa e, em seguida, selecione a `customers` tabela e a `Customer's first order's [!DNL Google Analytics] source` coluna.
1. Se um caminho não preencher automaticamente, selecione o caminho que melhor conecta as tabelas clientes e pedidos.
1. Clique **[!UICONTROL Save]** em para criar a dimensão.

Veja a seguir uma olhada em todo o processo:

![](../../assets/help_center2.gif)

Conclua unindo o `Customer's first order's` meio e `campaign` as `orders` dimensões à tabela. Associar-se as dimensões e, se houver problemas, verifique [ o final do artigo ](#stuck) se precisar de ajuda.

### Resumindo

Você concluiu a criação das dimensões, o que significa que agora é possível criar análises poderosas que faixa o desempenho de vários canais e campanhas. Lembre-se de que as **novas colunas não estarão disponíveis até que a próxima atualização seja concluída** .

Algumas das dimensões mais populares são abordadas neste tópico, mas o céu é o limite-tente criar sua própria grátis para efetuar o ping nos EUA se quiser ajuda para explorar outras opções. 

### Observações adicionais

**`Orders`tabela #1**: ao criar o `Order's [!DNL Google Analytics]` médio e `campaign` dimensões, a diferença são as colunas selecionadas na etapa 12. Neste exemplo, a coluna foi `Source`.

**`Customers`tabela**: ao criar o `Customer's first order's [!DNL Google Analytics]` médio e `campaign` dimensões, a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna foi `Order's [!DNL Google Analytics]` origem.

**`Orders`tabela #2**: ao ingressar no `Customer's first order's [!DNL Google Analytics]` médio e `campaign` colunas para o `orders` , a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna foi `Customer's first order's [!DNL Google Analytics]` origem.
