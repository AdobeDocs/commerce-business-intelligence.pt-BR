---
title: tabela de cotações
description: Saiba como trabalhar com a tabela de aspas.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# tabela de cotações

O `quote` tabela (`sales_flat_quote` em M1) contém registros em cada carrinho de compras criado em sua loja, quer tenham sido abandonados ou convertidos em uma compra. Cada linha representa um carrinho. Devido ao tamanho potencial desta tabela, recomendamos que você exclua registros periodicamente se determinados critérios forem atendidos, como se houvesse algum carrinho não convertido com mais de 60 dias.

>[!NOTE]
>
>A análise de carrinhos abandonados históricos só será possível se você não excluir registros do `quote` tabela. Se você excluir registros, só poderá ver os carrinhos ainda não removidos do banco de dados.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_currency_code` | Moeda para todos os valores capturados em `base_*` campos (que `base_grand_total`, `base_subtotal`e assim por diante). Normalmente, isso reflete a moeda padrão da loja de Comércio |
| `base_grand_total` | Preço final cotado para o cliente para o carrinho, após a aplicação de todos os impostos, frete e descontos. Embora o cálculo preciso seja personalizável, em geral a variável `base_grand_total` é calculada como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto da mercadoria de todos os itens incluídos no carrinho. Impostos, remessa, descontos e assim por diante não estão incluídos |
| `created_at` | Carimbo de data e hora da criação, geralmente armazenado localmente em UTC. Dependendo da sua configuração em [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatório no [!DNL MBI] que difere do fuso horário do banco de dados |
| `customer_email` | Endereço de email do cliente que criou o carrinho |
| `customer_id` | `Foreign key` associada à `customer_entity` , se o cliente estiver registrado. Associar-se a `customer_entity.entity_id` para determinar os atributos do cliente associados ao usuário que criou o carrinho. Se o carrinho foi criado por meio do check-out de convidado, este campo será `NULL` |
| `entity_id` (PK) | Identificador exclusivo para a tabela e normalmente usado em associações a outras tabelas na instância do Commerce |
| `is_active` | Campo booleano que retorna &quot;1&quot; se o carrinho foi criado por um cliente e ainda não foi convertido em um pedido. Retorna &quot;0&quot; para carrinhos convertidos ou carrinhos criados por meio do administrador |
| `items_qty` | Soma da quantidade total de todos os itens incluídos no carrinho |
| `reserved_order_id` | `Foreign key` associada à `sales_order` tabela. Associar-se a `sales_order.increment_id` para determinar os detalhes do pedido associados ao carrinho convertido. Para carrinhos não associados a uma ordem convertida, a variável `reserved_order_id` permanecerá `NULL` |
| `store_id` | `Foreign key` associada à `store` tabela. Associar-se a `store`.`store_id` para determinar qual visualização da loja de comércio está associada ao carrinho |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order date` | Carimbo de data e hora refletindo a data de criação da ordem dos carrinhos convertidos. Calculado por associação `quote.reserved_order_id` para `sales_order.increment_id` e retornar `sales_order.created_at` campo |
| `Seconds between cart creation and order` | Tempo decorrido entre a criação do carrinho e a criação do pedido. Calculado por subtração `created_at` from `Order date`, retornado como um número inteiro de segundos |
| `Seconds since cart creation` | Tempo decorrido entre a data de criação do carrinho e agora. Calculado por subtração `created_at` do carimbo de data e hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos. Mais usado para identificar a idade do carrinho |
| `Store name` | O nome da loja Comércio associado a este pedido. Calculado por associação `quote.store_id` para `store.store_id` e retornar `name` campo |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of abandoned carts` | A contagem de carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtros:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |
| `Avg time to cart conversion` | O tempo médio entre a criação do carrinho e a criação de pedidos para carrinhos convertidos | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | A soma do total de receita potencial do carrinho abandonado, em que a receita é definida como `base_grand_total` campo | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtros:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |

{style=&quot;table-layout:auto&quot;}

## Caminhos de associação de chave externa

`customer_entity`

* Associar-se a `customer_entity` para criar novas colunas em nível de cliente associadas ao cliente que criou o carrinho.
   * Caminho: `quote.customer_id` (muitos) => `customer_entity.entity_id` (1)

`sales_order`

* Associar-se a `sales_order` tabela para criar novas colunas que retornam detalhes do pedido associados a um carrinho convertido.
   * Caminho:`quote.reserved_order_id` (muitos) => `sales_order.increment_id` (1)

`store`

* Associar-se a `store` tabela para criar novas colunas que retornam detalhes relacionados à loja de comércio associada ao carrinho.
   * Caminho: `quote.store_id` (muitos) => `store.store_id` (1)
