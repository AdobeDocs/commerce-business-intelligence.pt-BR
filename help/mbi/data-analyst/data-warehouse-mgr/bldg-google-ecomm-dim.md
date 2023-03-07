---
title: Build[!DNL Google ECommerce]dimensões
description: Saiba como criar dimensões que vinculam seus dados de comércio eletrônico aos seus pedidos e dados de clientes.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Build [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

Agora que você terminou [conectar seu[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), o que você pode fazer com esses dados no [!DNL MBI]? Este artigo orienta você na criação de dimensões que vinculam os dados de comércio eletrônico aos seus pedidos e dados do cliente.

As dimensões cobertas oferecem a capacidade de criar análises que [responda a perguntas vitais sobre seus canais e campanhas de marketing](../../data-analyst/analysis/most-value-source-channel.md). Que porcentagem da receita vem de cada origem? Como o valor vitalício dos clientes adquiridos da Facebook se compara ao dos de [!DNL Google]?

## Pré-requisitos e visão geral

Para criar as dimensões neste artigo, você precisa de uma [!DNL Google ECommerce] tabela, um `orders` tabela e um `customers` tabela. Essas tabelas devem ser [sincronizado com a sua Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes que as dimensões possam ser criadas. As tabelas sincronizadas são exibidas na variável `Synced Tables` seção do `Data Warehouse Manager`.

Veja a seguir como sincronizar tabelas e colunas se precisar de uma atualização:

![](../../assets/Syncing_New_Columns.gif)

Depois de criar uma associação a partir do `orders` tabela para a [!DNL Google eCommerce] crie as três primeiras dimensões na lista abaixo. Em seguida, use essas dimensões para criar três dimensões de usuário/cliente no `customers` tabela. Para finalizar, você associa essas colunas à `orders` tabela.

Estas são as dimensões cobertas:

* **Tabela Pedidos**

* do pedido [!DNL Google Analytics] origem
* do pedido [!DNL Google Analytics] médio
* do pedido [!DNL Google Analytics]Uma campanha
* do primeiro pedido do cliente [!DNL Google Analytics] origem
* do primeiro pedido do cliente [!DNL Google Analytics] médio
* do primeiro pedido do cliente [!DNL Google Analytics] campaign

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

Veja aqui todo o processo:

![](../../assets/help_center.gif)

Em seguida, tente criar **do pedido [!DNL Google Analytics] médio** e `campaign`. Não há muitas alterações nessas dimensões, então tente. Mas se você ficar preso, você pode verificar [no fim deste artigo](#stuck) para ver o que é diferente.

### Tabela Clientes {#customers}

Este exemplo cria a variável **do primeiro pedido do cliente [!DNL Google Analytics] origem** dimensão.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `customers`) que contém as informações do cliente.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Para este exemplo, selecione a variável `is MAX` definição do [lista suspensa definição](../../data-analyst/data-warehouse-mgr/calc-column-types.md). A variável `is MIN` a definição também pode funcionar se aplicada a uma coluna de texto com apenas um valor possível. A parte importante é garantir que os filtros adequados sejam definidos, o que você fará posteriormente.
1. Clique em **[!UICONTROL Select a table and column]** e selecione a `orders` , depois a variável `Order's [!DNL Google Analytics] source` coluna.
1. Clique em **[!UICONTROL Save]**.
1. Depois de voltar ao esquema de tabela, clique no link `Options` , depois `Filters`.
1. Clique em **[!UICONTROL Add Filter Set]** e, em seguida, selecione a `Orders we count` definido. Você deseja que apenas os pedidos incluídos no conjunto de filtros de pedidos contados sejam incluídos, portanto, é importante que esse conjunto de filtros seja selecionado.
1. Clique em **[!UICONTROL Add Filter]**. Você deseja encontrar o do primeiro pedido do cliente [!DNL Google Analytics] , portanto, é necessário adicionar um filtro:

   _orders.Número da ordem do cliente = 1

   _
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Em seguida, tente criar **do primeiro pedido do cliente [!DNL Google Analytics] médio** e `campaign`. Não há muitas alterações nessas dimensões, então tente. Mas se você ficar preso, você pode verificar [no fim deste artigo](#stuck) para ver o que é diferente.

### Bônus: Tabela de pedidos, rodada 2

Você pode parar aqui se desejar, mas esta seção permite uma análise mais detalhada trazendo a **do primeiro pedido do cliente [!DNL Google Analytics] dimensões** você criou na [última seção](#customers) no `orders` tabela. A criação de dimensões nesta seção permite analisar todas as métricas criadas no `orders` tabela - `Revenue`, `Number of orders`, `Distinct buyers`e assim por diante - usando o [!DNL Google Analytics] atributos da primeira ordem de um cliente.

Este exemplo une o `Customer's first order's [!DNL Google Analytics] source` dimensão ao `orders` tabela.

1. Na lista de tabelas na Data Warehouse, clique na tabela (neste caso, `orders`) que contém as informações do pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecionar `Joined Column` na lista suspensa de definição. Isso unirá as dimensões de clientes criadas na seção anterior à `orders` tabela.
1. Clique em **[!UICONTROL Select a table and column]** e selecione a `customers` tabela e o `Customer's first order's [!DNL Google Analytics] source` coluna.
1. Se um caminho não for preenchido automaticamente, selecione o caminho que melhor conecta as tabelas de clientes e pedidos.
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Veja aqui todo o processo:

![](../../assets/help_center2.gif)

Conclua ingressando no `Customer's first order's` médio e `campaign` dimensões para o `orders` tabela. Una as dimensões e, se houver problemas, confira [no fim do artigo](#stuck) se precisar de ajuda.

### Encapsulamento

Você terminou de criar as dimensões, o que significa que agora é possível criar análises poderosas que rastreiam o desempenho de seus vários canais e campanhas. Lembre-se de que a variável **novas colunas não estarão disponíveis até que a próxima atualização seja concluída**.

Algumas das dimensões mais populares são abordadas neste artigo, mas o céu é o limite - tente criar o seu próprio ou sinta-se livre para nos enviar um ping se quiser ajuda com a exploração de outras opções. 

### Estou preso! O que é diferente? {#stuck}

**`Orders`tabela #1:** Ao criar a variável `Order's [!DNL Google Analytics]` médio e `campaign` dimensões, a diferença são as colunas selecionadas na etapa 12. Neste exemplo, a coluna foi `Source`.

**`Customers`tabela:** Ao criar a variável `Customer's first order's [!DNL Google Analytics]` médio e `campaign` dimensões, a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna foi `Order's [!DNL Google Analytics]` origem.

**`Orders`tabela #2:** Ao ingressar no `Customer's first order's [!DNL Google Analytics]` médio e `campaign` colunas para o `orders` , a diferença são as colunas selecionadas na etapa 5. Neste exemplo, a coluna foi `Customer's first order's [!DNL Google Analytics]` origem.
