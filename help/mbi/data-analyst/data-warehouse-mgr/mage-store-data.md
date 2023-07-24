---
title: Armazenamento de dados no Adobe Commerce
description: Saiba como os dados são gerados, o que causa a inserção de uma nova linha e como as ações são registradas no banco de dados do Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Armazenamento de dados em [!DNL Adobe Commerce]

A variável [!DNL Adobe Commerce] A platform registra e organiza uma grande variedade de dados comerciais valiosos em centenas de tabelas. Este tópico descreve:

* como esses dados são gerados
* o que faz com que uma nova linha seja inserida em uma das [Tabelas principais do Commerce](../data-warehouse-mgr/common-mage-tables.md)
* como ações como fazer uma compra ou criar uma conta são registradas na [!DNL Adobe Commerce] banco de dados

Para discutir esses conceitos, consulte o seguinte exemplo:

`Clothes4U` A é uma varejista de roupas com presença on-line e de tijolo e argamassa. Usa [!DNL Magento Open Source] por trás de seu site para coletar e organizar dados.

## `catalog\_product\_entity`

É 22 de setembro e `Clothes4U` O está lançando três novos itens para sua linha de outono: `Throwback Bellbottoms`, `Straight Leg Jeans`, e `V-Neck T-Shirts`. A `Clothes4U` funcionário abrir o Administrador do Commerce, cliques em **[!UICONTROL Add Product]** e insere todas as informações para `Throwback Bellbottoms`.

Satisfeito com todas as configurações para `Throwback Bellbottoms`, o funcionário clica **[!UICONTROL Save]**, que insere a primeira linha abaixo na `catalog_product_entity` tabela. O funcionário repete o processo, criando outro produto do Commerce para `Straight Leg Jeans`e, em seguida, um terceiro para `V-Neck T-Shirt`, inserindo a segunda e a terceira linhas abaixo na `catalog_product_entity` tabela:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Essa é a chave primária do `catalog_product_entity` tabela, o que significa que cada linha da tabela deve ter uma `entity_id`. Each `entity_id` nesta tabela só pode ser associado a um produto, e cada produto só pode ser associado a um `entity_id`
   * A linha superior da tabela acima, `entity_id` = 205, é a nova linha criada para &quot;Throwback Bellbottom&quot;. Onde quer que `entity_id` = 205 aparece na plataforma Commerce, se refere ao produto &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - O Commerce tem várias categorias de objetos (como clientes, endereços e produtos, para citar algumas), e essa coluna é usada para indicar a categoria na qual essa linha específica se enquadra.
   * Sendo este o `catalog_product_entity` cada linha tem o mesmo tipo de entidade: produto. No Adobe Commerce, a variável `entity_type_id` para produto é 4, por isso todos os três novos produtos criados retornam 4 para esta coluna.
* `attribute_set_id` - Os conjuntos de atributos são usados para identificar produtos que têm o mesmo tipo de descritores.
   * As duas primeiras linhas da tabela são a `Throwback Bellbottoms` e `Straight Leg Jeans` produtos, sendo que ambos são calças. Esses produtos teriam os mesmos descritores (por exemplo, nome, inseto, cintura) e, portanto, teriam os mesmos `attribute_set_id`. O terceiro item, `V-Neck T-Shirt` tem uma diferente `attribute_set_id` porque não teria os mesmos descritores que as calças; camisas não têm cintura ou insetos.
* `sku` - São valores exclusivos atribuídos a cada produto pelo usuário ao criar um produto no Adobe Commerce.
* `created_at` - Essa coluna retorna a marca de data e hora de quando cada produto foi criado

## `customer\_entity`

Logo após a adição dos três novos produtos, um novo cliente, `Sammy Customer`, visitas `Clothes4U`Site do pela primeira vez. Desde `Clothes4U` não permite ordens de convidados, `Sammy Customer` O deve primeiro criar uma conta no site. O cliente digita as credenciais necessárias e clica em enviar, resultando na seguinte nova entrada na [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Assim como a mesa anterior, `entity_id` é a chave primária do `customer_entity` tabela.
   * Quando `Sammy Customer` criou uma conta e a linha acima foi gravada na `customer_entity` tabela, o cliente foi atribuído `entity_id` = 214 Em todas as tabelas, o cliente identificou como `entity_id` = 214 sempre se refere ao usuário Sammy Customer
* `entity_type_id` - Essa coluna identifica que tipo de entidade está sendo listado nessa tabela e funciona da mesma maneira que na `catalog_product_entity` tabela
   * Todas as linhas no `customer_entity` A tabela é um cliente e o Commerce define os clientes como `entity_type_id` 1 por padrão
* `email` - esse campo é preenchido pelo email que um novo cliente insere ao fazer sua conta
* `created_at` - Essa coluna retorna o carimbo de data e hora de quando cada usuário ingressou

## `sales\_flat\_order (or Sales\_order` se você tiver [!DNL Adobe Commerce 2.x]

Com a criação da conta concluída, `Sammy Customer` O está pronto para começar a fazer uma compra. No site, o cliente adiciona dois pares do `Throwback Bellbottoms` e um `V-Neck T-Shirt` ao carrinho. Satisfeito com as seleções, o cliente passa para o check-out e envia o pedido, criando a seguinte entrada no [tabela de ordem simples de venda](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - esta é a chave primária do `sales_flat_order` tabela.
   * Quando Sammy Customer fez este pedido e a linha acima foi gravada na `sales_flat_order` tabela, o pedido foi atribuído `entity_id` = 227
* `customer_id` - Essa coluna é o identificador exclusivo do cliente que fez esse pedido específico
   * A variável `customer_id` associado a este pedido é 214, que é do Sammy Customer `entity_id` no `customer_entity` tabela.
* `subtotal` - Essa coluna é o valor total cobrado de um cliente pelo pedido
   * Os dois pares de &quot;Throwback Bellbottom&quot; e &quot;V-Neck T-Shirt&quot; custam US $ 94,85 no total
* `created_at` - Essa coluna retorna o carimbo de data e hora de quando cada pedido foi criado

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(se você tiver o Commerce 2.0 ou posterior)

Além da única linha no `Sales\_flat\_order` tabela, quando `Sammy Customer` envia a ordem, uma linha para cada item único nessa ordem é inserida na [`sales\_flat\_order\_item` tabela](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - Essa coluna é a chave primária do `sales_flat_order_item` tabela
   * `Sammy Customer`O pedido de criou duas linhas nesta tabela porque o pedido continha dois produtos distintos
* `name` - Esta coluna é o nome do produto
* `product_id` - Esta coluna é o identificador exclusivo do produto ao qual esta linha se refere
   * A primeira linha acima tem `product_id` = 205 porque `Throwback Bellbottoms` ter um `entity_id` de 205 sobre o `catalog_product_entity` tabela
* `order_id` - Esta coluna é a `entity_id` do pedido que contém esses itens de pedido específicos
   * Ambas as linhas acima têm `order_id` = 227 porque ambos fazem parte do pedido feito por `Sammy Customer`, que `entity_id` = 227 no `sales_flat_order` tabela
* `qty_ordered` - Esta coluna indica o número de unidades do produto incluídas neste pedido específico
   * `Sammy Customer`A ordem de continha dois pares de `Throwback Bellbottoms`
* `price` - Essa coluna é o preço de uma única unidade do item do pedido
   * A variável `subtotal` de `Sammy Customer`A ordem do no `sales_flat_order` tabela era de 94,85, que é a soma de dois pares de `Throwback Bellbottoms` US$ 39,95 cada e 1 `V-Neck T-Shirt` US$ 14,95.
