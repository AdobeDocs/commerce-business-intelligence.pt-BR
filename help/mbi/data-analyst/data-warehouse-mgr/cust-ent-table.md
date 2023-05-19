---
title: tabela customer_entity
description: Saiba como acessar registros de todas as contas registradas.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Tabela customer_entity

A variável `customer_entity` a tabela contém registros de todas as contas registradas. Uma conta é considerada registrada se eles se inscreverem em uma conta, independentemente de concluírem uma compra. Cada linha corresponde a uma conta registrada exclusiva, conforme identificado pelo `entity_id`.

Esta tabela não contém registros de clientes que fazem um pedido por meio do check-out do convidado. Se a loja aceitar o check-out do convidado, consulte [como contabilizar pedidos de convidados](../data-warehouse-mgr/guest-orders.md) para essas ordens.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `created_at` | Carimbo de data e hora correspondente à data de registro da conta, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data e hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que difere do fuso horário do seu banco de dados |
| `email` | Endereço de email associado à conta |
| `entity_id` PK) | Identificador exclusivo da tabela, geralmente usado em associações com a `customer_id` em outras tabelas na instância |
| `group_id` | Chave estrangeira associada à `customer_group` tabela. Associar-se a `customer_group.customer_group_id` para determinar o grupo de clientes associado à conta registrada |
| `store_id` | Chave estrangeira associada à `store` tabela. Associar-se a `store`.`store_id` para determinar qual exibição de loja do Commerce está associada à conta registrada |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's first 30 day revenue` | Soma total da receita de todas as ordens feitas por este cliente dentro de 30 dias da data da primeira ordem do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e a soma de `base_grand_total` para todas as ordens em que `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, que é o número de segundos em 30 dias |
| `Customer's first order date` | Carimbo de data e hora do primeiro pedido feito por esse cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e retornando o mínimo `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Região de faturamento associada ao primeiro pedido do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e o retorno do `Billing address region` onde `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Código do cupom associado ao primeiro pedido do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e o retorno do `sales_order.coupon_code` onde `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nome do grupo do cliente registrado. Calculado por associação `customer_entity.group_id` para `customer_group`.`customer_group_id` e o retorno do `customer_group_code` campo |
| `Customer's lifetime number of coupons` | Número total de cupons aplicados a todos os pedidos feitos por esse cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e a contagem do número de ordens em que a `sales_order.coupon_code` não é `NULL` |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por esse cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e a contagem do número de linhas no `sales_order` tabela |
| `Customer's lifetime revenue` | Soma total da receita de todos os pedidos feitos por esse cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e a soma de `base_grand_total` campo para todos os pedidos feitos por este cliente |
| `Seconds since customer's first order date` | Tempo decorrido entre a data do primeiro pedido do cliente e a data atual. Calculado por subtração `Customer's first order date` no carimbo de data e hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos |
| `Store name` | O nome da Commerce store associada a esta conta registrada. Calculado por associação `customer_entity.store_id` para `store.store_id` e o retorno do `name` campo |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Avg first 30 day revenue` | A receita média por cliente para pedidos feitos no prazo de 30 dias a partir da primeira ordem do cliente | Operação: média<br/>Operando: `Customer's first 30 day revenue`<br/>Carimbo de data/hora: `created_at`<br/>Filtros:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclui clientes que ainda não atingiram 30 dias desde seu primeiro pedido) |
| `Avg lifetime coupons` | O número médio de cupons aplicados a pedidos por cliente durante sua vida útil | Operação: média<br/>Operando: `Customer's lifetime number of coupons`<br/>Carimbo de data/hora: `created_at` |
| `Avg lifetime orders` | O número médio de pedidos feitos por cliente durante sua vida útil | Operação: média<br/>Operando: `Customer's lifetime number of orders`<br/>Carimbo de data/hora: `created_at` |
| `Avg lifetime revenue` | A receita total média por cliente para todos os pedidos feitos durante sua vida útil | Operação: média<br/>Operando: `Customer's lifetime revenue`<br/>Carimbo de data/hora: `created_at` |
| `New customers` | O número de clientes com pelo menos um pedido, contado na data do primeiro pedido. Exclui contas que se registram, mas nunca fazem um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data/hora: `Customer's first order date` |
| `Registered accounts` | O número de contas registradas. Inclui todas as contas registradas, independentemente da conta ter feito um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data/hora: `created_at` |

{style="table-layout:auto"}

## Caminhos de Junção de Chave Estrangeira

`customer_group`

* Associar-se a `customer_group` tabela para criar colunas que retornam o nome do grupo de clientes da conta registrada.
   * Caminho: `customer_entity.group_id` (muitos) => `customer_group.customer_group_id` (um)

`store`

* Associar-se a `store` tabela para criar colunas que retornam detalhes relacionados à loja associada à conta registrada.
   * Caminho: `customer_entity.store_id` (muitos) => `store.store_id` (um)
