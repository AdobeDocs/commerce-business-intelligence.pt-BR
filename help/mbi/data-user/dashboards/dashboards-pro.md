---
title: Painéis de Controle Prontos para Uso
description: Saiba mais sobre os painéis prontos para uso para fornecer insights sobre sua empresa.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# Painéis de controle prontos para uso

O [!DNL Adobe Commerce Intelligence] inclui painéis prontos para uso para fornecer insights sobre sua empresa. Com os painéis, você pode verificar a integridade de métricas essenciais, como a receita vitalícia do usuário, o número de compras repetidas, os principais produtos comprados em um determinado período e muito mais. Esses painéis pré-configurados foram criados para ajudá-lo a tomar decisões de negócios conscientes.

>[!NOTE]
>
>O acesso a esses painéis depende do tipo de conta e do nível de acesso. Se você não vir esses painéis, contate o [suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).

## Disponibilidade do relatório

Para os painéis `Customers` e `Executive Summary`, alguns relatórios só estão disponíveis, dependendo da configuração de check-out da sua loja. Especificamente, se o armazenamento permitir check-out de convidado ou não permitir check-out de convidado.

## Clientes (check-out de convidado permitido)

O painel Clientes (checkout de convidado permitido) fornece informações sobre sua base de clientes, como comportamento de compra. Esse painel pode ajudar a melhorar a retenção do cliente e determinar quais clientes geram a receita mais alta.

### Relatórios

| Nome | Descrição |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Pedidos nos últimos 30 dias de clientes que nunca fizeram um pedido anteriormente. |
| `Orders by Existing Customers (Past 30 Days)` | Pedidos nos últimos 30 dias de clientes que fizeram pelo menos um pedido anteriormente. |
| `Total Unique Customers (Past 30 Days)` | Contagem de clientes únicos que fizeram pedidos nos últimos 30 dias. |
| `Orders by New vs Existing Customers` | Número de pedidos por clientes sem pedidos anteriores versus clientes com pelo menos um pedido anterior. |
| `Subsequent Order Probability (All Time)` | A probabilidade de os clientes que fizeram um pedido fazerem outro. |
| `% of Customers with Multiple Orders (All Time)` | Porcentagem de todos os clientes que fizeram mais de um pedido. |
| `Median Time Between Orders (All Time)` | Tempo médio que cada cliente leva entre a realização de um pedido e o próximo. |
| `Subsequent Order Probability` | A probabilidade de os clientes que fizeram um pedido fazerem outro pedido, dividido pelo número do pedido. Ou seja, o percentual de clientes com um pedido que fazem um segundo, o percentual com dois que fazem um terceiro, e assim por diante. |
| `Time Between Orders` | O tempo médio e mediano que os clientes passam entre os pedidos, dividido por número de pedido (ou seja, o tempo entre os pedidos um e dois, dois e três e assim por diante). |
| `Number of Customers - Lifetime Orders` | Para um determinado número de pedidos feitos durante a vida útil de um cliente, o número de clientes que fizeram esses pedidos e a porcentagem de toda a base de clientes que esse número representa. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clientes que fizeram sua primeira e única compra entre três e seis meses atrás. |
| `Avg LTV by First Order` | Compara a receita média cumulativa de vida útil do cliente em todos os coortes. Os coortes são definidos pelo mês em que um cliente fez uma compra pela primeira vez. Por exemplo, uma coorte `Jan 2020` mostra o LTV médio cumulativo para clientes cuja primeira compra foi em janeiro de 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparação da receita média dos clientes nos 30 dias após a primeira compra em relação a toda a vida útil. Cada bolha corresponde a uma região de entrega e o tamanho de cada bolha representa o número de clientes adquiridos dessa região. |

## Clientes (checkout de convidado não é permitido)

O painel Clientes (sem check-out de convidado permitido) fornece informações sobre sua base de clientes, como comportamento de compra e conversões de registros de conta para disposições de pedidos. Esse painel pode ajudar a melhorar a retenção do cliente e determinar quais clientes geram a receita mais alta.

### Relatórios

