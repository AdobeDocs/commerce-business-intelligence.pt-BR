---
title: Compreender e avaliar os relacionamentos de tabela
description: Saiba como entender quantas ocorrências possíveis em uma tabela podem pertencer a uma entidade em outra, e vice-versa.
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Compreender e avaliar os relacionamentos de tabela

Ao avaliar a relação entre duas tabelas fornecidas, é necessário entender quantas ocorrências possíveis em uma tabela podem pertencer a uma entidade em outra, e vice-versa. Por exemplo, vamos usar um `users` tabela e uma `orders` tabela. Nesse caso, você quer saber quantos **ordens** um **usuário** , e quantos **usuários** um **pedido** poderia pertencer a.

Compreender os relacionamentos é essencial para manter a integridade dos dados, pois afeta a precisão de seus [colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) e [dimensões](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Para saber mais, consulte [tipos de relacionamento](#types) e [como avaliar as tabelas em sua Data Warehouse.](#eval)

## Tipos de relacionamento {#types}

Existem três tipos de relações que podem existir entre duas tabelas:

* [&quot;um para um&quot;](#onetoone)
* [&quot;um para muitos&quot;](#onetomany)
* [&quot;muitos para muitos&quot;](#manytomany)

### `One-to-One` {#onetoone}

Em um `one-to-one` relacionamento, um registro na Tabela `B` pertence a um e a apenas um registro na Tabela `A`. E um registro na Tabela `A` pertence a um e a apenas um registro na Tabela `B`.

Por exemplo, na relação entre pessoas e números de carta de condução, uma pessoa pode ter um e apenas um número de carta de condução, e o número de carta de condução pertence a uma e a uma única pessoa.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

Em um `one-to-many` relacionamento, um registro na Tabela `A` pode pertencer a vários registros na Tabela `B`. Pense na relação entre `orders` e `items` - um pedido pode conter muitos itens, mas um item pertence a um único pedido. Nesse caso, a variável `orders` a tabela é de um lado e o `items` mesa é o lado de muitos.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

Em um `many-to-many` relacionamento, um registro na Tabela `B` pode pertencer a vários registros na Tabela `A`. E vice-versa, um registro na Tabela `A` pode pertencer a vários registros na Tabela `B`.

Pense na relação entre **products** e **categorias**: um produto pode pertencer a muitas categorias e uma categoria pode conter muitos produtos.

![](../../assets/many-to-many.png)

## Avaliar suas tabelas {#eval}

Dados os tipos de relacionamentos que existem entre tabelas, você pode aprender a avaliar as tabelas em seu data warehouse. À medida que esses relacionamentos formam a forma como as colunas calculadas de várias tabelas são definidas, é importante entender como identificar os relacionamentos de tabela e que lado - `one` ou `many` - o quadro pertence a.

Há dois métodos que você pode usar para avaliar as relações de um determinado par de tabelas na sua Data Warehouse. O primeiro método emprega um [quadro conceptual](#concept) que considera como as entidades da tabela interagem entre si. O segundo método utiliza o [schema da tabela](#schema).

### Uso da Estrutura Conceitual {#concept}

Esse método usa um quadro conceitual para descrever como as entidades nas duas tabelas são capazes de interagir umas com as outras. É importante compreender que este quadro avalia o que é possível, tendo em conta a relação existente.

Por exemplo, ao pensar em usuários e pedidos, considere tudo o que é possível no relacionamento. Um usuário registrado não pode fazer pedidos, apenas um pedido ou vários pedidos dentro de sua vida útil. Se você acabou de iniciar sua empresa e nenhum pedido foi feito ainda, ainda é possível que um determinado usuário possa colocar muitos pedidos em sua vida útil e as tabelas sejam criadas para acomodar isso.

Para usar este método:

1. Identifique a entidade que está sendo descrita em cada tabela. **Dica: geralmente é um substantivo**. Por exemplo, a variável `user` e `orders` as tabelas estão descrevendo explicitamente os usuários e pedidos.
1. Identifique os verbos que descrevem como essas entidades interagem. Por exemplo, ao comparar usuários a pedidos, os usuários &quot;colocam&quot; pedidos. Na outra direção, os pedidos &quot;pertencem&quot; aos usuários.

Esse tipo de estrutura pode ser aplicado a qualquer emparelhamento de tabelas em sua Data Warehouse, permitindo identificar facilmente o tipo de relacionamento, bem como qual tabela é um lado e qual tabela é um lado muito diferente.

Depois de identificar a terminologia que descreve como as duas tabelas interagem, enquadre a interação em ambas as direções considerando como uma determinada instância da primeira entidade se relaciona à segunda. Estes são alguns exemplos de cada relação:

### `One-to-One`

Uma determinada pessoa pode ter um e apenas um número de carta de condução. Um determinado número de carta de condução pertence a uma única pessoa.

Isso é uma `one-to-one` relacionamento em que cada tabela é de um lado.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Um determinado pedido pode possivelmente conter muitos itens. Um determinado item pertence a um e somente um pedido.

Isso é uma `one-to-many` relacionamento em que a tabela de pedidos é de um lado e a tabela de itens é de vários lados.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Um determinado produto pode possivelmente pertencer a muitas categorias. Uma determinada categoria pode conter muitos produtos.

Isso é uma `many-to-many` relacionamento em que cada tabela é um lado muito grande.

![](../../assets/many-to-many3.png)

### Uso do esquema da tabela {#schema}

O segundo método aproveita o schema da tabela. O esquema define quais colunas são as [`Primary`](http://en.wikipedia.org/wiki/Unique_key) e [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) chaves. É possível usar essas chaves para vincular tabelas e ajudar a determinar os tipos de relacionamento.

Depois de identificar as colunas que vinculam duas tabelas, use os tipos de coluna para avaliar a relação entre elas. Veja alguns exemplos:

### `One-to-one`

Se as tabelas estiverem vinculadas usando o `primary key` de ambas as tabelas, a mesma entidade exclusiva está sendo descrita em cada tabela e a relação é `one-to-one`.

Por exemplo, um `users` tabela pode capturar a maioria dos atributos do usuário (como nome) enquanto um `user_source` tabela captura fontes de registro do usuário. Em cada tabela, uma linha representa um usuário.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Você aceita pedidos de convidado? Consulte [Pedidos de convidado](../data-warehouse-mgr/guest-orders.md) para saber como os pedidos de convidado podem afetar seus relacionamentos de tabela.

Quando as tabelas são vinculadas usando um `Foreign key` apontando para um `primary key`, esta configuração descreve uma `one-to-many` relação. Um lado será a tabela que contém a variável `primary key` e o lado de muitos será a tabela contendo a variável `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Se qualquer um dos seguintes for verdadeiro, a relação será `many-to-many`:

* `Non-primary key` colunas estão sendo usadas para vincular duas tabelas
   ![](../../assets/many-to-many1.png)
* Parte de um compósito `primary key` é usada para vincular duas tabelas

![](../../assets/many-to-mnay2.png)

## Próximas etapas

Avaliar corretamente as relações da tabela é fundamental para modelar seus dados com precisão. Agora que você entende como as tabelas estão relacionadas entre si, consulte [o que você pode fazer com o Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md).
