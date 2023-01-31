---
title: tabela customer_entity
description: Saiba como acessar registros de todas as contas registradas.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Tabela customer_entity

O `customer_entity` tabela contém registros de todas as contas registradas. Uma conta é considerada registrada se se inscrever em uma conta, independentemente de alguma vez terem concluído uma compra ou não. Cada linha corresponde a uma conta registrada exclusiva, conforme identificado pelo `entity_id`.

Esta tabela não contém registros de clientes que fazem um pedido via check-out de convidado. Se sua loja aceitar check-out de convidado, [saiba como contar](../data-warehouse-mgr/guest-orders.md) para esses clientes.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `created_at` | Carimbo de data e hora correspondente à data de registro da conta, geralmente armazenado localmente em UTC. Dependendo da sua configuração em [!DNL MBI], esse carimbo de data e hora pode ser convertido em um fuso horário de relatório no [!DNL MBI] que difere do fuso horário do banco de dados |
| `email` | Endereço de email associado à conta |
| `entity_id` (PK) | Identificador exclusivo para a tabela e normalmente usado em associações ao `customer_id` em outras tabelas na instância |
| `group_id` | Chave externa associada à `customer_group` tabela. Associar-se a `customer_group.customer_group_id` para determinar o grupo de clientes associado à conta registrada |
| `store_id` | Chave externa associada à `store` tabela. Associar-se a `store`.`store_id` para determinar qual exibição de loja do Commerce está associada à conta registrada |

{style=&quot;table-layout:auto&quot;}

## Colunas Calculadas Comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's first 30 day revenue` | Soma total da receita para todos os pedidos feitos por este cliente dentro de 30 dias da data do primeiro pedido do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e resumir `base_grand_total` para todas as ordens em que `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, que é o número de segundos em 30 dias |
| `Customer's first order date` | Carimbo de data e hora do primeiro pedido feito por este cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e regressando ao mínimo `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Região de faturamento associada ao primeiro pedido do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e retornar `Billing address region` em que `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Código do cupom associado ao primeiro pedido do cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e retornar `sales_order.coupon_code` em que `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nome do grupo do cliente registrado. Calculado por associação `customer_entity.group_id` para `customer_group`.`customer_group_id` e retornar `customer_group_code` campo |
| `Customer's lifetime number of coupons` | Número total de cupons aplicados a todas as ordens feitas por este cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e contando o número de pedidos em que a `sales_order.coupon_code` não é `NULL` |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por este cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e a contagem do número de linhas na `sales_order` tabela |
| `Customer's lifetime revenue` | Soma total da receita para todos os pedidos feitos por este cliente. Calculado por associação `customer_entity.entity_id` para `sales_order.customer_id` e resumir `base_grand_total` campo para todos os pedidos feitos por este cliente |
| `Seconds since customer's first order date` | Tempo decorrido entre a data do primeiro pedido do cliente e agora. Calculado por subtração `Customer's first order date` do carimbo de data e hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos |
| `Store name` | O nome da loja Comércio associado a esta conta registrada. Calculado por associação `customer_entity.store_id` para `store.store_id` e retornar `name` campo |

{style=&quot;table-layout:auto&quot;}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Avg first 30 day revenue` | A receita média por cliente para pedidos feitos dentro de 30 dias do primeiro pedido do cliente | Operação: Média<br/>Operando: `Customer's first 30 day revenue`<br/>Carimbo de data e hora: `created_at`<br/>Filtros:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclui clientes que ainda não atingiram 30 dias desde o primeiro pedido) |
| `Avg lifetime coupons` | O número médio de cupons aplicado a ordens por cliente ao longo do seu período de vida | Operação: Média<br/>Operando: `Customer's lifetime number of coupons`<br/>Carimbo de data e hora: `created_at` |
| `Avg lifetime orders` | O número médio de pedidos feitos por cliente durante sua vida útil | Operação: Média<br/>Operando: `Customer's lifetime number of orders`<br/>Carimbo de data e hora: `created_at` |
| `Avg lifetime revenue` | A receita total média por cliente para todos os pedidos feitos durante sua vida útil | Operação: Média<br/>Operando: `Customer's lifetime revenue`<br/>Carimbo de data e hora: `created_at` |
| `New customers` | O número de clientes com pelo menos um pedido, contado na data do primeiro pedido. Exclui contas que se registram, mas nunca fazem um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data e hora: `Customer's first order date` |
| `Registered accounts` | O número de contas registradas. Inclui todas as contas registradas, independentemente de a conta ter ou não efetuado um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data e hora: `created_at` |

{style=&quot;table-layout:auto&quot;}

## Caminhos de associação de chave externa

`customer_group`

* Associar-se a `customer_group` tabela para criar novas colunas que retornam o nome do grupo de clientes da conta registrada.
   * Caminho: `customer_entity.group_id` (muitos) => `customer_group.customer_group_id` (1)

`store`

* Associar-se a `store` tabela para criar novas colunas que retornam detalhes relacionados à loja associada à conta registrada.
   * Caminho: `customer_entity.store_id` (muitos) => `store.store_id` (1)