| Nome | Descrição |
|---|---|
| `Account Registration (Past 30 Days)` | O número de pessoas que se registraram para uma conta em sua loja nos últimos 30 dias. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | O número de pessoas que se registraram para uma conta em sua loja nos últimos 30 dias e também fizeram pelo menos um pedido. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Porcentagem de contas registradas nos últimos 30 dias que fizeram um pedido. |
| `% Conversion from Registration to First Order` | Porcentagem de contas registradas que fizeram um pedido, por mês de registro. |
| `Orders by New vs Existing Customers` | Número de pedidos por clientes sem pedidos anteriores versus clientes com pelo menos um pedido anterior. |
| `Subsequent Order Probability (All Time)` | A probabilidade de os clientes que fizeram um pedido fazerem outro. |
| `% of Customers with Multiple Orders (All Time)` | Porcentagem de todos os clientes que fizeram mais de um pedido. |
| `Median Time Between Orders (All Time)` | Tempo médio que cada cliente leva entre a realização de um pedido e o próximo. |
| `Subsequent Order Probability` | A probabilidade de os clientes que fizeram um pedido fazerem outro, dividido pelo número do pedido. Isto é, por cento de clientes com um pedido que fazem um segundo, por cento com dois que fazem um terceiro, e assim por diante. |
| `Time Between Orders` | O tempo médio e mediano que os clientes passam entre os pedidos, dividido por número de pedido (ou seja, o tempo entre os pedidos um e dois, dois e três e assim por diante). |
| `Number of Customers - Lifetime Orders` | Para um determinado número de pedidos feitos durante a vida útil de um cliente, o número de clientes que fizeram esses pedidos e a porcentagem de toda a base de clientes que esse número representa. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clientes que fizeram sua primeira e única compra entre três e seis meses atrás. |
| `Avg LTV by First Order` | Compara a receita média cumulativa de vida útil do cliente em todos os coortes. Os coortes são definidos pelo mês em que um cliente fez uma compra pela primeira vez. Por exemplo, uma coorte de janeiro de 2020 mostra o LTV médio cumulativo para clientes cuja primeira compra foi em janeiro de 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparação da receita média dos clientes nos 30 dias após a primeira compra em relação a toda a vida útil. Cada bolha corresponde a uma região de entrega e o tamanho de cada bolha representa o número de clientes adquiridos dessa região. |

## Resumo executivo (check-out de convidado permitido)

O painel Resumo executivo (checkout de convidado permitido) fornece uma imagem sucinta de como a empresa está se saindo em termos de pedidos e receita. Esse painel foi projetado para que os executivos obtenham uma compreensão geral do desempenho dos negócios, mas também pode ser revelador para outras pessoas.

### Relatórios

| Nome | Descrição |
|---|---|
| `Revenue (Current Month)` | A receita gerada pela sua loja para o mês atual. Nesse caso, a receita é definida como o preço final pago por um cliente em um pedido. |
| `Revenue (Past 6 Months by Day)` | Receita diária total, sobreposta à receita diária média dos sete dias anteriores. Nesse caso, a receita é definida como o preço final pago por um cliente em um pedido. |
| `% Change in Revenue (MoM MTD)` | Comparação da receita do mês atual (até agora) com a mesma parte do mês anterior. |
| `Revenue from New vs Existing Customers (Current Month)` | Receita do mês atual (até agora) atribuída a novos clientes (novos) em comparação a clientes existentes (colocando em segundo ou último pedido). |
| `Average Order Value (Current Month)` | Valor médio diário de pedidos feitos no mês atual (até o momento). O valor do pedido é definido como o preço final pago por um cliente em um pedido. |
| `Orders (Current Month)` | O número de pedidos feitos em sua loja para o mês atual (até agora). |
| `% Change in Orders (MoM MTD)` | Comparação do número de pedidos do mês atual (até agora) versus a mesma parte do mês anterior. |
| `Orders by New Customers (Current Month)` | Pedidos do mês atual de clientes que nunca fizeram um pedido anteriormente. |
| `Orders by Existing Customers (Current Month)` | Pedidos do mês atual de clientes que fizeram pelo menos um pedido anteriormente. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Número de pedidos por clientes sem pedidos anteriores vs. por clientes com pelo menos um pedido anterior, para cada semana do ano atual (até agora). |

## Resumo executivo (nenhum check-out de convidado permitido)

O painel Resumo executivo (sem check-out de convidado permitido) fornece uma imagem sucinta de como a empresa está se saindo em termos de pedidos, receita e registros de conta. Esse painel foi projetado para que os executivos obtenham uma compreensão geral do desempenho dos negócios, mas também pode ser revelador para outras pessoas.

### Relatórios

| Nome | Descrição |
|---|---|
| `Revenue (Current Month)` | A receita gerada pela sua loja este mês. Nesse caso, a receita é definida como o preço final pago por um cliente em um pedido. |
| `Revenue (Past 6 Months by Day)` | Receita diária total, sobreposta à receita diária média dos sete dias anteriores. Nesse caso, a receita é definida como o preço final pago por um cliente em um pedido. |
| `% Change in Revenue (MoM MTD)` | Comparação da receita até o momento neste mês em relação à mesma parte do mês anterior. |
| `Revenue from New vs Existing Customers (Current Month)` | Receita do mês atual (até agora) atribuída a novos clientes (novos) em comparação a clientes existentes (colocando em segundo ou último pedido). |
| `Average Order Value (Current Month)` | Valor médio diário de pedidos feitos no mês atual (até o momento). O valor do pedido é definido como o preço final pago por um cliente em um pedido. |
| `Orders (Current Month)` | O número de pedidos feitos em sua loja para o mês atual (até agora). |
| `% Change in Orders (MoM MTD)` | Comparação do número de pedidos do mês atual (até agora) versus a mesma parte do mês anterior. |
| `Account Registrations (Current Month)` | O número de contas recém-registradas até agora neste mês. |
| `% Conversion from Registration to First Order (Current Month)` | A porcentagem de contas registradas até agora neste mês que fizeram um pedido. |
| `% Conversion from Registration to First Order (Current Year by Week)` | A porcentagem de contas registradas semanalmente até agora este ano que fizeram um pedido. |

