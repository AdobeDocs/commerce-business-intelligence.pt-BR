---
title: tabela sales_order
description: Saiba como trabalhar com a tabela sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/zdxIx9qHzEyoCbFzh0EBv1BKJEWiShtAt33-dtkEGNo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 1200
ht-degree: 0%

---

# Tabela `sales_order`

A tabela `sales_order` (`sales_flat_order` em M1) é onde cada pedido é capturado. Normalmente, cada linha representa uma ordem única, embora existam algumas implementações personalizadas do Commerce que resultam na divisão de uma ordem em linhas separadas.

Esta tabela inclui todos os pedidos do cliente, independentemente de esse pedido ter sido processado por meio da finalização da compra do convidado. Se a loja aceitar o check-out de convidado, você poderá encontrar mais informações sobre este [caso de uso](../data-warehouse-mgr/guest-orders.md).

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_currency_code` | Moeda para todos os valores capturados nos campos `base_*` (ou seja, `base_grand_total`, `base_subtotal` e assim por diante). Normalmente, isso reflete a moeda padrão da loja da Commerce |
| `base_discount_amount` | Valor de desconto aplicado ao pedido |
| `base_grand_total` | Preço final pago pelo cliente no pedido, após a aplicação de todos os impostos, frete e descontos. Embora o cálculo preciso seja personalizável, em geral o `base_grand_total` é calculado como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de mercadoria de todos os itens incluídos no pedido. Impostos, frete, descontos e assim por diante não estão incluídos |
| `base_shipping_amount` | Valor de remessa aplicado à ordem |
| `base_tax_amount` | Valor de imposto aplicado ao pedido |
| `billing_address_id` | `Foreign key` associado à tabela `sales_order_address`. Ingressar em `sales_order_address.entity_id` para determinar os detalhes do endereço de cobrança associado ao pedido |
| `coupon_code` | Cupom aplicado à ordem. Se nenhum cupom for aplicado, este campo será `NULL` |
| `created_at` | Carimbo de data e hora de criação do pedido, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data/hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que seja diferente do fuso horário do banco de dados |
| `customer_email` | Endereço de email do cliente que faz o pedido. Isso é preenchido em todas as situações, incluindo pedidos processados por meio da finalização da compra do convidado |
| `customer_group_id` | Chave estrangeira associada à tabela `customer_group`. Ingressar em `customer_group.customer_group_id` para determinar o grupo de clientes associado ao pedido |
| `customer_id` | `Foreign key` associado à tabela `customer_entity`, se o cliente estiver registrado. Ingresse em `customer_entity.entity_id` para determinar os atributos do cliente associados ao pedido. Se o pedido foi feito através do check-out do convidado, este campo é `NULL` |
| `entity_id` (CP) | Identificador exclusivo da tabela e geralmente usado em associações com outras tabelas na instância do Commerce |
| `increment_id` | Identificador exclusivo de um pedido, geralmente chamado de `order_id` no Adobe Commerce. O `increment_id` é usado com mais frequência para junções com fontes externas, como [!DNL Google Ecommerce] |
| `shipping_address_id` | Chave estrangeira associada à tabela `sales_order_address`. Ingressar em `sales_order_address.entity_id` para determinar os detalhes do endereço de entrega associados ao pedido |
| `status` | Status do pedido. Pode retornar valores como &quot;concluído&quot;, &quot;processando&quot;, &quot;cancelado&quot;, &quot;reembolsado&quot; e qualquer status personalizado implementado na instância do Commerce. Sujeito a alterações conforme o pedido é processado |
| `store_id` | `Foreign key` associado à tabela `store`. Ingressar em `store`.`store_id` para determinar qual exibição de armazenamento do Commerce está associada ao pedido |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Billing address city` | Cidade de cobrança do pedido. Calculado ingressando em `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e retornando o campo `city` |
| `Billing address country` | Código do país para cobrança do pedido. Calculado ingressando em `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e retornando o `country_id` |
| `Billing address region` | Região de cobrança (geralmente estado ou província) do pedido. Calculado ingressando em `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e retornando o campo `region` |
| `Customer's first order date` | Carimbo de data e hora do primeiro pedido feito por esse cliente. Geralmente considerada como a &quot;data de aquisição&quot; de um cliente. Calculado retornando o mínimo de `sales_order`.Valor de `created_at` para cada cliente único |
| `Customer's first order's billing region` | Região de faturamento de aquisição do cliente que fez a ordem. Calculado retornando o `Billing address region` associado ao primeiro pedido do cliente |
| `Customer's first order's coupon_code` | Código do cupom de aquisição do cliente que fez este pedido. Calculado retornando o `coupon_code` associado ao primeiro pedido do cliente |
| `Customer's group code` | Nome do grupo do cliente que fez este pedido. Calculado ingressando em `sales_order`.`customer_group_id` a `customer_group`.`customer_group_id` e retornando o campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Quantidade total de cupons aplicados a todos os pedidos feitos por esse cliente. Calculado pela contagem do número de pedidos em que `coupon_code` não é `NULL` para cada cliente único |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por esse cliente. Calculado pela contagem do número de linhas na tabela `sales_order` para cada cliente único |
| `Customer's lifetime revenue` | Soma total da receita de todos os pedidos feitos por esse cliente. Calculado pela soma do campo `base_grand_total` para todos os pedidos de cada cliente único |
| `Customer's order number` | Classificação de ordem sequencial para a ordem deste cliente. Calculado identificando todos os pedidos feitos por um cliente, classificando-os em ordem crescente pelo carimbo de data e hora `created_at` e atribuindo um valor inteiro crescente a cada pedido. Por exemplo, o primeiro pedido do cliente retorna um `Customer's order number` de 1, o segundo pedido do cliente retorna um `Customer's order number` de 2 e assim por diante. |
| `Customer's order number (previous-current)` | Classificação da ordem anterior do cliente concatenada com a classificação desta ordem, separada por um caractere `-`. Calculado pela concatenação (&quot;`Customer's order number` - 1&quot;) com &quot;`-`&quot; seguido por &quot;`Customer's order number`&quot;. Por exemplo, para o pedido associado à segunda compra do cliente, essa coluna retorna um valor de `1-2`. Usado com mais frequência ao representar o tempo entre dois eventos de ordem (ou seja, no gráfico &quot;Tempo entre ordens&quot;) |
| `Is customer's last order?` | Determina se o pedido corresponde ao último pedido do cliente ou ao pedido mais recente. Calculado comparando o valor `Customer's order number` com `Customer's lifetime number of orders`. Quando esses dois campos são iguais para a ordem especificada, essa coluna retorna `Yes`; caso contrário, retorna `No` |
| `Number of items in order` | Quantidade total de itens incluídos no pedido. Calculado ingressando em `sales_order`.`entity_id` a `sales_order_item`.`order_id` e soma de `sales_order_item`.Campo `qty_ordered` |
| `Seconds between customer's first order date and this order` | Tempo decorrido entre este pedido e o primeiro pedido do cliente. Calculado subtraindo `Customer's first order date` de `created_at` para cada pedido, retornado como um número inteiro de segundos |
| `Seconds since previous order` | Tempo decorrido entre este pedido e o pedido imediatamente anterior do cliente. Calculado subtraindo-se o `created_at` da ordem anterior do `created_at` desta ordem, retornado como um número inteiro de segundos. Por exemplo, para o registro de pedido correspondente à terceira ordem de um cliente, essa coluna retorna o número de segundos entre a segunda ordem do cliente e a terceira ordem. Para a primeira ordem do cliente, este campo retorna `NULL` |
| `Shipping address city` | Cidade de remessa do pedido. Calculado ingressando em `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e retornando o campo `city` |
| `Shipping address country` | Código do país para remessa do pedido. Calculado ingressando em `sales_order`.`Shipping_address_id` a `sales_order_address`.`entity_id` e retornando o `country_id` |
| `Shipping address region` | Região de remessa (geralmente estado ou província) do pedido. Calculado ingressando em `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e retornando o campo `region` |
| `Store name` | O nome da loja da Commerce associada a este pedido. Calculado ingressando em `sales_order`.`store_id` a `store`.`store_id` e retornando o campo `name` |

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Avg order value` | A receita média por pedido, em que a receita é definida como `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | O tempo médio entre o pedido de um cliente (n-1) e o enésimo pedido, para todos os clientes e pedidos | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | A soma do valor bruto da mercadoria para todas as ordens, em que GMV é definido como o subtotal, antes da aplicação de todos os impostos e descontos | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | O tempo mediano entre o pedido de um cliente (n-1) e o enésimo pedido, para todos os clientes e pedidos | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | A contagem total de pedidos feitos | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | A soma da receita de todos os pedidos, em que a receita é definida como o preço final pago pelo cliente, depois que todos os impostos, descontos, remessa etc. são aplicados | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | A soma do valor de remessa de todas as ordens | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | A soma dos impostos aplicados a todas as ordens | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | O número de clientes únicos que fazem um pedido no intervalo de tempo do relatório especificado. Por exemplo, se o intervalo do relatório for semanal, cada cliente que faz pelo menos um pedido em uma determinada semana é contado exatamente uma vez, independentemente de quantos pedidos eles fizeram nessa semana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Caminhos de associação

`customer_entity`

* Ingresse na tabela `customer_entity` para criar novas colunas no nível do cliente associadas ao cliente que fez o pedido.
   * Caminho: `sales_order.customer_id` (muitos) => `customer_entity.entity_id` (um)

`customer_group`

* Ingresse na tabela `customer_group` para criar colunas que retornam o nome do grupo de clientes do cliente que fez o pedido.
   * Caminho: `sales_order.customer_group_id` (muitos) => `customer_group.customer_group_id` (um)

`sales_order_address`

* Ingresse na tabela `sales_order_address` para criar colunas que retornam locais de cobrança e de remessa associados ao pedido. Dois caminhos de ligação são possíveis, dependendo se os detalhes de faturamento ou envio são necessários.
   * Caminhos:
      * Envio: `sales_order.shipping_address_id`(muitos) => `sales_order_address.entity_id` (um)
      * Faturamento: `sales_order.billing_address_id`(muitos) => `sales_order_address.entity_id` (um)

`store`

* Associe-se à tabela `store` para criar colunas que retornam detalhes relacionados à loja da Commerce associada ao pedido.
   * Caminho: `sales_order.store_id` (muitos) => `store.store_id` (um)
