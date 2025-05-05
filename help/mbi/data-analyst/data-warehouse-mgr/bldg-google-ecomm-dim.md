---
title: Compilar [!DNL Google ECommerce] dimensões
description: Saiba como criar dimensões que vinculam seus dados de comércio eletrônico aos seus pedidos e dados de clientes.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Compilar [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Requer [permissões de administrador](../../administrator/user-management/user-management.md).

Agora que você terminou de [conectar sua[!DNL Google ECommerce] conta](../../data-analyst/importing-data/integrations/google-ecommerce.md), o que você pode fazer com esses dados em [!DNL Commerce Intelligence]? Este tópico aborda a criação de dimensões que vinculam os dados de comércio eletrônico aos seus pedidos e aos dados do cliente.

As dimensões cobertas oferecem a capacidade de criar análises que [respondem a perguntas vitais sobre seus canais e campanhas de marketing](../../data-analyst/analysis/most-value-source-channel.md). Que porcentagem da receita vem de cada origem? Como o valor vitalício de [!DNL Facebook] clientes adquiridos se compara aos de [!DNL Google]?

## Pré-requisitos e visão geral

Para criar as dimensões neste tópico, você precisa de uma tabela [!DNL Google ECommerce], uma tabela `orders` e uma tabela `customers`. Essas tabelas devem ser [sincronizadas com a Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes que as dimensões possam ser compiladas. As tabelas sincronizadas são exibidas na seção `Synced Tables` de `Data Warehouse Manager`.

Veja a seguir como sincronizar tabelas e colunas se precisar de uma atualização:

![](../../assets/Syncing_New_Columns.gif)

Depois de criar uma ligação da tabela `orders` para a tabela [!DNL Google eCommerce], você cria as três primeiras dimensões na lista abaixo. Em seguida, use essas dimensões para criar três dimensões de usuário/cliente na tabela `customers`. Para finalizar, você associa essas colunas à tabela `orders`.

Estas são as dimensões cobertas:

* **Tabela de pedidos**

* Origem do pedido [!DNL Google Analytics]
* Mídia [!DNL Google Analytics] do pedido
* [!DNL Google Analytics]Uma campanha do pedido
* Origem de [!DNL Google Analytics] do primeiro pedido do cliente
* Meio [!DNL Google Analytics] do primeiro pedido do cliente
* Campanha [!DNL Google Analytics] de primeiro pedido do cliente

* **Tabela de clientes**

* Origem de [!DNL Google Analytics] do primeiro pedido do cliente
* Meio [!DNL Google Analytics] do primeiro pedido do cliente
* Campanha [!DNL Google Analytics] de primeiro pedido do cliente

## Criação de dimensões

Para criar dimensões, abra o [Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) clicando em **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabela de pedidos, rodada 1

Este exemplo cria a dimensão Source **[!DNL Google Analytics] do pedido**.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `orders`) que contém suas informações de pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecione `Joined Column` na [lista suspensa de definições](../data-warehouse-mgr/calc-column-types.md). Este exemplo funciona com uma [relação um para um](../data-warehouse-mgr/table-relationships.md), correspondendo a coluna `eCommerce.transactionID` a exatamente uma linha da tabela `orders`.
1. Em seguida, é necessário definir o caminho ou como a tabela e a coluna que estão sendo usadas são conectadas. Clique na lista suspensa `Select a table and column`.
1. O caminho necessário não está disponível, portanto, é necessário criar um novo. Clique em **[!UICONTROL Create new Path]**.
1. Na janela exibida, defina o lado de `Many` como `orders.order\_id` ou a coluna na tabela `orders` que contém a ID do pedido.
1. No lado de `One`, localize a tabela `Google ECommerce` e defina a coluna como `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Clique em **[!UICONTROL Save]** para criar o caminho.
1. Após adicionar o caminho, clique na lista suspensa **[!UICONTROL Select table and column]** novamente.
1. Localize a tabela `ECommerce` e clique na coluna `Source`. Isso vincula os pedidos às informações de origem.
1. Depois de voltar ao esquema da tabela, clique em **[!UICONTROL Save]** novamente para criar a dimensão.

Veja aqui todo o processo:

![](../../assets/help_center.gif)

Em seguida, tente criar a **mídia [!DNL Google Analytics] do pedido** e `campaign`. Não há muitas alterações nessas dimensões, então tente. Mas se ficar preso, você pode conferir [o final deste artigo](#stuck) para ver o que é diferente.

### Tabela Clientes {#customers}

Este exemplo cria a dimensão [!DNL Google Analytics] de origem **do** Cliente da primeira ordem.

1. Na lista de tabelas da Data Warehouse, clique na tabela (neste caso, `customers`) que contém suas informações de cliente.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Para este exemplo, selecione a definição `is MAX` na lista suspensa [definição](../../data-analyst/data-warehouse-mgr/calc-column-types.md). A definição `is MIN` também pode funcionar se aplicada a uma coluna de texto com apenas um valor possível. A parte importante é garantir que os filtros adequados sejam definidos, o que você fará posteriormente.
1. Clique na lista suspensa **[!UICONTROL Select a table and column]**, selecione a tabela `orders` e, em seguida, a coluna `Order's [!DNL Google Analytics] source`.
1. Clique em **[!UICONTROL Save]**.
1. Depois de voltar ao esquema da tabela, clique na lista suspensa `Options` e, em seguida, `Filters`.
1. Clique em **[!UICONTROL Add Filter Set]** e selecione o conjunto `Orders we count`. Você deseja que apenas os pedidos incluídos no conjunto de filtros de pedidos contados sejam incluídos, portanto, é importante que esse conjunto de filtros seja selecionado.
1. Clique em **[!UICONTROL Add Filter]**. Você deseja encontrar a origem [!DNL Google Analytics] do primeiro pedido do cliente, então é necessário adicionar um filtro:

   _orders.Número da ordem do cliente = 1

   _
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Em seguida, tente criar a **mídia [!DNL Google Analytics] do primeiro pedido do cliente** e `campaign`. Não há muitas alterações nessas dimensões, então tente. Mas se ficar preso, você pode conferir [o final deste artigo](#stuck) para ver o que é diferente.

### Bônus: Tabela de pedidos, rodada 2

Você pode parar aqui se desejar, mas esta seção habilita análises adicionais trazendo as [!DNL Google Analytics] dimensões **da** primeira ordem do Cliente[que você criou na &lbrace;última seção](#customers) para a tabela `orders`. A criação de dimensões nesta seção permite analisar todas as métricas criadas na tabela `orders` - `Revenue`, `Number of orders`, `Distinct buyers` e assim por diante - usando os [!DNL Google Analytics] atributos da primeira ordem de um cliente.

Este exemplo une a dimensão `Customer's first order's [!DNL Google Analytics] source` à tabela `orders`.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `orders`) que contém suas informações de pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecione `Joined Column` na lista suspensa de definição. Isso une as dimensões de clientes criadas na seção anterior à tabela `orders`.
1. Clique na lista suspensa **[!UICONTROL Select a table and column]** e selecione a tabela `customers` e a coluna `Customer's first order's [!DNL Google Analytics] source`.
1. Se um caminho não for preenchido automaticamente, selecione o caminho que melhor conecta as tabelas de clientes e pedidos.
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Veja aqui todo o processo:

![](../../assets/help_center2.gif)

Conclua unindo a mídia `Customer's first order's` e as dimensões `campaign` à tabela `orders`. Associe-se às dimensões e, se houver problemas, confira [o fim do artigo](#stuck) se precisar de ajuda.

### Encapsulamento

Você terminou de criar as dimensões, o que significa que agora é possível criar análises poderosas que rastreiam o desempenho de seus vários canais e campanhas. Lembre-se de que as **novas colunas não estarão disponíveis até que a próxima atualização seja concluída**.

Algumas das dimensões mais populares são abordadas neste tópico, mas o céu é o limite - tente criar o seu próprio ou sinta-se à vontade para nos enviar um ping se quiser ajuda para explorar outras opções. 

### Observações adicionais

**`Orders`tabela #1**: ao criar a mídia `Order's [!DNL Google Analytics]` e as dimensões `campaign`, a diferença são as colunas selecionadas na etapa 12. Neste exemplo, a coluna era `Source`.

**`Customers`tabela**: ao criar as dimensões `Customer's first order's [!DNL Google Analytics]` média e `campaign`, a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna era de `Order's [!DNL Google Analytics]` origem.

**`Orders`tabela #2**: ao unir a mídia `Customer's first order's [!DNL Google Analytics]` e as colunas `campaign` à tabela `orders`, a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna era de `Customer's first order's [!DNL Google Analytics]` origem.
