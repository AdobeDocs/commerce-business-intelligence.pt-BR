---
title: tabela sales_order_item
description: Saiba como trabalhar com a tabela sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` Tabela

A variável `sales_order_item` tabela (`sales_flat_order_item` em M1) contém registros de todos os produtos que foram comprados em um pedido. Cada linha representa uma `sku` incluído em um pedido. A quantidade de unidades que foram compradas para um `sku` é mais frequentemente representado pela `qty_ordered` campo.

## Tipos de produto

A variável `sales_order_item` captura detalhes em todos [tipos de produto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) que foram comprados. Uma prática comum em [!DNL Adobe Commerce] é oferecer produtos configuráveis ou, em outras palavras, um produto que pode ser personalizado de acordo com o tamanho, a cor e outros atributos do produto. Embora um produto configurável tenha seu próprio `sku`Além disso, pode estar relacionado a vários produtos simples, em que cada produto simples representa uma configuração exclusiva. Consulte [configuração de produtos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obter mais informações.

Por exemplo, considere um produto configurável, como uma camiseta. Quando um cliente faz o check-out, ele seleciona opções para alterar a cor e o tamanho. Se o cliente selecionar uma cor de `blue`e um tamanho de `small`, eles acabam comprando um produto simples como `t-shirt-blue-small` que se relaciona com o produto principal de `t-shirt`.

Quando um produto configurável é incluído em um pedido, duas linhas são geradas no `sales_order_item` tabela: um para o [simples](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` e um para o [configurável](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) pai. Esses dois registros na `sales_order_item` A tabela pode ser relacionada entre si por meio da seguinte associação:

* (simples) `sales_order_item.parent_item_id` => (configurável) `sales_order_item.item_id`

Portanto, é possível relatar as vendas de produtos no nível simples ou no nível configurável. Por padrão, todos os arquivos `order-item-level` métricas no [!DNL Commerce Intelligence] são configurados para excluir os produtos simples e *somente* relatório sobre as versões configuráveis. Isso é feito por meio da `Ordered products we count` conjunto de filtros, que filtra na condição em que `parent_item_id` é `NULL`.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|----|----|
| `base_price` | Preço de uma unidade individual de um produto no momento da venda após [regras de preço de catálogo, descontos hierárquicos e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes da aplicação de impostos, descontos de remessa ou carrinho. Isso é representado na moeda base do armazenamento. |
| `created_at` | Carimbo de data e hora de criação do item do pedido, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data e hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que difere do fuso horário do banco de dados. |
| `item_id` PK) | Identificador exclusivo da tabela. |
| `name` | Nome do texto do item do pedido. |
| `order_id` | `Foreign key` associado à `sales_order` tabela. Associar-se a `sales_order.entity_id` para determinar os atributos da ordem associados ao item da ordem. |
| `parent_item_id` | `Foreign key` que relaciona um produto simples ao seu pacote principal ou produto configurável. Associar-se a `sales_order_item.item_id` para determinar os atributos do produto principal associados ao produto simples. Para itens de pedido principal (ou seja, tipos de produto agrupados ou configuráveis), a variável `parent_item_id` é `NULL`. |
| `product_id` | `Foreign key` associado à `catalog_product_entity` tabela. Associar-se a `catalog_product_entity.entity_id` para determinar os atributos do produto associados ao item do pedido. |
| `product_type` | Tipo de produto vendido. Potencial [tipos de produto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluem: simples, configurável, agrupado, virtual, pacote e baixável. |
| `qty_ordered` | Quantidade de unidades incluídas no carrinho para o item de pedido específico no momento da venda. |
| `sku` | Identificador exclusivo do item do pedido que foi comprado. |
| `store_id` | `Foreign key` associado à `store` tabela. Associar-se a `store.store_id` para determinar qual exibição de loja do Commerce está associada ao item do pedido. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's email` | Endereço de email do cliente que faz o pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `customer_email` campo. |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por esse cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `Customer's lifetime number of orders` campo. |
| `Customer's lifetime revenue` | Soma total da receita de todos os pedidos feitos por esse cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `Customer's lifetime revenue` campo. |
| `Customer's order number` | Classificação de ordem sequencial para a ordem deste cliente. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `Customer's order number` campo. |
| `Order item total value (quantity * price)` | Valor total de um item de pedido no momento da venda após [regras de preço de catálogo, descontos hierárquicos e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes da aplicação de impostos, descontos de remessa ou carrinho. Calculado multiplicando o `qty_ordered` pela `base_price`. |
| `Order's coupon_code` | Cupom aplicado ao pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `coupon_code` campo. |
| `Order's increment_id` | Identificador exclusivo do pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `increment_id` campo. |
| `Order's status` | Status do pedido. Calculado por associação `sales_order_item.order_id` para `sales_order.entity_id` e o retorno do `status` campo. |
| `Store name` | Nome da loja de Commerce associada ao item do pedido. Calculado por associação `sales_order_item.store_id` para `store.store_id` e o retorno do `name` campo. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Products ordered` | A quantidade total de produtos incluídos em carrinhos no momento da venda | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valor total dos produtos incluídos em carrinhos no momento da venda após a aplicação das regras de preço de catálogo, descontos em camadas e preços especiais e antes da aplicação de impostos, frete ou descontos de carrinho | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Unir caminhos

`catalog_product_entity`

* Associar-se a `catalog_product_entity` tabela para criar colunas que retornam atributos de produto associados ao item do pedido.
   * Caminho: `sales_order_item.product_id` (muitos) => `catalog_product_entity.entity_id` (um)

`sales_order`

* Associar-se a `sales_order` tabela para criar novas colunas no nível do pedido associadas ao item do pedido.
   * Caminho: `sales_order_item.order_id` (muitos) => `sales_order.entity_id` (um)

`sales_order_item`

* Associar-se a `sales_order_item` para criar colunas que associam detalhes do SKU pai configurável ou pacote ao produto simples. [Entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obter assistência na configuração desses cálculos, caso esteja criando no gerenciador de Datas Warehouse.
   * Caminho: `sales_order_item.parent_item_id` (muitos) => `sales_order_item.item_id` (um)

`store`

* Associar-se a `store` tabela para criar colunas que retornam detalhes relacionados à loja do Commerce associada ao item do pedido.
   * Caminho: `sales_order_item.store_id` (muitos) => `store.store_id` (um)
