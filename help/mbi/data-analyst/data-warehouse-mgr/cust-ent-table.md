---
title: tabela customer_entity
description: Saiba como acessar registros de todas as contas registradas.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Tabela customer_entity

A tabela `customer_entity` contém registros de todas as contas registradas. Uma conta é considerada registrada se eles se inscreverem em uma conta, independentemente de concluírem uma compra. Cada linha corresponde a uma conta registrada exclusiva, conforme identificado pelo `entity_id` dessa conta.

Esta tabela não contém registros de clientes que fazem um pedido por meio do check-out do convidado. Se a loja aceitar o check-out do convidado, consulte [como contabilizar pedidos de convidado](../data-warehouse-mgr/guest-orders.md) para esses pedidos.

## Colunas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `created_at` | Carimbo de data e hora correspondente à data de registro da conta, armazenado localmente em UTC. Dependendo da sua configuração no [!DNL Commerce Intelligence], esse carimbo de data/hora pode ser convertido em um fuso horário de relatórios no [!DNL Commerce Intelligence] que seja diferente do fuso horário do banco de dados |
| `email` | Endereço de email associado à conta |
| `entity_id` (CP) | Identificador exclusivo da tabela e geralmente usado em associações com o `customer_id` em outras tabelas na instância |
| `group_id` | Chave estrangeira associada à tabela `customer_group`. Ingressar em `customer_group.customer_group_id` para determinar o grupo de clientes associado à conta registrada |
| `store_id` | Chave estrangeira associada à tabela `store`. Ingressar em `store`.`store_id` para determinar qual exibição de armazenamento do Commerce está associada à conta registrada |

{style="table-layout:auto"}

## Colunas calculadas comuns

| **Nome da coluna** | **Descrição** |
|---|---|
| `Customer's first 30 day revenue` | Soma total da receita de todas as ordens feitas por este cliente dentro de 30 dias da data da primeira ordem do cliente. Calculado unindo `customer_entity.entity_id` a `sales_order.customer_id` e somando o campo `base_grand_total` para todos os pedidos em que `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, que é o número de segundos em 30 dias |
| `Customer's first order date` | Carimbo de data e hora do primeiro pedido feito por esse cliente. Calculado ao juntar `customer_entity.entity_id` a `sales_order.customer_id` e retornar o mínimo de `sales_order`.Valor `created_at` |
| `Customer's first order's billing region` | Região de faturamento associada ao primeiro pedido do cliente. Calculado ingressando `customer_entity.entity_id` em `sales_order.customer_id` e retornando o `Billing address region`, onde `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Código do cupom associado ao primeiro pedido do cliente. Calculado ingressando `customer_entity.entity_id` em `sales_order.customer_id` e retornando o `sales_order.coupon_code`, onde `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nome do grupo do cliente registrado. Calculado pela associação de `customer_entity.group_id` a `customer_group`.`customer_group_id` e retornando o campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Número total de cupons aplicados a todos os pedidos feitos por esse cliente. Calculado ao juntar `customer_entity.entity_id` a `sales_order.customer_id` e contar o número de pedidos nos quais `sales_order.coupon_code` não é `NULL` |
| `Customer's lifetime number of orders` | Contagem total de pedidos feitos por esse cliente. Calculado unindo `customer_entity.entity_id` a `sales_order.customer_id` e contando o número de linhas na tabela `sales_order` |
| `Customer's lifetime revenue` | Soma total da receita de todos os pedidos feitos por esse cliente. Calculado ingressando de `customer_entity.entity_id` em `sales_order.customer_id` e somando o campo `base_grand_total` para todos os pedidos feitos por este cliente |
| `Seconds since customer's first order date` | Tempo decorrido entre a data do primeiro pedido do cliente e a data atual. Calculado pela subtração de `Customer's first order date` do carimbo de data/hora do servidor no momento em que a consulta é executada, retornado como um número inteiro de segundos |
| `Store name` | O nome da loja da Commerce associada a esta conta registrada. Calculado ao ingressar de `customer_entity.store_id` em `store.store_id` e retornar o campo `name` |

{style="table-layout:auto"}

## Métricas comuns

| **Nome da métrica** | **Descrição** | **Construção** |
|---|---|---|
| `Avg first 30 day revenue` | A receita média por cliente para pedidos feitos no prazo de 30 dias a partir da primeira ordem do cliente | Operação: Average<br/>Operand: `Customer's first 30 day revenue`<br/>Carimbo de data/hora: `created_at`<br/>Filtros:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclui clientes que ainda não atingiram 30 dias desde sua primeira ordem) |
| `Avg lifetime coupons` | O número médio de cupons aplicados a pedidos por cliente durante sua vida útil | Operação: Média<br/>Operando: `Customer's lifetime number of coupons`<br/>Carimbo de data/hora: `created_at` |
| `Avg lifetime orders` | O número médio de pedidos feitos por cliente durante sua vida útil | Operação: Média<br/>Operando: `Customer's lifetime number of orders`<br/>Carimbo de data/hora: `created_at` |
| `Avg lifetime revenue` | A receita total média por cliente para todos os pedidos feitos durante sua vida útil | Operação: Média<br/>Operando: `Customer's lifetime revenue`<br/>Carimbo de data/hora: `created_at` |
| `New customers` | O número de clientes com pelo menos um pedido, contado na data do primeiro pedido. Exclui contas que se registram, mas nunca fazem um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data/hora: `Customer's first order date` |
| `Registered accounts` | O número de contas registradas. Inclui todas as contas registradas, independentemente da conta ter feito um pedido | Operação: Contagem<br/>Operando: `entity_id`<br/>Carimbo de data/hora: `created_at` |

{style="table-layout:auto"}

## Caminhos de Junção de Chave Estrangeira

`customer_group`

* Ingresse na tabela `customer_group` para criar colunas que retornam o nome do grupo de clientes da conta registrada.
   * Caminho: `customer_entity.group_id` (muitos) => `customer_group.customer_group_id` (um)

`store`

* Ingresse na tabela `store` para criar colunas que retornam detalhes relacionados ao armazenamento associado à conta registrada.
   * Caminho: `customer_entity.store_id` (muitos) => `store.store_id` (um)
