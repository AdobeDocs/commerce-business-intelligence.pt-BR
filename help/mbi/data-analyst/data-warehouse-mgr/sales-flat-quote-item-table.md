---
title: tabela quote_item
description: Saiba como trabalhar com a tabela quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# Tabela quote_item

O `quote_item` tabela (`sales_flat_quote_item` on [!DNL Magento] 1) contém registros de todos os itens adicionados a um carrinho de compras, independentemente de o carrinho ter sido abandonado ou convertido em uma compra. Cada linha representa um item do carrinho. Devido ao tamanho potencial desta tabela, recomendamos que você exclua registros periodicamente se determinados critérios forem atendidos, como se houvesse algum carrinho não convertido com mais de 60 dias.

>[!NOTE]
>
>A análise de carrinhos abandonados históricos só será possível se você não excluir registros do `quote` e `quote_item` tabela. Se você excluir registros, só poderá ver os carrinhos ainda não removidos do banco de dados.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_price` | Preço de uma unidade individual de um produto no momento em que o item foi adicionado ao carrinho, após [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicados e antes de qualquer imposto, frete ou desconto no carrinho ser aplicado, representado na moeda base da loja |
| `created_at` | Carimbo de data e hora da criação do item do carrinho, geralmente armazenado localmente em UTC. Dependendo da sua configuração em [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatório no [!DNL MBI] que difere do fuso horário do banco de dados |
| `item_id` (PK) | Identificador exclusivo para a tabela |
| `name` | Nome do texto do item de ordem |
| `parent_item_id` | `Foreign key` que relaciona um produto simples ao seu pacote principal ou produto configurável. Associar-se a `quote_item.item_id` para determinar os atributos de produto pai associados ao produto simples. Para itens do carrinho pai (ou seja, tipos de produto configuráveis ou de pacote), a variável `parent_item_id` será `NULL` |
| `product_id` | `Foreign key` associada à `catalog_product_entity` tabela. Associar-se a `catalog_product_entity.entity_id` para determinar os atributos de produto associados ao item do pedido |
| `product_type` | Tipo de produto que foi adicionado ao carrinho. Potencial [tipos de produtos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluem: simples, configurável, agrupada, virtual, pacote e baixável |
| `qty` | Quantidade de unidades incluídas no carrinho para o item específico do carrinho |
| `quote_id` | `Foreign key` associada à `quote` tabela. Associar-se a `quote.entity_id` para determinar os atributos do carrinho associados ao item do carrinho |
| `sku` | Identificador exclusivo para o item do carrinho |
| `store_id` | Chave externa associada à `store` tabela. Associar-se a `store.store_id` para determinar qual visualização da loja de comércio está associada ao item do carrinho |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Cart creation date` | Carimbo de data e hora associado à data de criação do carrinho. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e retornar `created_at` timestamp |
| `Cart is active? (1/0)` | Campo booleano que retorna &quot;1&quot; se o carrinho foi criado por um cliente e ainda não foi convertido em um pedido. Retorna &quot;0&quot; para carrinhos convertidos ou carrinhos criados pelo administrador. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e retornar `is_active` campo |
| `Cart item total value (qty * base_price)` | Valor total de um item no momento em que o item foi adicionado ao carrinho, após [regras de preço de catálogo, descontos em camadas e preços especiais](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) são aplicadas e antes da aplicação de quaisquer impostos, frete ou descontos no carrinho. Calculado multiplicando o `qty` pela `base_price` |
| `Seconds since cart creation` | Tempo decorrido entre a data de criação do carrinho e agora. Calculado por associação `quote_item.quote_id` para `quote.entity_id` e retornar `Seconds since cart creation` campo |
| `Store name` | Nome do armazenamento do Commerce associado ao item do pedido. Calculado por associação `sales_order_item.store_id` para `store.store_id` e retornar `name` campo |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of abandoned cart items` | Quantidade total de itens adicionados aos carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |
| `Abandoned cart item value` | Soma da receita total associada aos carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |

{style=&quot;table-layout:auto&quot;}

## Caminhos de associação de chave externa

`catalog_product_entity`

* Associar-se a `catalog_product_entity` tabela para criar novas colunas que retornam atributos de produto associados ao item do carrinho.
   * Caminho: `quote_item.product_id` (muitos) => `catalog_product_entity.entity_id` (1)

`quote`

* Associar-se a `quote` tabela para criar novas colunas no nível do carrinho associadas ao item do carrinho.
   * Caminho: `quote_item.quote_id` (muitos) => `quote.entity_id` (1)

`quote_item`

* Associar-se a `quote_item` para criar novas colunas que associem detalhes do SKU pai configurável ou do pacote ao produto simples. Observe que será necessário [entrar em contato com o suporte](../../guide-overview.md) para obter assistência na configuração desses cálculos, se estiver criando no gerenciador de Datas Warehouse.
   * Caminho: `quote_item.parent_item_id` (muitos) => `quote_item.item_id` (1)

`store`

* Associar-se a `store` tabela para criar novas colunas que retornam detalhes relacionados à loja de comércio associada ao item do carrinho.
   * Caminho: `quote_item.store_id` (muitos) => `store.store_id` (1)
