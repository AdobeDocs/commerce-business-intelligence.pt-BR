---
title: Entender e avaliar as relações de tabela
description: Saiba como entender quantas ocorrências possíveis em uma tabela podem pertencer a uma entidade em outra.
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# Entender e avaliar as relações de tabela

Ao avaliar a relação entre duas determinadas tabelas, você precisa entender quantas ocorrências possíveis em uma tabela poderiam pertencer a uma entidade em outra, e vice-versa. Por exemplo, use um `users` tabela e um `orders` tabela. Nesse caso, você quer saber quantas **pedidos** um determinado **usuário** tenha colocado e o número possível de **usuários** um **pedido** pode pertencer a.

Entender relacionamentos é vital para manter a integridade dos dados, pois isso afeta a precisão de seus [colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) e [dimensões](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Para saber mais, consulte [tipos de relacionamento](#types) e [como avaliar as tabelas na Data Warehouse.](#eval)

## Tipos de relacionamento {#types}

Há três tipos de relações que podem existir entre duas tabelas:

1. [&quot;um para um&quot;](#onetoone)
1. [&quot;de um para muitos&quot;](#onetomany)
1. [`muitos para muitos`](#manytomany)

### `One-to-One` {#onetoone}

Em um `one-to-one` relacionamento, um registro na tabela `B` pertence a apenas um registro na tabela `A`. E um recorde na tabela `A` pertence a apenas um registro na Tabela `B`.

Por exemplo, no relacionamento entre pessoas e números de carteira de motorista, uma pessoa pode ter apenas um número de carteira de motorista, e um número de carteira de motorista pertence a apenas uma pessoa.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

Em um `one-to-many` relacionamento, um registro na tabela `A` pode pertencer a vários registros na tabela `B`. Pense na relação entre `orders` e `items` - um pedido pode conter muitos itens, mas um item pertence a um único pedido. Neste caso, o `orders` a tabela é um lado e o `items` a mesa é o lado muitos.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

Em um `many-to-many` relacionamento, um registro na tabela `B` pode pertencer a vários registros na tabela `A`. E vice-versa, um recorde na tabela `A` pode pertencer a vários registros na tabela `B`.

Pense na relação entre **products** e **categorias**: um produto pode pertencer a muitas categorias, e uma categoria pode conter muitos produtos.

![](../../assets/many-to-many.png)

## Avaliando Suas Tabelas {#eval}

Dados os tipos de relações que existem entre tabelas, você pode aprender a avaliar as tabelas em sua Data Warehouse. À medida que esses relacionamentos moldam como as colunas calculadas de várias tabelas são definidas, é importante entender como identificar os relacionamentos entre tabelas e qual lado. `one` ou `many` - a tabela pertence a.

Há dois métodos que podem ser usados para avaliar os relacionamentos de um determinado par de tabelas dentro da Data Warehouse. O primeiro método utiliza um [quadro conceptual](#concept) que considera como as entidades da tabela interagem entre si. O segundo método usa o [esquema da tabela](#schema).

### Uso da Estrutura Conceitual {#concept}

Esse método usa uma estrutura conceitual para descrever como as entidades nas duas tabelas podem interagir entre si. É importante entender que esse arcabouço avalia o que é possível, dada a relação.

Por exemplo, ao pensar em usuários e pedidos, considere tudo o que é possível no relacionamento. Um usuário registrado não pode fazer pedidos, fazer apenas um pedido ou fazer vários pedidos durante sua vida útil. Se você iniciou sua empresa e nenhum pedido foi feito, é possível que um determinado usuário possa fazer muitos pedidos ao longo de sua vida útil. As tabelas são criadas para acomodar isso.

Para usar este método:

1. Identifique a entidade que está sendo descrita em cada tabela. **Dica: geralmente é um substantivo**. Por exemplo, a variável `user` e `orders` As tabelas descrevem explicitamente usuários e pedidos.

1. Identifique um ou mais verbos que descrevam como essas entidades interagem. Por exemplo, ao comparar usuários a pedidos, os usuários &quot;fazem&quot; pedidos. Indo na outra direção, os pedidos &quot;pertencem&quot; aos usuários.

Esse tipo de estrutura pode ser aplicado a qualquer par de tabelas na Data Warehouse. Isso permite identificar facilmente o tipo de relação e qual tabela está em um lado e qual tabela está em vários lados.

Depois de identificar a terminologia que descreve como as duas tabelas interagem, enquadre a interação em ambas as direções considerando como uma determinada instância da primeira entidade se relaciona com a segunda. Estes são alguns exemplos de cada relação:

### `One-to-One`

Uma determinada pessoa só pode ter um número de carteira de motorista. Um determinado número de carteira de motorista pertence a apenas uma pessoa.

Este é um `one-to-one` relação em que cada tabela é um lado.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Uma determinada ordem pode conter muitos itens. Um determinado item pertence a apenas um pedido.

Este é um `one-to-many` relação em que a tabela pedidos é um lado e a tabela itens é o lado muitos.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Um determinado produto pode possivelmente pertencer a muitas categorias. Uma determinada categoria pode conter muitos produtos.

Este é um `many-to-many` relação em que cada tabela é um lado muitos.

![](../../assets/many-to-many3.png)

### Usando o Esquema da Tabela {#schema}

O segundo método usa o schema da tabela. O esquema define quais colunas são as [`Primary`](https://en.wikipedia.org/wiki/Unique_key) e [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) chaves. Você pode usar essas chaves para vincular tabelas e ajudar a determinar os tipos de relacionamento.

Depois de identificar as colunas que vinculam duas tabelas, use os tipos de coluna para avaliar o relacionamento da tabela. Veja alguns exemplos:

### `One-to-one`

Se as tabelas estiverem vinculadas usando a variável `primary key` de ambas as tabelas, a mesma entidade única está sendo descrita em cada tabela e a relação é `one-to-one`.

Por exemplo, uma variável `users` tabela pode capturar a maioria dos atributos do usuário (como nome) enquanto uma tabela complementar `user_source` A tabela captura fontes de registro do usuário. Em cada tabela, uma linha representa um usuário.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Você aceita ordens de convidados? Consulte [Pedidos de convidados](../data-warehouse-mgr/guest-orders.md) para saber como as ordens de convidados podem afetar seus relacionamentos de tabela.

Quando as tabelas são vinculadas usando um `Foreign key` apontando para um `primary key`, esta configuração descreve uma `one-to-many` relação. O lado um é o quadro que contém o `primary key` e o lado muitos é a tabela que contém o `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Se uma das situações a seguir for verdadeira, a relação será `many-to-many`:

* `Non-primary key` as colunas estão sendo usadas para vincular duas tabelas
   ![](../../assets/many-to-many1.png)
* Parte de um composto `primary key` é usado para vincular duas tabelas

![](../../assets/many-to-mnay2.png)

## Próximas etapas

A avaliação correta das relações de tabela é essencial para a modelagem precisa dos dados. Agora que você entende como as tabelas estão relacionadas umas com as outras, consulte [o que você pode fazer com o Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md).
