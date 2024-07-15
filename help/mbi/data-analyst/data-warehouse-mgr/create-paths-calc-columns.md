---
title: Criar ou excluir caminhos para colunas calculadas
description: Saiba como definir um caminho que descreva como a tabela em que você está criando uma coluna está relacionada à tabela da qual você está obtendo informações.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Criar ou Excluir Caminhos para Colunas Calculadas

## Atualizador das Colunas Calculadas

Ao [criar colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) na Data Warehouse, você deverá definir um caminho que descreva como a tabela na qual você está criando uma coluna está relacionada à tabela da qual você está obtendo informações. Para criar um caminho com êxito, você precisa saber duas coisas:

1. Como as tabelas em seus bancos de dados se relacionam
1. As chaves primária e estrangeira que definem esta relação

Se você souber essas informações, poderá criar facilmente um caminho seguindo as instruções neste tópico. Você pode pedir a um especialista técnico em sua organização ou entrar em contato com a [equipe de Serviços Profissionais](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Atualizadores de relacionamentos de tabela e tipos de chave {#refresher}

### Relacionamentos de tabela {#relationships}

Este conceito é abordado no [artigo sobre como entender e avaliar as relações da tabela](../../data-analyst/data-warehouse-mgr/table-relationships.md), mas um resumo rápido nunca prejudicou ninguém, certo?

As tabelas podem ser relacionadas entre si de uma das três formas a seguir:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | A relação entre pessoas e números de carteira de motorista. Uma pessoa pode ter apenas um número de carteira de motorista, e um número de carteira de motorista pertence a apenas uma pessoa. |
| **`one-to-many`** | A relação entre pedidos e itens - um pedido pode conter muitos itens, mas um item pertence a um único pedido. Nesse caso, a tabela pedidos é o lado um e a tabela itens é o lado muitos. |
| **`many-to-many`** | A relação entre produtos e categorias: um produto pode pertencer a muitas categorias e uma categoria pode conter muitos produtos. |

{style="table-layout:auto"}

Quando uma relação entre duas tabelas é entendida, ela pode ser usada para determinar qual caminho deve ser criado para trazer informações de uma tabela para outra. A próxima etapa requer o conhecimento das chaves primária e estrangeira que facilitam uma relação com a tabela.

### Chaves primárias e estrangeiras {#keys}

`Primary Key` é uma coluna ou conjunto de colunas inalterável que produz valores únicos em uma tabela. Por exemplo, quando um cliente faz um pedido em um site, uma nova linha é adicionada à tabela `orders` no carrinho de compras, com um novo `order_id`. Este `order_id` permite que o cliente e a empresa acompanhem o progresso desse pedido específico. Como a ID do pedido é exclusiva, geralmente é o `Primary Key` de uma tabela `orders`.

`Foreign Key` é uma coluna criada dentro de uma tabela que está vinculada à coluna `Primary Key` de outra tabela. As Chaves estrangeiras criam referências entre tabelas, permitindo que os analistas pesquisem e vinculem registros facilmente. Diga que você queria saber quais pedidos pertenciam a cada um de seus clientes. A coluna `customer id` (`Primary Key` da tabela `customers`) e a coluna `order_id` (`Foreign Key` na tabela `customers`, referenciando o `Primary Key` da tabela `orders`) permitem-nos vincular e analisar essas informações. Ao criar um caminho, você é solicitado a definir o `Primary Key` e o `Foreign Key`.

## Criação de um caminho {#createpath}

Ao criar uma coluna na Data Warehouse, você deve definir o caminho que traz informações de uma tabela para outra. Às vezes, os caminhos são preenchidos previamente porque existe um caminho entre as tabelas, mas se isso não acontecer, você deverá criar um.

Use a relação entre **clientes** e **pedidos** para mostrar como ela é feita. Detalhado:

* A relação é `one-to-many` - um cliente pode ter muitos pedidos, mas um pedido só pode ter um cliente. Isso informa a direção do relacionamento ou onde a coluna calculada deve ser criada. Nesse caso, significa que as informações da tabela `orders` podem ser trazidas para a tabela `customers`.
* O `primary key` que você deseja usar é `customers.customerid` ou a coluna `customer ID` na tabela `customers`.
* O `foreign key` que você deseja usar é `orders.customerid` ou a coluna `customer ID` na tabela `orders`.

Agora, você pode criar o caminho.

1. Clique em **[!UICONTROL Data > Data Warehouse]**.
1. Na lista da tabela, clique na tabela na qual deseja criar a coluna. Neste exemplo, é a tabela `customers`.
1. O esquema de tabela é exibido. Clique em **[!UICONTROL Create New Column]**.
1. Dê um nome à sua coluna, por exemplo, `Customer's orders`.
1. Selecione a definição da coluna. Confira o [Guia de Colunas Calculadas](../data-warehouse-mgr/creating-calculated-columns.md) para obter uma página de ajuda útil.
1. Na lista suspensa [!UICONTROL Select table and column], clique na opção **[!UICONTROL Create new path]**.

   ![Criando caminhos para o modal de colunas calculadas](../../assets/Creating_Paths_modal.png)

1. Usando os menus suspensos, selecione as chaves primária e estrangeira para cada tabela.

   No lado de `Many`, selecione `orders.customerid` - lembre-se, os clientes podem ter muitos pedidos.

   No lado de `One`, você seleciona `customers.customerid` - um pedido só pode ter um cliente.

1. Clique em **[!UICONTROL Save]** para salvar o caminho e concluir a criação da coluna.

### Limitações da criação de caminhos {#limits}

* **[!DNL Commerce Intelligence]não pode adivinhar relações de chave primária/estrangeira**. Você não deseja introduzir dados incorretos em sua conta, portanto, a criação de caminhos deve ser feita manualmente.

* **Atualmente, caminhos só podem ser especificados entre duas tabelas diferentes**. A lógica que você está tentando recriar envolve mais de duas tabelas? Pode fazer sentido (1) unir as colunas a uma tabela intermediária primeiro, depois à tabela de &quot;destino final&quot; ou (2) consultar a [equipe de Serviços Profissionais](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para encontrar a melhor abordagem para suas metas.

* **Uma coluna só pode ser a referência de chave estrangeira para UM caminho de cada vez**. Por exemplo, se `order_items.order_id` aponta para `orders.id`, então `order_items.order_id` não pode apontar para mais nada.

* **`Many-to-many`caminhos podem ser tecnicamente criados, mas geralmente produzem dados incorretos porque nenhum dos lados é uma verdadeira `one-to-many` chave estrangeira**. A melhor maneira de abordar esses caminhos sempre depende da análise específica desejada. Consulte a equipe de analistas do RJ para descobrir a melhor solução.

Se você for impedido de criar uma coluna calculada devido a uma ou mais limitações acima, entre em contato com o suporte com uma descrição da coluna em que você está

## Excluir um Caminho de Coluna Calculada {#delete}

Criou um caminho incorreto na Data Warehouse? Ou talvez você esteja fazendo uma pequena limpeza de primavera e queira arrumar? Se precisar excluir um caminho da sua conta, você pode [enviar um tíquete para os analistas de suporte do Adobe](../../guide-overview.md#Submitting-a-Support-Ticket). **Inclua o nome do caminho!**

## Encapsulamento {#wrapup}

Agora que você está familiarizado com a criação de caminhos para colunas calculadas na sua Data Warehouse. Se você ainda não tiver certeza sobre um caminho específico, lembre-se de que você sempre pode clicar em **[!UICONTROL Support]** na sua conta do [!DNL Commerce Intelligence] para obter assistência.

## Relacionados

* [Entendendo e avaliando relações de tabelas](../data-warehouse-mgr/table-relationships.md)
* [Criação de caminhos para colunas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos de Colunas Calculadas](../data-warehouse-mgr/calc-column-types.md) tentando criar.
