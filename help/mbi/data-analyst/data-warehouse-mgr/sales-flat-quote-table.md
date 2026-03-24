---
title: Tabela de cotações
description: Saiba como trabalhar com a tabela de cotações.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/Q-46fusr2IS4ZQDrR8IjHEttueSBpT2-LQBtsejMEC4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 612
ht-degree: 0%

---

# Tabela de Cotações

A tabela `quote` (`sales_flat_quote` em M1) contém registros em cada carrinho de compras criado em sua loja, independentemente de terem sido abandonados ou convertidos em uma compra. Cada linha representa um carrinho. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias.

>[!NOTE]
>
>A análise de carrinhos históricos e abandonados só é possível se você não excluir registros da tabela `quote`. Ao excluir registros, você só poderá ver os carrinhos que ainda não foram removidos do banco de dados.

## Colunas Nativas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `base_currency_code` | Moeda para todos os valores capturados nos campos `base_*` (ou seja, `base_grand_total`, `base_subtotal` e assim por diante). Normalmente, isso reflete a moeda padrão da loja da Commerce |
| `base_grand_total` | Preço final cotado para o cliente do carrinho, depois que todos os impostos, frete e descontos são aplicados. Embora o cálculo preciso seja personalizável, em geral `base_grand_total` é calculado como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de mercadoria de todos os itens incluídos no carrinho. Impostos, frete, descontos e assim por diante não estão incluídos |
| `created_at` | Carimbo de data e hora de criação do carrinho, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data/hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que seja diferente do fuso horário do banco de dados |
| `customer_email` | Endereço de email do cliente que criou o carrinho |
| `customer_id` | `Foreign key` associado à tabela `customer_entity`, se o cliente estiver registrado. Associe-se a `customer_entity.entity_id` para determinar os atributos do cliente associados ao usuário que criou o carrinho. Se o carrinho foi criado através do check-out do convidado, este campo é `NULL` |
| `entity_id` (CP) | Identificador exclusivo da tabela e geralmente usado em associações com outras tabelas na instância do Commerce |
| `is_active` | Campo booleano que retorna &quot;1&quot; se o carrinho foi criado por um cliente e ainda não foi convertido em um pedido. Retorna &quot;0&quot; para carrinhos convertidos ou carrinhos criados pelo administrador |
| `items_qty` | Soma da quantidade total de todos os itens incluídos no carrinho |
| `reserved_order_id` | `Foreign key` associado à tabela `sales_order`. Associe-se a `sales_order.increment_id` para determinar os detalhes do pedido associados a um carrinho convertido. Para carrinhos que não estão associados a uma ordem convertida, o `reserved_order_id` permanece `NULL` |
| `store_id` | `Foreign key` associado à tabela `store`. Ingressar em `store`.`store_id` para determinar qual exibição de loja do Commerce está associada ao carrinho |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Order date` | Carimbo de data e hora que reflete a data de criação da ordem para carrinhos convertidos. Calculado ao ingressar de `quote.reserved_order_id` em `sales_order.increment_id` e retornar o campo `sales_order.created_at` |
| `Seconds between cart creation and order` | Tempo decorrido entre a criação do carrinho e a criação do pedido. Calculado pela subtração de `created_at` de `Order date`, retornado como um número inteiro de segundos |
| `Seconds since cart creation` | Tempo decorrido entre a data de criação do carrinho e agora. Calculado pela subtração de `created_at` do carimbo de data/hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos. Usado mais frequentemente para identificar a idade de um carrinho |
| `Store name` | O nome da loja da Commerce associada a este pedido. Calculado ao ingressar de `quote.store_id` em `store.store_id` e retornar o campo `name` |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Number of abandoned carts` | A contagem de carrinhos que atendem a condições específicas de &quot;abandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtros:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |
| `Avg time to cart conversion` | O tempo médio entre a criação do carrinho e a criação da ordem para carrinhos convertidos | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | A soma da receita potencial total do carrinho abandonado, em que a receita é definida como o campo `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtros:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, onde &quot;x&quot; corresponde ao tempo decorrido (em segundos) desde a criação do carrinho, além do qual um carrinho é considerado abandonado |

{style="table-layout:auto"}

## Caminhos de Junção de Chave Estrangeira

`customer_entity`

* Associe-se à tabela `customer_entity` para criar novas colunas no nível do cliente associadas ao cliente que criou o carrinho.
   * Caminho: `quote.customer_id` (muitos) => `customer_entity.entity_id` (um)

`sales_order`

* Associe-se à tabela `sales_order` para criar colunas que retornam detalhes da ordem associados ao carrinho convertido.
   * Caminho:`quote.reserved_order_id` (muitos) => `sales_order.increment_id` (um)

`store`

* Ingresse na tabela `store` para criar colunas que retornam detalhes relacionados à loja da Commerce associada ao carrinho.
   * Caminho: `quote.store_id` (muitos) => `store.store_id` (um)