## Pedidos

O painel Pedidos fornece informações sobre o volume transacional de pedidos, o status, os códigos de cupom usados, a receita gerada e os métodos de pagamento usados. Por exemplo, você pode rastrear o processo de preenchimento e garantir que não haja ocorrências de problemas ou gargalos.

>[!NOTE]
>
>Os relatórios nesse painel estão disponíveis para contas conectadas a lojas com qualquer tipo de configuração (check-out de convidado, sem check-out de convidado).

### Relatórios

| Nome | Descrição |
|---|---|
| `Orders (Past 30 Days)` | O número de pedidos feitos com sua loja nos últimos 30 dias. |
| `Revenue (Past 30 Days)` | A receita gerada pela sua loja nos últimos 30 dias. A receita é definida como o preço final pago por um cliente em um pedido. |
| `Average Order Value (Past 30 Days)` | Valor médio de pedidos feitos nos últimos 30 dias. O valor do pedido é definido como o preço final pago por um cliente em um pedido. |
| `Orders` | O número de pedidos feitos em sua loja a cada mês. |
| `Revenue by Payment Method` | A receita gerada pela sua loja, dividida pelo método de pagamento. A receita é definida como o preço final pago por um cliente em um pedido. |
| `AOV by New vs Existing Customers` | Valor médio mensal de pedidos feitos em sua loja, dividido por pedidos feitos por clientes sem pedidos anteriores, versus clientes com pelo menos um pedido anterior. O valor do pedido é definido como o preço final pago por um cliente em um pedido. |
| `% Orders by Status (Past 30 Days)` | Porcentagem de pedidos de cada dia nos últimos 30 dias que estão atualmente em cada status de pedido. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Uma lista de todos os pedidos feitos há mais de um dia que ainda estão com status incompleto (não cancelado ou concluído). |
| `Orders Per Hour (Past 7 Days)` | Volume do pedido por dia e por hora. |
| `Revenue Details (Past 30 Days)` | Detalhamento diário da receita dos últimos 30 dias em todos os componentes do valor total da receita. |
| `Order Details by Coupon Code (Past 30 Days)` | Para cada código de cupom oferecido pela sua loja, detalhes sobre como esse código de cupom foi usado e quais devoluções ele trouxe durante os últimos 30 dias. |
| `% Orders with Coupon (Past 30 Days)` | A porcentagem de pedidos feitos nos últimos 30 dias que usaram um cupom em comparação com aqueles que não usaram. |

## Produtos

O painel Produtos mostra o desempenho geral do produto em termos de produtos solicitados, seu Valor Bruto de Mercadoria (GMV) e os principais produtos comprados e reembolsados. Ele pode ajudá-lo a equilibrar compras e devoluções e determinar o sucesso e a popularidade do produto. Seu armazenamento deve estar [configurado para rastrear reembolsos](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html?lang=pt-BR) para que esses gráficos sejam preenchidos.

>[!NOTE]
>
>Os relatórios nesse painel estão disponíveis para contas conectadas a lojas com qualquer tipo de configuração (check-out de convidado, sem check-out de convidado).

### Relatórios

| Nome | Descrição |
|---|---|
| `GMV (Past 30 Days)` | O valor bruto de mercadoria de todos os produtos vendidos nos últimos 30 dias. GMV é definida como a quantidade solicitada multiplicada pelo preço base de cada produto. |
| `% GMV (Past 30 Days) Refunded` | Porcentagem de GMV para produtos comprados nos últimos 30 dias que resultaram em reembolso. |
| `Product Quantity Ordered (Past 30 Days)` | Quantidade total de itens solicitados nos últimos 30 dias. |
| `% Purchased Products (Past 30 Days) Refunded` | Porcentagem de itens comprados nos últimos 30 dias que resultaram em reembolso. |
| `Gross Merchandise Value` | O valor bruto de mercadoria de todos os produtos vendidos, por mês. GMV é definida como a quantidade solicitada multiplicada pelo preço base de cada produto. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Para cada produto, uma comparação do número total de pedidos nos últimos 30 dias com a taxa de reembolso do produto. O tamanho de cada bolha representa a taxa de reembolso. |
| `Product Performance Details (Past 30 Days)` | Informações detalhadas sobre vendas e reembolsos subsequentes nos últimos 30 dias, por sku e nome do produto. |
| `Top Purchased Products by GMV (Past 30 Days)` | Produtos vendidos nos últimos 30 dias que geraram mais receita (os 10 principais). |
| `Top Refunded Products by GMV (Past 30 Days)` | Produtos comprados nos últimos 30 dias que resultaram na maior perda de GMV devido a reembolsos (os 10 principais). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Produtos vendidos nos últimos 30 dias nos maiores números (os 10 melhores). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Produtos comprados nos últimos 30 dias que resultaram na maior quantidade reembolsada (os 10 principais). |
