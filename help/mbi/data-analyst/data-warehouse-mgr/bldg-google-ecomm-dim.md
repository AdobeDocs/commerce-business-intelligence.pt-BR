---
title: Criar[!DNL Google ECommerce]dimensões
description: Saiba como criar dimensões que vincularão seus dados de comércio eletrônico aos seus pedidos e dados do cliente.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Criar [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

Agora que você terminou [conectar seu[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), o que você pode fazer com esses dados em [!DNL MBI]? Neste artigo, abordamos a criação de dimensões que vincularão seus dados de comércio eletrônico aos seus pedidos e dados de clientes.

As dimensões que abordamos lhe darão a capacidade de criar análises que [responda perguntas vitais sobre seus canais e campanhas de marketing](../../data-analyst/analysis/most-value-source-channel.md). Que porcentagem da receita vem de cada fonte? Como o valor vitalício dos clientes adquiridos pela Facebook se compara ao valor dos clientes adquiridos pela [!DNL Google]?

## Pré-requisitos e visão geral

Para criar as dimensões neste artigo, você precisa de um [!DNL Google ECommerce] tabela, um `orders` tabela e uma `customers` tabela. Essas tabelas têm de ser [sincronizado com seu data warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes que as dimensões possam ser criadas. As tabelas sincronizadas são exibidas na `Synced Tables` da seção `Data Warehouse Manager`.

Veja a seguir uma visão rápida da sincronização de tabelas e colunas se você precisar de um atualizador:

![](../../assets/Syncing_New_Columns.gif)

Depois de criar uma associação do `orders` à tabela [!DNL Google eCommerce] , criamos as três primeiras dimensões na lista abaixo. Em seguida, usamos essas dimensões para criar três dimensões de usuário/cliente na `customers` tabela. Para finalizar, unimos essas colunas ao `orders` tabela.

Estas são as dimensões que abordamos:

* **Tabela de pedidos**

* Order&#39;s [!DNL Google Analytics] source
* Order&#39;s [!DNL Google Analytics] medium
* Order&#39;s [!DNL Google Analytics]Uma campanha
* O primeiro pedido do cliente [!DNL Google Analytics] source
* O primeiro pedido do cliente [!DNL Google Analytics] medium
* O primeiro pedido do cliente [!DNL Google Analytics] campanha

* **Tabela de clientes**

* O primeiro pedido do cliente [!DNL Google Analytics] source
* O primeiro pedido do cliente [!DNL Google Analytics] medium
* O primeiro pedido do cliente [!DNL Google Analytics] campanha

## Criação das dimensões

Para criar dimensões, abra o [Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) clicando em **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabela de pedidos, rodada 1

Neste exemplo, criamos a variável **Order&#39;s [!DNL Google Analytics] Origem** dimensão.

1. Na lista de tabelas da Data Warehouse, clique na tabela (no nosso caso, `orders`) que contém as informações do pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecionar `Joined Column` do [lista suspensa definição](../data-warehouse-mgr/calc-column-types.md). Neste exemplo, estamos trabalhando com um [relação um para um](../data-warehouse-mgr/table-relationships.md), correspondendo ao `eCommerce.transactionID` para exatamente uma linha do `orders` tabela.
1. Em seguida, precisamos definir o caminho ou como a tabela e a coluna que está sendo usada estão conectadas. Clique no botão `Select a table and column` lista suspensa.
1. O caminho de que precisamos não está disponível, portanto precisamos criar um novo. Clique em **[!UICONTROL Create new Path]**.
1. Na janela exibida, defina a variável `Many` lado a lado `orders.order\_id`ou a coluna na `orders` tabela que contém a ID do pedido.
1. No `One` lado, encontre a `Google ECommerce` em seguida, defina a coluna como `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Clique em **[!UICONTROL Save]** para criar o caminho.
1. Após adicionar o caminho, clique no botão **[!UICONTROL Select table and column]** novamente.
1. Localize a variável `ECommerce` e clique no botão `Source` coluna. Isso vincula os pedidos às informações de origem.
1. Depois de voltar ao schema da tabela, clique em **[!UICONTROL Save]** novamente para criar a dimensão.

Veja o processo inteiro:

![](../../assets/help_center.gif)

Em seguida, tente criar **Order&#39;s [!DNL Google Analytics] medium** e `campaign`. Pouco vai mudar para essas dimensões, então tente. Mas se você ficar preso, você pode verificar [o fim deste artigo](#stuck) para ver o que é diferente.

### Tabela de clientes {#customers}

Neste exemplo, criamos a variável **O primeiro pedido do cliente [!DNL Google Analytics] source** dimensão.

1. Na lista de tabelas da Data Warehouse, clique na tabela (no nosso caso, `customers`) que contém as informações do cliente.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Neste exemplo, selecionamos a variável `is MAX` da [lista suspensa definição](../../data-analyst/data-warehouse-mgr/calc-column-types.md). O `is MIN` A definição também poderia funcionar se aplicada a uma coluna de texto com apenas um valor possível. A parte importante é garantir a definição de filtros adequados, o que fazemos mais tarde.
1. Clique no botão **[!UICONTROL Select a table and column]** e selecione o `orders` , em seguida, a `Order's [!DNL Google Analytics] source` coluna.
1. Clique em **[!UICONTROL Save]**.
1. Depois de voltar ao schema da tabela, clique no link `Options` lista suspensa, em seguida `Filters`.
1. Clique em **[!UICONTROL Add Filter Set]** e selecione o `Orders we count` definido. Queremos que apenas os pedidos incluídos no filtro de contagem de pedidos sejam incluídos, portanto, é importante que esse conjunto de filtros seja selecionado.
1. Clique em **[!UICONTROL Add Filter]**. Queremos encontrar o primeiro pedido do cliente [!DNL Google Analytics] fonte, portanto, precisamos adicionar um filtro:

   _orders.Número do pedido do cliente = 1

   _
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Em seguida, tente criar **O primeiro pedido do cliente [!DNL Google Analytics] medium** e `campaign`. Pouco vai mudar para essas dimensões, então tente. Mas se você ficar preso, você pode verificar [o fim deste artigo](#stuck) para ver o que é diferente.

### Bônus: Tabela de pedidos, rodada 2

Você pode parar aqui se desejar, mas esta seção permite análises adicionais trazendo a variável **O primeiro pedido do cliente [!DNL Google Analytics] dimensões** criamos no [última seção](#customers) na `orders` tabela. A criação das dimensões nesta seção permite analisar todas as métricas baseadas em `orders` tabela - `Revenue`, `Number of orders`, `Distinct buyers`, e assim por diante - usando o [!DNL Google Analytics] atributos do primeiro pedido de um cliente.

Neste exemplo, participamos do `Customer's first order's [!DNL Google Analytics] source` à dimensão `orders` tabela.

1. Na lista de tabelas da Data Warehouse, clique na tabela (no nosso caso, `orders`) que contém as informações do pedido.
1. Clique em **[!UICONTROL Create a Column]**.
1. Nomeie a coluna.
1. Selecionar `Joined Column` na lista suspensa definição. Isso unirá as dimensões do cliente criadas na seção anterior à `orders` tabela.
1. Clique no botão **[!UICONTROL Select a table and column]** , em seguida, selecione o `customers` e a `Customer's first order's [!DNL Google Analytics] source` coluna.
1. Se um caminho não for preenchido automaticamente, selecione o caminho que melhor conecta as tabelas de clientes e pedidos.
1. Clique em **[!UICONTROL Save]** para criar a dimensão.

Veja o processo inteiro:

![](../../assets/help_center2.gif)

Termine unindo o `Customer's first order's` médio e médio `campaign` à `orders` tabela. Faça uma tentativa e, como já mencionamos, confira [o fim do artigo](#stuck) se precisar de ajuda.

### Quebra de linha

Concluímos a criação das dimensões, o que significa que agora podemos criar análises poderosas que rastreiam o desempenho de nossos vários canais e campanhas. Sabemos que você está ansioso para começar, mas lembre-se do **novas colunas não estarão disponíveis até que a próxima atualização seja concluída**.

Abordamos algumas das dimensões mais populares neste artigo, mas o céu é o limite - tente criar as suas próprias dimensões ou sinta-se à vontade para nos tocar se quiser ajudar a explorar outras opções. 

### Estou preso! o que é diferente? {#stuck}

**`Orders`tabela nº 1:** Ao criar o `Order's [!DNL Google Analytics]` médio e médio `campaign` , a diferença será as colunas selecionadas na etapa 12. No nosso exemplo, a coluna era `Source`.

**`Customers`tabela:** Ao criar o `Customer's first order's [!DNL Google Analytics]` médio e médio `campaign` , a diferença será as colunas selecionadas na etapa 5. No nosso exemplo, a coluna era `Order's [!DNL Google Analytics]` fonte.

**`Orders`tabela nº 2:** Ao entrar na `Customer's first order's [!DNL Google Analytics]` médio e médio `campaign` para `orders` tabela, a diferença será as colunas selecionadas na etapa 5. No nosso exemplo, a coluna era `Customer's first order's [!DNL Google Analytics]` fonte.
