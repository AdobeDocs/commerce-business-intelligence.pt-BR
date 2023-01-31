---
title: Criar ou excluir caminhos para colunas calculadas
description: Saiba como definir um caminho descrevendo como a tabela na qual você está criando uma coluna está relacionada à tabela da qual você está extraindo informações.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Criar ou excluir caminhos para colunas calculadas

## Refresher colunas calculadas

When [criação de colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) em sua Data Warehouse, você será solicitado a definir um caminho descrevendo como a tabela na qual você está criando uma coluna está relacionada à tabela da qual você está extraindo informações. Para criar um caminho com êxito, você precisa saber duas coisas:

1. Como as tabelas em seus bancos de dados se relacionam
1. As chaves primárias e estrangeiras que definem essa relação

Se você souber essas informações, poderá criar facilmente um caminho seguindo as instruções deste artigo. Fornecemos uma visão geral desses conceitos se você estiver se sentindo um pouco inseguro, mas talvez queira perguntar a um especialista técnico em sua organização ou entrar em contato com a equipe de suporte.

## Atualizações sobre relacionamentos de tabela e tipos de chave {#refresher}

### Relacionamentos de Tabela {#relationships}

Nós cobrimos este conceito em profundidade em nossa [Artigo Noções básicas e avaliação de relações de tabela](../../data-analyst/data-warehouse-mgr/table-relationships.md)Mas um resumo rápido nunca machucou ninguém, certo?

As tabelas podem ser relacionadas entre si de uma das três formas a seguir:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | A relação entre pessoas e números de carta de condução. Uma pessoa pode ter um e apenas um número de carta de condução, e o número de carta de condução pertence a uma única pessoa. |
| **`one-to-many`** | A relação entre pedidos e itens - um pedido pode conter muitos itens, mas um item pertence a um único pedido. Nesse caso, a tabela de pedidos é de um lado e a tabela de itens é de vários lados. |
| **`many-to-many`** | A relação entre produtos e categorias: um produto pode pertencer a muitas categorias e uma categoria pode conter muitos produtos. |

{style=&quot;table-layout:auto&quot;}

Assim que uma relação entre duas tabelas for entendida, ela poderá ser usada para determinar qual caminho deve ser criado para trazer as informações de uma tabela para outra. Esta próxima etapa requer conhecer as chaves primárias e estrangeiras que facilitam um relacionamento de tabela.

### Chaves primárias e estrangeiras {#keys}

A `Primary Key` é uma coluna ou conjunto de colunas inalterável que produz valores exclusivos em uma tabela. Por exemplo, quando um cliente faz um pedido em um site, uma nova linha é adicionada à variável `orders` tabela em seu carrinho de compras, com um novo `order_id`. Essa `order_id` permite que o cliente e a empresa acompanhem o progresso dessa ordem específica. Como a ID do pedido é exclusiva, geralmente é a variável `Primary Key` de um `orders` tabela.

A `Foreign Key` é uma coluna criada dentro de uma tabela que se vincula ao `Primary Key` de outra tabela. Chaves estrangeiras criam referências entre tabelas, permitindo que os analistas pesquisem facilmente e vinculem registros. Digamos que queríamos saber quais pedidos pertenciam a cada um de nossos clientes. O `customer id` column (`Primary Key` do `customers` tabela) e o `order_id` column (`Foreign Key` no `customers` , referenciando a `Primary Key` do `orders` tabela) nos permite vincular e analisar essas informações. Ao criar um caminho, você será solicitado a definir ambas as variáveis `Primary Key` e `Foreign Key`.

## Criação de um caminho {#createpath}

Ao criar uma coluna no data warehouse, é necessário definir o caminho que traz informações de uma tabela para outra. Às vezes, os caminhos são preenchidos previamente, pois um caminho já existe entre tabelas, mas se isso não acontecer, será necessário criar um.

Usamos a relação entre **clientes** e **ordens** para mostrar como é feito. Analisado:

* A relação é `one-to-many` - um cliente pode ter muitas ordens, mas uma ordem só pode ter um cliente. Isso nos informa a direção do relacionamento ou onde a coluna calculada deve ser criada. Nesse caso, significa informações do `orders` pode ser trazida para o `customers` tabela.
* O `primary key` queremos usar é `customers.customerid`ou o `customer ID` na coluna `customers` tabela.
* O `foreign key` queremos usar é `orders.customerid`ou o `customer ID` na coluna `orders` tabela.

Agora, nós os guiamos até criando o caminho.

1. Clique em **[!UICONTROL Data > Data Warehouse]**.
1. Na lista da tabela, clique na tabela na qual deseja criar a coluna. No nosso exemplo, é o `customers` tabela.
1. O schema da tabela será exibido. Clique em **[!UICONTROL Create New Column]**.
1. Dê um nome à coluna - por exemplo, `Customer's orders`.
1. Selecione a definição da coluna. Confira o [Guia de Coluna Calculada](../data-warehouse-mgr/creating-calculated-columns.md) para uma folha de trapaça útil.
1. No [!UICONTROL Select table and column] , clique no botão **[!UICONTROL Create new path]** opção.

   ![Criação de caminhos para o modal de colunas calculadas](../../assets/Creating_Paths_modal.png)

1. Usando as listas suspensas, selecione as chaves primária e estrangeira para cada tabela.

   No `Many` lado, selecionamos `orders.customerid` - lembre-se, os clientes podem ter muitos pedidos.

   No `One` lado, selecionamos `customers.customerid` - um pedido só pode ter um cliente.

1. Clique em **[!UICONTROL Save]** para salvar o caminho e concluir a criação da coluna.

### Limitações da criação de caminhos {#limits}

* **[!DNL MBI]não é possível adivinhar relações de chave primária/estrangeira**. Não queremos inserir dados incorretos em sua conta, portanto, a criação de caminhos deve ser feita manualmente.
* **Atualmente, os caminhos só podem ser especificados entre duas tabelas diferentes**. A lógica que você está tentando recriar envolve mais de duas tabelas? Assim, pode fazer sentido (1) unir as colunas a uma tabela intermediária primeiro, depois à tabela de &quot;destino final&quot; ou (2) consultar nossa equipe para encontrar a melhor abordagem para suas metas.
* **Uma coluna só pode ser a referência de chave externa para um caminho ONE de uma vez**. Por exemplo, se `order_items.order_id` pontos a `orders.id`, em seguida `order_items.order_id` não pode apontar para mais nada.
* **`Many-to-many`caminhos podem ser criados tecnicamente, mas muito frequentemente produzirão dados ruins, pois nenhum dos lados é um verdadeiro `one-to-many` chave externa**. A melhor maneira de abordar esses caminhos sempre depende da análise específica desejada. Consulte a equipe de analistas RJ para descobrir a melhor solução.

Se você não conseguir criar uma coluna calculada devido a uma ou mais das limitações acima, entre em contato com o suporte com uma descrição da coluna na qual você está

## Excluir um caminho de coluna calculada {#delete}

Criou um caminho incorreto na sua Data Warehouse? Ou talvez você esteja fazendo uma limpeza de primavera e queira arrumar? Se precisar excluir um caminho de sua conta, você pode [envie um tíquete para nossos analistas de suporte](../../guide-overview.md). **Certifique-se de incluir o nome do caminho!**

## Quebra de linha {#wrapup}

Agora você pode se sentir confortável em criar caminhos para colunas calculadas em sua Data Warehouse. Se você ainda não tiver certeza sobre um caminho específico, lembre-se de que sempre pode clicar em **[!UICONTROL Support]** em seu [!DNL MBI] para obter assistência.

## Relacionado

* [Como entender e avaliar relações de tabela](../data-warehouse-mgr/table-relationships.md)
* [Criação de caminhos para colunas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos de Colunas Calculadas](../data-warehouse-mgr/calc-column-types.md) tentando criar.
