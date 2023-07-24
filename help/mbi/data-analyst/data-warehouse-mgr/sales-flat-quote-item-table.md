---
title: tabela quote_item
description: Saiba como trabalhar com a tabela quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Tabela quote_item

A variável `quote_item` tabela (`sales_flat_quote_item` em M1) contém registros em cada item adicionado a um carrinho de compras, independentemente de o carrinho ter sido abandonado ou convertido em uma compra. Cada linha representa um item do carrinho. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias.

>[!NOTE]
>
>A análise de carrinhos históricos e abandonados só é possível se você não excluir registros da `quote` e `quote_item` tabela. Ao excluir registros, você só poderá ver os carrinhos que ainda não foram removidos do banco de dados.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_price` | Preço de uma unidade individual de um produto no momento em que o item foi adicionado ao carrinho, após [regras de preço de catálogo, descontos hierárquicos e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes da aplicação de impostos, descontos de remessa ou carrinho. Isso é representado na moeda base do armazenamento. |
| `created_at` | Carimbo de data e hora de criação do item do carrinho, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data e hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que difere do fuso horário do seu banco de dados |
| `item_id` PK) | Identificador exclusivo da tabela |
| `name` | Nome do texto do item do pedido |
| `parent_item_id` | `Foreign key` que relaciona um produto simples ao seu pacote principal ou produto configurável. Associar-se a `quote_item.item_id` para determinar os atributos do produto principal associados ao produto simples. Para itens do carrinho principal (ou seja, tipos de produto agrupados ou configuráveis), a variável `parent_item_id` é `NULL` |
| `product_id` | `Foreign key` associado à `catalog_product_entity` tabela. Associar-se a `catalog_product_entity.entity_id` para determinar os atributos do produto associados ao item do pedido |
| `product_type` | Tipo de produto adicionado ao carrinho. Potencial [tipos de produto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluem: simples, configurável, agrupado, virtual, pacote e disponível para download |
| `qty` | Quantidade de unidades incluídas no carrinho para o item de carrinho específico |
| `quote_id` | `Foreign key` associado à `quote` tabela. Associar-se a `quote.entity_id` para determinar os atributos do carrinho associados ao item do carrinho |
| `sku` | Identificador exclusivo do item do carrinho |
| `store_id` | Chave estrangeira associada à `store` tabela. Associar-se a `store.store_id` para determinar qual exibição de loja do Commerce está associada ao item do carrinho |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Cart creation date` | Carimbo de data e hora associado à data de criação do carrinho. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e o retorno do `created_at` carimbo de data e hora |
| `Cart is active? (1/0)` | Campo booleano que retorna &quot;1&quot; se o carrinho foi criado por um cliente e ainda não foi convertido em um pedido. Retorna &quot;0&quot; para carrinhos convertidos ou carrinhos criados pelo administrador. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e o retorno do `is_active` campo |
| `Cart item total value (qty * base_price)` | Valor total de um item no momento em que ele foi adicionado ao carrinho, após [regras de preço de catálogo, descontos hierárquicos e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes da aplicação de impostos, descontos de remessa ou carrinho. Calculado multiplicando o `qty` pela `base_price` |
| `Seconds since cart creation` | Tempo decorrido entre a data de criação do carrinho e agora. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e o retorno do `Seconds since cart creation` campo |
| `Store name` | Nome da loja de Commerce associada ao item do pedido. Calculado por associação `sales_order_item.store_id` para `store.store_id` e o retorno do `name` campo |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of abandoned cart items` | Quantidade total de itens adicionados aos carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho além do qual um carrinho é considerado abandonado |
| `Abandoned cart item value` | Soma da receita total associada aos carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho além do qual um carrinho é considerado abandonado |

{style="table-layout:auto"}

## Caminhos de Junção de Chave Estrangeira

`catalog_product_entity`

* Associar-se a `catalog_product_entity` tabela para criar colunas que retornam atributos de produto associados ao item do carrinho.
   * Caminho: `quote_item.product_id` (muitos) => `catalog_product_entity.entity_id` (um)

`quote`

* Associar-se a `quote` tabela para criar novas colunas no nível do carrinho associadas ao item do carrinho.
   * Caminho: `quote_item.quote_id` (muitos) => `quote.entity_id` (um)

`quote_item`

* Associar-se a `quote_item` para criar colunas que associam detalhes do SKU pai configurável ou pacote ao produto simples. [Entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obter assistência na configuração desses cálculos, caso esteja criando no gerenciador de Datas Warehouse.
   * Caminho: `quote_item.parent_item_id` (muitos) => `quote_item.item_id` (um)

`store`

* Associar-se a `store` tabela para criar colunas que retornam detalhes relacionados à loja do Commerce associada ao item do carrinho.
   * Caminho: `quote_item.store_id` (muitos) => `store.store_id` (um)
