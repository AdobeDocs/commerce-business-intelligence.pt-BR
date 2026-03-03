---
title: Armazenamento de dados no Adobe Commerce
description: Saiba como os dados são gerados, o que causa a inserção de uma nova linha e como as ações são registradas no banco de dados do Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Armazenando Dados em [!DNL Adobe Commerce]

A plataforma [!DNL Adobe Commerce] registra e organiza uma grande variedade de dados comerciais valiosos em centenas de tabelas. Este tópico descreve:

* como esses dados são gerados
* o que faz com que uma nova linha seja inserida em uma das [Tabelas principais do Commerce](../data-warehouse-mgr/common-mage-tables.md)
* como ações como fazer uma compra ou criar uma conta são registradas no banco de dados do [!DNL Adobe Commerce]

Para discutir esses conceitos, consulte o seguinte exemplo:

`Clothes4U` é um retailer de roupas com presença online e física. Ele usa [!DNL Magento Open Source] por trás de seu site para coletar e organizar dados.

## `catalog\_product\_entity`

É 22 de setembro e `Clothes4U` está lançando três novos itens para sua linha de outono: `Throwback Bellbottoms`, `Straight Leg Jeans` e `V-Neck T-Shirts`. Um funcionário do `Clothes4U` abre o Administrador do Commerce, clica em **[!UICONTROL Add Product]** e insere todas as informações para `Throwback Bellbottoms`.

Satisfeito com todas as configurações para `Throwback Bellbottoms`, o funcionário clica em **[!UICONTROL Save]**, que insere a primeira linha abaixo na tabela `catalog_product_entity`. O funcionário repete o processo, criando outro produto Commerce para `Straight Leg Jeans` e, em seguida, um terceiro para `V-Neck T-Shirt`, inserindo a segunda e terceira linhas abaixo na tabela `catalog_product_entity`:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Calças10 | 09/2016/22 09:15:43 |
| 206 | 4 | 8 | Calças11 | 09/2016/22 09:18:17 |
| 207 | 4 | 12 | Camisas6 | 09/2016/22 09:24:02 |

* `entity_id` - Esta é a chave primária da tabela `catalog_product_entity`, o que significa que cada linha da tabela deve ter um `entity_id` diferente. Cada `entity_id` nessa tabela pode ser associado a apenas um produto, e cada produto só pode ser associado a um `entity_id`
   * A linha superior da tabela acima, `entity_id` = 205, é a nova linha criada para &quot;Throwback Bellbottom&quot;. Sempre que `entity_id` = 205 for exibido na plataforma do Commerce, ele se refere ao produto &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - O Commerce tem várias categorias de objetos (como clientes, endereços e produtos, para citar algumas), e essa coluna é usada para indicar a categoria na qual essa linha específica se enquadra.
   * Sendo esta a tabela `catalog_product_entity`, cada linha tem o mesmo tipo de entidade: produto. No Adobe Commerce, o `entity_type_id` para o produto é 4, razão pela qual todos os três novos produtos criados retornam 4 para esta coluna.
* `attribute_set_id` - Os conjuntos de atributos são usados para identificar produtos que têm o mesmo tipo de descritores.
   * As duas primeiras linhas da tabela são os produtos `Throwback Bellbottoms` e `Straight Leg Jeans`, que são calças. Esses produtos teriam os mesmos descritores (por exemplo, nome, inseto, cintura) e, portanto, teriam o mesmo `attribute_set_id`. O terceiro item, `V-Neck T-Shirt` tem um `attribute_set_id` diferente porque não teria os mesmos descritores que as calças; as camisas não têm cós ou insetos.
* `sku` - São valores únicos atribuídos a cada produto pelo usuário ao criar um produto no Adobe Commerce.
* `created_at` - Esta coluna retorna o carimbo de data e hora de quando cada produto foi criado

## `customer\_entity`

