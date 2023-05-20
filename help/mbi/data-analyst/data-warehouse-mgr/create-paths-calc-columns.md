---
title: Criar ou excluir caminhos para colunas calculadas
description: Saiba como definir um caminho que descreva como a tabela em que você está criando uma coluna está relacionada à tabela da qual você está obtendo informações.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Criar ou Excluir Caminhos para Colunas Calculadas

## Atualização de colunas calculadas

Ao [ criar colunas ](../data-warehouse-mgr/creating-calculated-columns.md) calculadas no data warehouse, você será solicitado a definir um caminho que descreve como a tabela em que você está criando uma coluna está relacionada à tabela da qual você está obtendo informações. Para criar um caminho com êxito, você precisa conhecer duas coisas:

1. Como as tabelas nos bancos de dados se relacionam entre si
1. As chaves primária e externa que definem esse relacionamento

Se você souber essas informações, poderá criar facilmente um caminho seguindo as instruções neste tópico. Você pode solicitar um especialista técnico em sua organização ou entrar em contato com o [ Serviços profissionais equipe ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) .

## Renovações em relações de tabela e tipos de chave {#refresher}

### Relações de tabela {#relationships}

Esse conceito é abordado no artigo ](../../data-analyst/data-warehouse-mgr/table-relationships.md) sobre a [ compreensão e avaliação de relações de tabela, mas um resumo rápido nunca prejudica ninguém, certo?

As tabelas podem ser relacionadas entre si de uma das três formas a seguir:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | A relação entre pessoas e números de carteira de motorista. Uma pessoa pode ter apenas um número de carteira de motorista, e um número de carteira de motorista pertence a apenas uma pessoa. |
| **`one-to-many`** | A relação entre pedidos e itens - um pedido pode conter muitos itens, mas um item pertence a um único pedido. Nesse caso, a tabela pedidos é o lado um e a tabela itens é o lado muitos. |
| **`many-to-many`** | A relação entre produtos e categorias: um produto pode pertencer a muitas categorias e uma categoria pode conter muitos produtos. |

{style="table-layout:auto"}

Quando uma relação entre duas tabelas é compreendida, ela pode ser usada para determinar qual caminho deve ser criado para trazer informações de uma tabela para outra. Essa próxima etapa requer conhecer as chaves primária e externa que facilitam um relacionamento de tabela.

### Chaves primárias e externas {#keys}

A `Primary Key` é uma coluna inalterável ou um conjunto de colunas que produz valores únicos em uma tabela. Por exemplo, quando um cliente faz uma solicitar em um site, uma nova linha é adicionada à `orders` tabela em seu carrinho de compras, com um novo `order_id` . Isso `order_id` permite que o cliente e a empresa faixam o progresso dessa solicitar específica. Como o solicitar ID é exclusivo, normalmente é a `Primary Key` de uma `orders` tabela.

A `Foreign Key` é uma coluna criada dentro de uma tabela vinculada à `Primary Key` coluna de outra tabela. As Chaves estrangeiras criam referências entre tabelas, permitindo que os analistas pesquisem e vinculem registros facilmente. Diga que você queria saber quais pedidos pertenciam a cada um de seus clientes. A variável `customer id` coluna (`Primary Key` do `customers` tabela) e a `order_id` coluna (`Foreign Key` no `customers` tabela, fazendo referência ao `Primary Key` do `orders` tabela) permite vincular e analisar essas informações. Ao criar um caminho, você é solicitado a definir as variáveis `Primary Key` e `Foreign Key`.

## Criação de um caminho {#createpath}

Ao criar uma coluna no data warehouse, você deve definir o caminho que traz informações de uma tabela para outra. Às vezes, os caminhos são preenchidos previamente porque um caminho existe entre as tabelas, mas se isso não acontecer, você deve criar um.

Use o relacionamento entre **clientes** e **pedidos** para mostrar como isso é feito. Dividido:

* O relacionamento é `one-to-many` -um cliente pode ter muitos pedidos, mas um solicitar pode ter somente um cliente. Isso nos informa a direção do relacionamento ou onde a coluna calculada deve ser criada. Nesse caso, isso significa que as informações da `orders` tabela podem ser trazidas para a `customers` tabela.
* O `primary key` que você deseja usar é `customers.customerid` ou a `customer ID` coluna na `customers` tabela.
* O `foreign key` que você deseja usar é `orders.customerid` ou a `customer ID` coluna na `orders` tabela.

Agora, você pode criar o caminho.

1. Clique em **[!UICONTROL Data > Data Warehouse]**.
1. Na lista da tabela, clique na tabela na qual deseja criar a coluna. Neste exemplo, é o `customers` tabela.
1. O esquema de tabela é exibido. Clique em **[!UICONTROL Create New Column]** .
1. Dê um nome à sua coluna, por exemplo, `Customer's orders` .
1. Selecione a definição da coluna. Confira a [ guia ](../data-warehouse-mgr/creating-calculated-columns.md) de coluna calculada para obter uma planilha de inconveniente.
1. [!UICONTROL Select table and column]Na lista suspensa, clique na **[!UICONTROL Create new path]** opção.

   ![Criação de caminhos para colunas calculadas modal](../../assets/Creating_Paths_modal.png)

1. Usando as listas suspensas, selecione as chaves primária e estrangeira para cada tabela.

   No `Many` lado, selecione `orders.customerid` - lembre-se, os clientes podem ter muitos pedidos.

   No `One` lado, selecione `customers.customerid` - um pedido só pode ter um cliente.

1. Clique em **[!UICONTROL Save]** para salvar o caminho e concluir a criação da coluna.

### Limitações de criação de caminhos {#limits}

* **[!DNL Commerce Intelligence]Não é possível adivinhar as relações** de chave primária/externa. Você não deseja apresentar dados incorretos no seu conta, portanto, criar caminhos deve ser feito manualmente.

* **No momento, os caminhos só podem ser especificados entre duas tabelas** diferentes. A lógica que você está tentando recriar envolve mais de duas tabelas? Em seguida, pode fazer sentido (1) unir as colunas a uma tabela intermediária primeiro, depois para a tabela &quot;destino final&quot; ou (2) consulte o [ equipe ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) serviços profissionais para encontrar a melhor abordagem para suas metas.

* **Uma coluna pode ser somente a referência da chave externa para um caminho de cada vez** . Por exemplo, se `order_items.order_id` apontar para `orders.id` , `order_items.order_id` não poderá apontar para nada mais.

* **`Many-to-many`tecnicamente podem ser criados, mas geralmente produzem dados ruins porque nenhum dos lados é verdadeiro `one-to-many` chave estrangeira**. A melhor maneira de abordar esses caminhos sempre depende da análise específica desejada. Consulte a equipe de analistas do RJ para descobrir a melhor solução.

Se você for impedido de criar uma coluna calculada devido a uma ou mais limitações acima, entre em contato com o suporte com uma descrição da coluna em que você está

## Excluir um caminho de coluna calculado {#delete}

Um caminho incorreto foi criado no data warehouse? Ou talvez você esteja fazendo uma pequena limpeza de mola e deseje se organizar? Se precisar excluir um caminho do seu conta, você pode [ enviar um bilhete para Adobe Systems analistas ](../../guide-overview.md#Submitting-a-Support-Ticket) de suporte. **Certifique-se de incluir o nome do caminho.**

## Resumindo {#wrapup}

Agora que você está confortável para criar caminhos para colunas calculadas no data warehouse. Se não tiver certeza sobre um caminho específico, lembre-se de que você sempre pode clicar em **[!UICONTROL Support]** no seu [!DNL Commerce Intelligence] conta para obter assistência.

## Relacionados

* [Entendendo e avaliando relações de tabelas](../data-warehouse-mgr/table-relationships.md)
* [Criação de caminhos para colunas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos ](../data-warehouse-mgr/calc-column-types.md) de coluna calculados que tentam criar.
