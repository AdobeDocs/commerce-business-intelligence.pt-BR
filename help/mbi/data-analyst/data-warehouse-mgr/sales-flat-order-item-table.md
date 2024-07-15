---
title: tabela sales_order_item
description: Saiba como trabalhar com a tabela sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Tabela `sales_order_item`

A tabela `sales_order_item` (`sales_flat_order_item` em M1) contém registros de todos os produtos que foram comprados em um pedido. Cada linha representa um `sku` exclusivo incluído em uma ordem. A quantidade de unidades que foram compradas por um `sku` específico é representada com mais frequência pelo campo `qty_ordered`.

## Tipos de produto

O `sales_order_item` captura detalhes sobre todos os [tipos de produtos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) que foram comprados. Uma prática comum no [!DNL Adobe Commerce] é oferecer produtos configuráveis ou, em outras palavras, um produto que pode ser personalizado de acordo com o tamanho, a cor e outros atributos do produto. Embora um produto configurável tenha seu próprio `sku`, ele pode estar relacionado a vários produtos simples, onde cada produto simples representa uma configuração de produto exclusiva. Consulte [configurando produtos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obter mais informações.

Por exemplo, considere um produto configurável, como uma camiseta. Quando um cliente faz o check-out, ele seleciona opções para alterar a cor e o tamanho. Se o cliente selecionar uma cor de `blue` e um tamanho de `small`, ele acabará comprando um produto simples como `t-shirt-blue-small`, que se relaciona ao produto principal de `t-shirt`.

Quando um produto configurável é incluído em um pedido, duas linhas são geradas na tabela `sales_order_item`: uma para o pai [simples](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` e outra para o pai [configurável](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html). Esses dois registros na tabela `sales_order_item` podem ser relacionados entre si através da seguinte associação:

* (simples) `sales_order_item.parent_item_id` => (configurável) `sales_order_item.item_id`

Portanto, é possível relatar as vendas de produtos no nível simples ou no nível configurável. Por padrão, todas as métricas `order-item-level` padrão em [!DNL Commerce Intelligence] são configuradas para excluir os produtos simples, e *somente* relata as versões configuráveis. Isso é feito por meio do conjunto de filtros `Ordered products we count`, que filtra a condição em que `parent_item_id` é `NULL`.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|----|----|
| `base_price` | Preço de uma unidade individual de um produto no momento da venda após a aplicação de [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) e antes da aplicação de impostos, frete ou descontos de carrinho. Isso é representado na moeda base do armazenamento. |
| `created_at` | Carimbo de data e hora de criação do item do pedido, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data/hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que seja diferente do fuso horário do banco de dados. |
| `item_id` (CP) | Identificador exclusivo da tabela. |
| `name` | Nome do texto do item do pedido. |
| `order_id` | `Foreign key` associado à tabela `sales_order`. Associe-se a `sales_order.entity_id` para determinar os atributos do pedido associados ao item do pedido. |
| `parent_item_id` | `Foreign key` que relaciona um produto simples ao seu pacote pai ou produto configurável. Associe-se a `sales_order_item.item_id` para determinar os atributos do produto principal associados ao produto simples. Para itens de pedido principal (isto é, tipos de produto agrupados ou configuráveis), o `parent_item_id` é `NULL`. |
| `product_id` | `Foreign key` associado à tabela `catalog_product_entity`. Associe-se a `catalog_product_entity.entity_id` para determinar os atributos de produto associados ao item do pedido. |
| `product_type` | Tipo de produto vendido. Os [tipos de produtos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) possíveis incluem: simples, configurável, agrupado, virtual, pacote e baixável. |
| `qty_ordered` | Quantidade de unidades incluídas no carrinho para o item de pedido específico no momento da venda. |
| `sku` | Identificador exclusivo do item do pedido que foi comprado. |
| `store_id` | `Foreign key` associado à tabela `store`. Ingresse em `store.store_id` para determinar qual exibição de armazenamento do Commerce está associada ao item do pedido. |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's email` | Endereço de email do cliente que faz o pedido. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `customer_email`. |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por esse cliente. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `Customer's lifetime number of orders`. |
| `Customer's lifetime revenue` | Soma total da receita de todos os pedidos feitos por esse cliente. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `Customer's lifetime revenue`. |
| `Customer's order number` | Classificação de ordem sequencial para a ordem deste cliente. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `Customer's order number`. |
| `Order item total value (quantity * price)` | Valor total de um item do pedido no momento da venda após a aplicação de [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) e antes da aplicação de impostos, descontos de remessa ou carrinho. Calculado pela multiplicação de `qty_ordered` por `base_price`. |
| `Order's coupon_code` | Cupom aplicado ao pedido. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `coupon_code`. |
| `Order's increment_id` | Identificador exclusivo do pedido. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `increment_id`. |
| `Order's status` | Status do pedido. Calculado ao ingressar de `sales_order_item.order_id` em `sales_order.entity_id` e retornar o campo `status`. |
| `Store name` | Nome da loja da Commerce associada ao item do pedido. Calculado ao ingressar de `sales_order_item.store_id` em `store.store_id` e retornar o campo `name`. |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Products ordered` | A quantidade total de produtos incluídos em carrinhos no momento da venda | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valor total dos produtos incluídos em carrinhos no momento da venda após a aplicação das regras de preço de catálogo, descontos em camadas e preços especiais e antes da aplicação de impostos, frete ou descontos de carrinho | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Caminhos de associação

`catalog_product_entity`

* Associe-se à tabela `catalog_product_entity` para criar colunas que retornam atributos de produto associados ao item do pedido.
   * Caminho: `sales_order_item.product_id` (muitos) => `catalog_product_entity.entity_id` (um)

`sales_order`

* Associe-se à tabela `sales_order` para criar novas colunas no nível do pedido associadas ao item do pedido.
   * Caminho: `sales_order_item.order_id` (muitos) => `sales_order.entity_id` (um)

`sales_order_item`

* Ingresse em `sales_order_item` para criar colunas que associem detalhes da SKU pai configurável ou pacote ao produto simples. [Contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obter assistência na configuração desses cálculos, caso esteja criando no gerenciador de Datas Warehouse.
   * Caminho: `sales_order_item.parent_item_id` (muitos) => `sales_order_item.item_id` (um)

`store`

* Associe-se à tabela `store` para criar colunas que retornam detalhes relacionados ao armazenamento da Commerce associado ao item do pedido.
   * Caminho: `sales_order_item.store_id` (muitos) => `store.store_id` (um)
