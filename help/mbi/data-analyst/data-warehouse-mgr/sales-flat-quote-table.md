---
title: Tabela de cotações
description: Saiba como trabalhar com a tabela de cotações.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Tabela de Cotações

A variável `quote` tabela (`sales_flat_quote` em M1) contém registros em cada carrinho de compras criado em sua loja, independentemente de terem sido abandonados ou convertidos em uma compra. Cada linha representa um carrinho. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias.

>[!NOTE]
>
>A análise de carrinhos históricos e abandonados só é possível se você não excluir registros da `quote` tabela. Ao excluir registros, você só poderá ver os carrinhos que ainda não foram removidos do banco de dados.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_currency_code` | Moeda para todos os valores capturados em `base_*` campos (ou seja, `base_grand_total`, `base_subtotal`e assim por diante). Normalmente, isso reflete a moeda padrão da loja de Comércio |
| `base_grand_total` | Preço final cotado para o cliente do carrinho, depois que todos os impostos, frete e descontos são aplicados. Embora o cálculo preciso seja personalizável, em geral, a `base_grand_total` é calculado como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de mercadoria de todos os itens incluídos no carrinho. Impostos, frete, descontos e assim por diante não estão incluídos |
| `created_at` | Carimbo de data e hora de criação do carrinho, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatórios no [!DNL MBI] que difere do fuso horário do seu banco de dados |
| `customer_email` | Endereço de email do cliente que criou o carrinho |
| `customer_id` | `Foreign key` associado à `customer_entity` tabela, se o cliente estiver registrado. Associar-se a `customer_entity.entity_id` para determinar os atributos do cliente associados ao usuário que criou o carrinho. Se o carrinho foi criado por meio do check-out do convidado, esse campo é `NULL` |
| `entity_id` PK) | Identificador exclusivo da tabela e geralmente usado em associações com outras tabelas na instância do Commerce |
| `is_active` | Campo booleano que retorna &quot;1&quot; se o carrinho foi criado por um cliente e ainda não foi convertido em um pedido. Retorna &quot;0&quot; para carrinhos convertidos ou carrinhos criados pelo administrador |
| `items_qty` | Soma da quantidade total de todos os itens incluídos no carrinho |
| `reserved_order_id` | `Foreign key` associado à `sales_order` tabela. Associar-se a `sales_order.increment_id` para determinar os detalhes do pedido associados ao carrinho convertido. Para carrinhos que não estão associados a um pedido convertido, a variável `reserved_order_id` permanece `NULL` |
| `store_id` | `Foreign key` associado à `store` tabela. Associar-se a `store`.`store_id` para determinar qual exibição de loja do Commerce está associada ao carrinho |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order date` | Carimbo de data e hora que reflete a data de criação da ordem para carrinhos convertidos. Calculado por associação `quote.reserved_order_id` para `sales_order.increment_id` e o retorno do `sales_order.created_at` campo |
| `Seconds between cart creation and order` | Tempo decorrido entre a criação do carrinho e a criação do pedido. Calculado por subtração `created_at` de `Order date`, retornado como um número inteiro de segundos |
| `Seconds since cart creation` | Tempo decorrido entre a data de criação do carrinho e agora. Calculado por subtração `created_at` no carimbo de data e hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos. Usado mais frequentemente para identificar a idade de um carrinho |
| `Store name` | O nome da loja de Commerce associada a esta ordem. Calculado por associação `quote.store_id` para `store.store_id` e o retorno do `name` campo |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of abandoned carts` | A contagem de carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtros:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho além do qual um carrinho é considerado abandonado |
| `Avg time to cart conversion` | O tempo médio entre a criação do carrinho e a criação da ordem para carrinhos convertidos | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | A soma da receita potencial total do carrinho abandonado, em que a receita é definida como a `base_grand_total` campo | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtros:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho além do qual um carrinho é considerado abandonado |

{style="table-layout:auto"}

## Caminhos de Junção de Chave Estrangeira

`customer_entity`

* Associar-se a `customer_entity` tabela para criar novas colunas no nível do cliente associadas ao cliente que criou o carrinho.
   * Caminho: `quote.customer_id` (muitos) => `customer_entity.entity_id` (um)

`sales_order`

* Associar-se a `sales_order` tabela para criar colunas que retornam detalhes da ordem associados ao carrinho convertido.
   * Caminho:`quote.reserved_order_id` (muitos) => `sales_order.increment_id` (um)

`store`

* Associar-se a `store` tabela para criar colunas que retornam detalhes relacionados à loja do Commerce associada ao carrinho.
   * Caminho: `quote.store_id` (muitos) => `store.store_id` (um)
