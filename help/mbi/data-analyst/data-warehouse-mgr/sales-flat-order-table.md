---
title: tabela sales_order
description: Saiba como trabalhar com a tabela sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---

# `sales_order` Tabela

O `sales_order` tabela (`sales_flat_order` em M1) é onde cada pedido é capturado. Na maioria dos casos, cada linha representa um pedido exclusivo, embora existam algumas implementações personalizadas do Commerce que resultam na divisão de um pedido em linhas separadas.

Esta tabela inclui todas as ordens de clientes, independentemente de essa ordem ter sido processada por meio de check-out de convidado. Se a sua loja aceitar o check-out de convidado, você poderá encontrar mais informações sobre isso [caso de uso](../data-warehouse-mgr/guest-orders.md).

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_currency_code` | Moeda para todos os valores capturados em `base_*` campos (que `base_grand_total`, `base_subtotal`e assim por diante). Normalmente, isso reflete a moeda padrão da loja de Comércio |
| `base_discount_amount` | Valor do desconto aplicado à ordem |
| `base_grand_total` | Preço final pago pelo cliente no pedido, após a aplicação de todos os impostos, frete e descontos. Embora o cálculo preciso seja personalizável, em geral a variável `base_grand_total` é calculada como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto da mercadoria de todos os itens incluídos na ordem. Impostos, remessa, descontos e assim por diante não estão incluídos |
| `base_shipping_amount` | Valor de frete aplicado ao pedido |
| `base_tax_amount` | Valor de imposto aplicado à ordem |
| `billing_address_id` | `Foreign key` associada à `sales_order_address` tabela. Associar-se a `sales_order_address.entity_id` para determinar os detalhes do endereço de faturamento associados ao pedido |
| `coupon_code` | Cupom aplicado ao pedido. Se nenhum cupom for aplicado, esse campo será `NULL` |
| `created_at` | Carimbo de data e hora da criação do pedido, geralmente armazenado localmente em UTC. Dependendo da sua configuração em [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatório no [!DNL MBI] que difere do fuso horário do banco de dados |
| `customer_email` | Endereço de email do cliente que faz o pedido. Isso será preenchido em todas as situações, incluindo pedidos processados por meio de check-out de convidado |
| `customer_group_id` | Chave externa associada à `customer_group` tabela. Associar-se a `customer_group.customer_group_id` para determinar o grupo de clientes associado ao pedido |
| `customer_id` | `Foreign key` associada à `customer_entity` , se o cliente estiver registrado. Associar-se a `customer_entity.entity_id` para determinar os atributos do cliente associados ao pedido. Se o pedido foi colocado por meio do check-out do convidado, este campo será `NULL` |
| `entity_id` (PK) | Identificador exclusivo para a tabela e normalmente usado em associações a outras tabelas na instância do Commerce |
| `increment_id` | Identificador exclusivo de um pedido, geralmente chamado de `order_id` no Adobe Commerce. O `increment_id` é usada com mais frequência para associações a fontes externas, como [!DNL Google Ecommerce] |
| `shipping_address_id` | Chave externa associada à `sales_order_address` tabela. Associar-se a `sales_order_address.entity_id` para determinar os detalhes do endereço de entrega associado ao pedido |
| `status` | Status do pedido. Pode retornar valores como &quot;concluído&quot;, &quot;processamento&quot;, &quot;cancelado&quot;, &quot;reembolsado&quot;, bem como quaisquer status personalizados implementados na instância do Commerce. Sujeito a alterações à medida que o pedido é processado |
| `store_id` | `Foreign key` associada à `store` tabela. Associar-se a `store`.`store_id` para determinar qual visualização da loja de comércio está associada ao pedido |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Billing address city` | Cidade de cobrança do pedido. Calculado por associação `sales_order`.`billing_address_id` para `sales_order_address`.`entity_id` e retornar `city` campo |
| `Billing address country` | Código do país de cobrança do pedido. Calculado por associação `sales_order`.`billing_address_id` para `sales_order_address`.`entity_id` e retornar `country_id` |
| `Billing address region` | Região de faturamento (geralmente estado ou província) do pedido. Calculado por associação `sales_order`.`billing_address_id` para `sales_order_address`.`entity_id` e retornar `region` campo |
| `Customer's first order date` | Carimbo de data e hora do primeiro pedido feito por este cliente. Geralmente considerada a &quot;data de aquisição&quot; para um cliente. Calculado retornando o mínimo `sales_order`.`created_at` valor para cada cliente exclusivo |
| `Customer's first order's billing region` | Região de faturamento da aquisição para o cliente que fez o pedido. Calculado por retorno da variável `Billing address region` associado ao primeiro pedido do cliente |
| `Customer's first order's coupon_code` | Código do cupom de aquisição para o cliente que fez esse pedido. Calculado por retorno da variável `coupon_code` associado ao primeiro pedido do cliente |
| `Customer's group code` | Nome do grupo do cliente que fez este pedido. Calculado por associação `sales_order`.`customer_group_id` para `customer_group`.`customer_group_id` e retornar `customer_group_code` campo |
| `Customer's lifetime number of coupons` | Quantidade total de cupons aplicados a todos os pedidos feitos por este cliente. Calculado pela contagem do número de pedidos em que a variável `coupon_code` não é `NULL` para cada cliente exclusivo |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por este cliente. Calculado pela contagem do número de linhas no `sales_order` tabela para cada cliente único |
| `Customer's lifetime revenue` | Soma total da receita para todos os pedidos feitos por este cliente. Calculado pela soma do `base_grand_total` campo para todas as ordens de cada cliente único |
| `Customer's order number` | Classificação da ordem sequencial para o pedido deste cliente. Calculado identificando todas as ordens colocadas por um cliente, classificando-as em ordem crescente pela `created_at` carimbo de data e hora e atribuição de um valor inteiro de incremento a cada pedido. Por exemplo, o primeiro pedido do cliente retorna uma `Customer's order number` de 1; a segunda ordem retorna um `Customer's order number` de 2; e assim por diante |
| `Customer's order number (previous-current)` | Classificação da ordem anterior do cliente concatenada com a classificação dessa ordem, separada por uma `-` caractere. Calculado por concatenação (&quot;`Customer's order number` - 1&quot;) com &quot;`-`&quot; seguido de &quot;`Customer's order number`&quot;. Por exemplo, para o pedido associado à segunda compra do cliente, essa coluna retornará um valor de `1-2`. Mais usado ao representar o tempo entre dois eventos de pedido (ou seja, no gráfico &quot;Tempo entre pedidos&quot;) |
| `Is customer's last order?` | Determina se o pedido corresponde ou não ao último pedido ou ao mais recente do cliente. Calculado por comparação da variável `Customer's order number` com `Customer's lifetime number of orders`. Quando esses dois campos são iguais para uma determinada ordem, essa coluna retorna &quot;Sim&quot;; caso contrário, retorna &quot;Não&quot; |
| `Number of items in order` | Quantidade total de itens incluídos no pedido. Calculado por associação `sales_order`.`entity_id` para `sales_order_item`.`order_id` e resumir `sales_order_item`.`qty_ordered` campo |
| `Seconds between customer's first order date and this order` | Tempo decorrido entre este pedido e o primeiro pedido do cliente. Calculado por subtração `Customer's first order date` do `created_at` para cada pedido, retornado como um número inteiro de segundos |
| `Seconds since previous order` | Tempo decorrido entre este pedido e o pedido imediatamente anterior do cliente. Calculado subtraindo a variável `created_at` para o pedido anterior da `created_at` desta ordem, retornada como um número inteiro de segundos. Por exemplo, para o registro de pedido correspondente a um terceiro pedido do cliente, essa coluna retorna o número de segundos entre o segundo pedido do cliente e o terceiro. Para o primeiro pedido do cliente, este campo retornará `NULL` |
| `Shipping address city` | Cidade de remessa do pedido. Calculado por associação `sales_order`.`shipping_address_id` para `sales_order_address`.`entity_id` e retornar `city` campo |
| `Shipping address country` | Código do país de entrega do pedido. Calculado por associação `sales_order`.`Shipping_address_id` para `sales_order_address`.`entity_id` e retornar `country_id` |
| `Shipping address region` | Região de transporte (geralmente estado ou província) para o pedido. Calculado por associação `sales_order`.`shipping_address_id` para `sales_order_address`.`entity_id` e retornar `region` campo |
| `Store name` | O nome da loja Comércio associado a este pedido. Calculado por associação `sales_order`.`store_id` para `store`.`store_id` e retornar `name` campo |

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Avg order value` | A receita média por pedido, em que a receita é definida como `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | O tempo médio entre a ordem de um cliente (n-1) e a enésima ordem, para todos os clientes e ordens | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | A soma do valor bruto da mercadoria para todas as ordens, em que GMV é definido como o subtotal, antes de serem aplicados todos os impostos e descontos | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | O tempo mediano entre a ordem de um cliente (n-1) e a enésima ordem, para todos os clientes e pedidos | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | A contagem total de pedidos feitos | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | A soma da receita para todas as ordens, onde a receita é definida como o preço final pago pelo cliente, após a aplicação de todos os impostos, descontos, frete e assim por diante | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | A soma do valor de entrega para todas as ordens | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | A soma dos impostos aplicados a todas as ordens | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | O número de clientes únicos que fizeram um pedido no intervalo de tempo de relatório especificado. Por exemplo, se o intervalo do relatório foi semanal, cada cliente que faz pelo menos um pedido em uma determinada semana será contado exatamente uma vez, independentemente de quantos pedidos foi feito nessa semana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Caminhos de junção

`customer_entity`

* Associar-se a `customer_entity` tabela para criar novas colunas em nível de cliente associadas ao cliente que fez o pedido.
   * Caminho: `sales_order.customer_id` (muitos) => `customer_entity.entity_id` (1)

`customer_group`

* Associar-se a `customer_group` tabela para criar novas colunas que retornam o nome do grupo de clientes do cliente que fez o pedido.
   * Caminho: `sales_order.customer_group_id` (muitos) => `customer_group.customer_group_id` (1)

`sales_order_address`

* Associar-se a `sales_order_address` tabela para criar novas colunas que retornam locais de faturamento e entrega associados ao pedido. Dois caminhos de junção são possíveis, dependendo se os detalhes de cobrança ou envio são necessários.
   * Caminhos:
      * Remessa: `sales_order.shipping_address_id`(muitos) => `sales_order_address.entity_id` (1)
      * Faturamento: `sales_order.billing_address_id`(muitos) => `sales_order_address.entity_id` (1)

`store`

* Associar-se a `store` tabela para criar novas colunas que retornam detalhes relacionados à loja de comércio associada ao pedido.
   * Caminho: `sales_order.store_id` (muitos) => `store.store_id` (1)
