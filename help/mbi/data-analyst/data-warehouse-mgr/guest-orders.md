---
title: Pedidos de convidados
description: Saiba mais sobre o impacto que os pedidos de convidados têm nos seus dados e quais opções você tem para contabilizar corretamente os pedidos de convidados na sua Data Warehouse [!DNL Commerce Intelligence] .
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Pedidos de convidados

Ao revisar seus pedidos, se você notar que muitos valores de `customer\_id` são nulos ou não têm um valor para retornar à tabela `customers`, isso indica que sua loja permite pedidos de convidados. Isso significa que sua tabela `customers` provavelmente não inclui todos os seus clientes.

Este tópico discute o impacto que os pedidos de convidados têm nos seus dados e quais opções você tem para contabilizar corretamente os pedidos de convidados na sua Data Warehouse [!DNL Commerce Intelligence].

## Impacto dos pedidos de convidados nos dados

No banco de dados de comércio típico, há uma tabela `orders` que se une a uma tabela `customers`. Cada linha da tabela `orders` tem uma coluna `customer\_id` que é exclusiva de uma linha da tabela `customers`.

* **Se todos os clientes estiverem registrados** e os pedidos de convidados não forem permitidos, significa que cada registro na tabela `orders` tem um valor na coluna `customer\_id`. Como resultado, cada pedido se junta de volta à tabela `customers`.

  ![](../../assets/guest-orders-4.png)

* **Se os pedidos de convidado forem permitidos**, isso significa que alguns pedidos não têm um valor na coluna `customer\_id`. Somente clientes registrados recebem um valor para a coluna `customer\_id` na tabela `orders`. Os clientes que não estão registrados recebem um valor `NULL` (ou em branco) para esta coluna. Como resultado, nem todos os registros de pedido têm registros correspondentes na tabela `customers`.

  >[!NOTE]
  >
  >Para identificar o indivíduo único que fez o pedido, precisa haver outro atributo de usuário único além de `customer\_id` anexado a um pedido. Normalmente, o endereço de email do cliente é usado.

## Como contabilizar ordens de convidado na configuração do Data Warehouse

Normalmente, o engenheiro de vendas que implementa sua conta leva em consideração os pedidos de convidados ao criar a base da sua Data Warehouse.

A melhor maneira de considerar pedidos de convidados é basear todas as métricas de nível de cliente na tabela `orders`. Essa configuração usa uma ID de cliente exclusiva que todos os clientes têm, incluindo convidados (normalmente o email do cliente é usado). Isso ignora os dados de registro da tabela `customers`. Com essa opção, somente os clientes que tiverem feito pelo menos uma compra serão incluídos nos relatórios no nível do cliente. Os usuários registrados que ainda não fizeram uma compra não são incluídos. Com essa opção, a métrica `New customer` é baseada na data do primeiro pedido do cliente na tabela `orders`.

Observe que o filtro `Customers we count` definido nesse tipo de configuração tem um filtro para `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

Em uma situação sem pedidos de convidado, cada cliente existe como uma linha exclusiva na tabela de clientes (consulte a Imagem 1). Uma métrica como `New customers` pode simplesmente contar a ID desta tabela com base na data `created\_at` para entender Novos clientes com base na data de registro.

Em uma configuração de pedidos de convidado em que todas as métricas do cliente são baseadas na tabela `orders` para contabilizar pedidos de convidado, você deve garantir que esteja `not counting customers twice`. Se você contar a id da tabela de pedidos, estará contando cada pedido. Se, em vez disso, você contar a ID na tabela `orders` e usar um filtro, `Customer's order number = 1`, então você vai contar cada cliente único `only one time`. Isso é aplicável para todas as métricas no nível do cliente, como `Customer's lifetime revenue` ou `Customer's lifetime number of orders`.

Você pode ver acima que há `customer\_ids` nulo na tabela `orders`. Se você usar a `customer\_email` para identificar clientes únicos, verá que `erin@test.com` fez três (3) pedidos. Portanto, você pode criar uma métrica `New customers` na tabela `orders` com base nas seguintes condições:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
