---
title: Armazenamento de dados no Commerce
description: Saiba como os dados são gerados, o que exatamente faz com que uma nova linha seja inserida em uma das Tabelas de comércio principal e como ações são executadas, como fazer uma compra ou criar uma conta registrada no banco de dados do Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Armazenamento de dados em [!DNL Magento]

A plataforma de Comércio registra e organiza uma grande variedade de dados comerciais valiosos em centenas de tabelas. Neste tópico, você aprenderá como esses dados são gerados, o que exatamente faz com que uma nova linha seja inserida em uma das [Tabelas de comércio principal](../data-warehouse-mgr/common-mage-tables.md)e como as ações são, como fazer uma compra ou criar uma conta registrada no banco de dados do Commerce. Para explicar esses conceitos, consulte o seguinte exemplo:

`Clothes4U` é um varejista de roupas com presença online e de tijolo e argamassa. Ele usa o Magento Open Source por trás de seu site para coletar e organizar dados.

## `catalog\_product\_entity`

Em 22 de setembro, e `Clothes4U` O está acumulando três novos itens na linha de outono: `Throwback Bellbottoms`, `Straight Leg Jeans`e `V-Neck T-Shirts`. A `Clothes4U` funcionário abre o Administrador de comércio, clica em **[!UICONTROL Add Product]** e insere todas as informações para `Throwback Bellbottoms`.

Satisfeito com todas as configurações de `Throwback Bellbottoms`, o funcionário clica em **[!UICONTROL Save]**, que insere a primeira linha abaixo no `catalog_product_entity` tabela. O funcionário repete o processo, criando outro novo produto do Commerce para `Straight Leg Jeans`e, em seguida, um terço por `V-Neck T-Shirt`, inserindo a segunda e a terceira linhas abaixo no `catalog_product_entity` tabela:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Calças10 | 09/20/2016:15:43º |
| 206º | 4 | 8 | Calças11 | 09/20/2016:18:17º |
| 207 | 4 | 12º | Camisas6 | 09/20/2016:24:02 |

* `entity_id` - Essa é a chave primária do `catalog_product_entity` tabela, o que significa que cada linha da tabela deve ter uma tabela diferente `entity_id`. Cada `entity_id` nesta tabela só pode ser associada a um produto, e cada produto só pode ser associado a um `entity_id`
   * A linha superior da tabela acima, `entity_id` = 205, é a nova linha criada para &quot;Bandejas de Retorno&quot;. Onde `entity_id` = 205 aparece na plataforma Commerce, ele se refere ao produto &quot;Throwback Bellbotfs&quot;
* `entity_type_id` - O Commerce tem várias categorias de objetos (como clientes, endereços e produtos para nomear alguns) e essa coluna é usada para indicar a categoria na qual essa linha específica se enquadra.
   * Este é o `catalog_product_entity` tabela, cada linha tem o mesmo tipo de entidade: produto. Na Magento, a variável `entity_type_id` para o produto é 4, por isso os três novos produtos criados retornam 4 para essa coluna.
* `attribute_set_id` - Os conjuntos de atributos são usados para identificar produtos que têm os mesmos descritores.
   * As duas primeiras linhas da tabela são as `Throwback Bellbottoms` e `Straight Leg Jeans` produtos, ambos com calças. Esses produtos teriam os mesmos descritores (por exemplo, nome, inseto, cintura) e, portanto, teriam os mesmos descritores `attribute_set_id`. O terceiro ponto, `V-Neck T-Shirt` tem um `attribute_set_id` porque não teria os mesmos descritores que as calças; as camisas não têm cinturas ou feixes.
* `sku` - Esses são valores únicos atribuídos a cada produto pelo usuário ao criar um novo produto no Magento.
* `created_at` - Essa coluna retorna o carimbo de data e hora de quando cada produto foi criado

## `customer\_entity`