Logo após a adição dos três novos produtos, um novo cliente, `Sammy Customer`, visita o site de `Clothes4U` pela primeira vez. Como `Clothes4U` não permite pedidos de convidados, `Sammy Customer` deve primeiro criar uma conta no site. O cliente insere as credenciais necessárias e clica em enviar, resultando na seguinte nova entrada no [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Assim como a tabela anterior, `entity_id` é a chave primária da tabela `customer_entity`.
   * Quando `Sammy Customer` criou uma conta e a linha acima foi gravada na tabela `customer_entity`, foi atribuído ao cliente `entity_id` = 214. Em todas as tabelas, o cliente identificado como `entity_id` = 214 sempre se refere ao usuário Sammy Customer
* `entity_type_id` - Esta coluna identifica que tipo de entidade está sendo listado nesta tabela e funciona da mesma forma que na tabela `catalog_product_entity`
   * Cada linha da tabela `customer_entity` é um cliente, e a Commerce define os clientes como `entity_type_id` 1 por padrão
* `email` - este campo é preenchido pelo email que um novo cliente insere ao fazer sua conta
* `created_at` - Esta coluna retorna o carimbo de data/hora de quando cada usuário ingressou

## `sales\_flat\_order (or Sales\_order` se você tiver [!DNL Adobe Commerce 2.x]

Com a criação da conta concluída, `Sammy Customer` está pronto para começar a fazer uma compra. No site, o cliente adiciona dois pares do `Throwback Bellbottoms` e um `V-Neck T-Shirt` ao carrinho. Satisfeito com as seleções, o cliente passa para o check-out e envia o pedido, criando a seguinte entrada na [tabela de ordem simples de venda](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 23/09/2016 15:41:39 |

* `entity_id` - esta é a chave primária da tabela `sales_flat_order`.
   * Quando Sammy Customer fez este pedido e a linha acima foi gravada na tabela `sales_flat_order`, o pedido foi atribuído `entity_id` = 227.
* `customer_id` - Esta coluna é o identificador exclusivo do cliente que fez este pedido específico
   * O `customer_id` associado a este pedido é 214, que é o `entity_id` do Sammy Customer na tabela `customer_entity`.
* `subtotal` - Esta coluna é o valor total cobrado de um cliente pelo pedido
   * Os dois pares de &quot;Throwback Bellbottom&quot; e &quot;V-Neck T-Shirt&quot; custam US $ 94,85 no total
* `created_at` - Esta coluna retorna o carimbo de data/hora de quando cada pedido foi criado

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(se você tiver o Commerce 2.0 ou posterior)

Além da única linha na tabela `Sales\_flat\_order`, quando `Sammy Customer` envia a ordem, uma linha para cada item único nessa ordem é inserida na tabela [`sales\_flat\_order\_item`](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Esta coluna é a chave primária da tabela `sales_flat_order_item`
   * A ordem de `Sammy Customer` criou duas linhas nesta tabela porque a ordem continha dois produtos distintos
* `name` - Esta coluna é o nome do produto
* `product_id` - Esta coluna é o identificador exclusivo do produto ao qual esta linha se refere
   * A primeira linha acima tem `product_id` = 205 porque `Throwback Bellbottoms` tem um `entity_id` de 205 na tabela `catalog_product_entity`
* `order_id` - Esta coluna é o `entity_id` da ordem que contém estes itens de ordem específicos
   * Ambas as linhas acima têm `order_id` = 227 porque ambas fazem parte da ordem colocada por `Sammy Customer`, que tem `entity_id` = 227 na tabela `sales_flat_order`
* `qty_ordered` - Esta coluna é o número de unidades do produto incluídas neste pedido específico
   * A ordem de `Sammy Customer` continha dois pares de `Throwback Bellbottoms`
* `price` - Esta coluna é o preço de uma única unidade do item do pedido
   * O `subtotal` da ordem de `Sammy Customer` na tabela `sales_flat_order` era 94,85, que é a soma de dois pares de `Throwback Bellbottoms` a $39,95 cada um e 1 `V-Neck T-Shirt` a $14,95.
