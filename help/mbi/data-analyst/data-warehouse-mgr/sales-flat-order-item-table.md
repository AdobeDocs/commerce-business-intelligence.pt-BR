---
title: tabela sales_order_item
description: Saiba como trabalhar com a tabela sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# `sales_order_item` Tabela

O `sales_order_item` tabela (`sales_flat_order_item` no M1 1) contém registros de todos os produtos que foram comprados em um pedido. Cada linha representa uma `sku` incluído em um pedido. A quantidade de unidades que foram compradas para um `sku` é mais frequentemente representada pela variável `qty_ordered` campo.

## Tipos de produto

O `sales_order_item` captura detalhes em todos [tipos de produtos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) que foram comprados. Uma prática comum no Commerce é oferecer produtos configuráveis, ou seja, um produto que pode ser personalizado de acordo com o tamanho, a cor e outros atributos do produto. Embora um produto configurável tenha seu próprio `sku`, pode se referir a vários produtos simples, onde cada produto simples representa uma configuração de produto exclusiva. Consulte [configuração de produtos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obter mais informações.

Por exemplo, considere um produto configurável, como uma t-shirt. Quando um cliente faz o check-out, ele seleciona opções para alterar a cor e o tamanho. Se o cliente selecionar uma cor de `blue`e um tamanho de `small`, acabam comprando um produto simples como `t-shirt-blue-small` que se refere ao produto principal de `t-shirt`.

Quando um produto configurável é incluído em um pedido, duas linhas são geradas na variável `sales_order_item` tabela: um para o [simples](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`e um para o [configurável](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) pai. Esses dois registros no `sales_order_item` tabela pode ser relacionada entre si por meio da seguinte associação:

* (simples) `sales_order_item.parent_item_id` => (configurável) `sales_order_item.item_id`

Por conseguinte, é possível apresentar relatórios sobre as vendas de produtos quer ao nível simples, quer ao nível configurável. Por padrão, todos os `order-item-level` métricas em [!DNL MBI] estão configuradas para excluir os produtos simples, e *only* sobre as versões configuráveis. Isso é feito por meio da `Ordered products we count` conjunto de filtros, que filtra na condição em que `parent_item_id` é `NULL`.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|----|----|
| `base_price` | Preço de uma unidade individual de um produto no momento da venda após [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes de qualquer imposto, frete ou desconto no carrinho ser aplicado, representado na moeda base da loja |
| `created_at` | Carimbo de data e hora da criação do item do pedido, geralmente armazenado localmente em UTC. Dependendo da sua configuração em [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatório no [!DNL MBI] que difere do fuso horário do banco de dados |
| `item_id` (PK) | Identificador exclusivo para a tabela |
| `name` | Nome do texto do item de ordem |
| `order_id` | `Foreign key` associada à `sales_order` tabela. Associar-se a `sales_order.entity_id` para determinar os atributos da ordem associados ao item da ordem |
| `parent_item_id` | `Foreign key` que relaciona um produto simples ao seu pacote principal ou produto configurável. Associar-se a `sales_order_item.item_id` para determinar os atributos de produto pai associados ao produto simples. Para itens de pedido pai (ou seja, tipos de produto configuráveis ou agrupados), a variável `parent_item_id` será `NULL` |
| `product_id` | `Foreign key` associada à `catalog_product_entity` tabela. Associar-se a `catalog_product_entity.entity_id` para determinar os atributos de produto associados ao item do pedido |
| `product_type` | Tipo de produto vendido. Potencial [tipos de produtos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluem: simples, configurável, agrupada, virtual, pacote e baixável |
| `qty_ordered` | Quantidade de unidades incluídas no carrinho para o item de ordem específico no momento da venda |
| `sku` | Identificador exclusivo para o item de pedido que foi comprado |
| `store_id` | `Foreign key` associada à `store` tabela. Associar-se a `store.store_id` para determinar qual exibição da loja de comércio associada ao item de pedido |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's email` | Endereço de email do cliente que faz o pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `customer_email` campo |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por este cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `Customer's lifetime number of orders` campo |
| `Customer's lifetime revenue` | Soma total da receita para todos os pedidos feitos por este cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `Customer's lifetime revenue` campo |
| `Customer's order number` | Classificação da ordem sequencial para o pedido deste cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `Customer's order number` campo |
| `Order item total value (quantity * price)` | Valor total de um item de ordem no momento da venda após [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicadas e antes da aplicação de quaisquer impostos, frete ou descontos no carrinho. Calculado multiplicando o `qty_ordered` pela `base_price` |
| `Order's coupon_code` | Cupom aplicado ao pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `coupon_code` campo |
| `Order's increment_id` | Identificador exclusivo do pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `increment_id` campo |
| `Order's status` | Status do pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e retornar `status` campo |
| `Store name` | Nome do armazenamento do Commerce associado ao item do pedido. Calculado por associação `sales_order_item.store_id` para `store.store_id` e retornar `name` campo |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Products ordered` | A quantidade total de produtos incluídos em carrinhos no momento da venda | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | O valor total dos produtos incluídos nos carrinhos no momento da venda após as regras de preço do catálogo, descontos por níveis e preços especiais são aplicados e antes que quaisquer impostos, frete ou descontos no carrinho sejam aplicados | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` Caminhos de junção

`catalog_product_entity`

* Associar-se a `catalog_product_entity` tabela para criar novas colunas que retornam atributos de produto associados ao item do pedido.
   * Caminho: `sales_order_item.product_id` (muitos) => `catalog_product_entity.entity_id` (1)

`sales_order`

* Associar-se a `sales_order` tabela para criar novas colunas de nível de ordem associadas ao item de ordem.
   * Caminho: `sales_order_item.order_id` (muitos) => `sales_order.entity_id` (1)

`sales_order_item`

* Associar-se a `sales_order_item` para criar novas colunas que associem detalhes do SKU pai configurável ou do pacote ao produto simples. Observe que será necessário [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para obter assistência na configuração desses cálculos, se estiver criando no gerenciador de Datas Warehouse.
   * Caminho: `sales_order_item.parent_item_id` (muitos) => `sales_order_item.item_id` (1)

`store`

* Associar-se a `store` tabela para criar novas colunas que retornam detalhes relacionados à loja de comércio associada ao item de pedido.
   * Caminho: `sales_order_item.store_id` (muitos) => `store.store_id` (1)