Pouco depois da adição dos três novos produtos, um novo cliente, `Sammy Customer`, visitas `Clothes4U`O site do pela primeira vez. Since `Clothes4U` não [permitir pedidos de convidado](https://support.magento.com/hc/en-us/articles/360016729951-Common-Magento-Misconceptions), `Sammy Customer` deve primeiro criar uma conta no site. Ela insere suas credenciais e clica em enviar, resultando na seguinte nova entrada no [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Tal como a tabela anterior, `entity_id` é a chave primária do `customer_entity` tabela.
   * When `Sammy Customer` criou sua conta e a linha acima foi gravada no `customer_entity` mesa, ela foi atribuída `entity_id` = 214. Em todas as tabelas, o cliente identificou como `entity_id` = 214 sempre se refere ao usuário Sammy Customer
* `entity_type_id` - Esta coluna identifica o tipo de entidade que está sendo listado nesta tabela e funciona da mesma forma que na `catalog_product_entity` tabela
   * Cada linha no `customer_entity` será um cliente e o Commerce definirá clientes como `entity_type_id` 1 por padrão
* `email` - esse campo é preenchido pelo email inserido por um novo cliente ao fazer a conta
* `created_at` - Essa coluna retorna o carimbo de data e hora de quando cada usuário ingressou

## `sales\_flat\_order (or Sales\_order` se você tiver o Commerce 2.0 ou posterior)

Com a criação da conta concluída, `Sammy Customer` O está pronto para começar a comprar. Enquanto ela navega pelo site, ela adiciona dois pares da variável `Throwback Bellbottoms` e um `V-Neck T-Shirt` ao carrinho dela. Satisfeita com suas seleções, ela passa para o check-out e envia seu pedido, criando a seguinte entrada no [tabela de ordens fixas de vendas](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 23/09/2016 15:41:39º |

* `entity_id` - esta é a chave primária do `sales_flat_order` tabela.
   * Quando o Cliente Sammy fez este pedido e a linha acima foi gravada no `sales_flat_order` tabela, a ordem foi atribuída `entity_id` = 227.
* `customer_id` - Esta coluna é o identificador exclusivo do cliente que fez este pedido específico
   * O `customer_id` associado a este pedido é o 214, que é o do Sammy Customer `entity_id` no `customer_entity` tabela.
* `subtotal` - Esta coluna é o valor total cobrado a um cliente pelo pedido
   * Os 2 pares de &quot;Bellbotories&quot; e &quot;T-Shirt do Pescoço V&quot; custam $94,85 dólares no total
* `created_at` - Essa coluna retorna o carimbo de data e hora de quando cada pedido foi criado

## `sales\_flat\_order\_item ( or Sales\_order\_item` se você tiver o Commerce 2.0 ou posterior)

Além da única linha na `Sales\_flat\_order` tabela, quando `Sammy Customer` envia seu pedido, uma linha para cada item único nessa ordem é inserida na variável [`sales\_flat\_order\_item` tabela](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Esta coluna é a chave primária do `sales_flat_order_item` tabela
   * `Sammy Customer`O pedido da criou duas linhas nesta tabela porque o pedido dela continha dois produtos distintos
* `name` - Esta coluna é o nome do produto
* `product_id` - Esta coluna é o identificador exclusivo do produto a que esta linha se refere
   * A primeira linha acima tem `product_id` = 205 porque `Throwback Bellbottoms` ter um `entity_id` de 2005 sobre a `catalog_product_entity` tabela
* `order_id` - Esta coluna é o `entity_id` da ordem que contém esses itens de ordem específicos
   * Ambas as linhas acima têm `order_id` = 227 porque ambos fazem parte da ordem colocada por `Sammy Customer`, que `entity_id` = 227 no `sales_flat_order` tabela
* `qty_ordered` - Esta coluna é o número de unidades do produto incluídas nesta ordem específica
   * `Sammy Customer`A ordem do contém 2 pares de `Throwback Bellbottoms`
* `price` - Esta coluna é o preço de uma única unidade do item de ordem
   * O `subtotal` from `Sammy Customer`na ordem de `sales_flat_order` tabela era 94,85, que é a soma de 2 pares de `Throwback Bellbottoms` a US$ 39,95 cada e 1 `V-Neck T-Shirt` a US$ 14,95.
