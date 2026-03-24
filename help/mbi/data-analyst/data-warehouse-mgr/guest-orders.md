---
title: Pedidos de convidados
description: Saiba mais sobre o impacto que os pedidos de convidados têm nos seus dados e quais opções você tem para contabilizar corretamente os pedidos de convidados no seu  [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/leSf21lcOaEbm1aehC8iZLdbtRJFKK9yVQwdvft-GKQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 566
ht-degree: 0%

---

# Pedidos de convidados

Ao revisar seus pedidos, se você notar que muitos valores de `customer\_id` são nulos ou não têm um valor para retornar à tabela `customers`, isso indica que sua loja permite pedidos de convidados. Isso significa que sua tabela `customers` provavelmente não inclui todos os seus clientes.

Este tópico discute o impacto que os pedidos de convidados têm nos seus dados e quais opções você tem para contabilizar corretamente os pedidos de convidados na sua Data Warehouse [!DNL Commerce Intelligence].

## Impacto dos pedidos de convidados nos dados

No banco de dados de comércio típico, há uma tabela `orders` que se une a uma tabela `customers`. Cada linha da tabela `orders` tem uma coluna `customer\_id` que é exclusiva de uma linha da tabela `customers`.

* **Se todos os clientes estiverem registrados** e os pedidos de convidados não forem permitidos, significa que cada registro na tabela `orders` tem um valor na coluna `customer\_id`. Como resultado, cada pedido se junta de volta à tabela `customers`.

  ![Tabela de dados de pedidos convidados mostrando informações do cliente](../../assets/guest-orders-4.png)

* **Se os pedidos de convidado forem permitidos**, isso significa que alguns pedidos não têm um valor na coluna `customer\_id`. Somente clientes registrados recebem um valor para a coluna `customer\_id` na tabela `orders`. Os clientes que não estão registrados recebem um valor `NULL` (ou em branco) para esta coluna. Como resultado, nem todos os registros de pedido têm registros correspondentes na tabela `customers`.

  >[!NOTE]
  >
  >Para identificar o indivíduo único que fez o pedido, precisa haver outro atributo de usuário único além de `customer\_id` anexado a um pedido. Normalmente, o endereço de email do cliente é usado.

## Como contabilizar ordens de convidados na configuração do Data Warehouse

Normalmente, o engenheiro de vendas que implementa sua conta leva em consideração os pedidos de convidados ao criar a base da sua Data Warehouse.

A melhor maneira de considerar pedidos de convidados é basear todas as métricas de nível de cliente na tabela `orders`. Essa configuração usa uma ID de cliente exclusiva que todos os clientes têm, incluindo convidados (normalmente o email do cliente é usado). Isso ignora os dados de registro da tabela `customers`. Com essa opção, somente os clientes que tiverem feito pelo menos uma compra serão incluídos nos relatórios no nível do cliente. Os usuários registrados que ainda não fizeram uma compra não são incluídos. Com essa opção, a métrica `New customer` é baseada na data do primeiro pedido do cliente na tabela `orders`.

Observe que o filtro `Customers we count` definido nesse tipo de configuração tem um filtro para `Customer's order number = 1`.

![Configuração de conjunto de filtros para excluir ordens de convidados](../../assets/guest-orders-filter-set.png)

Em uma situação sem pedidos de convidado, cada cliente existe como uma linha exclusiva na tabela de clientes (consulte a Imagem 1). Uma métrica como `New customers` pode simplesmente contar a ID desta tabela com base na data `created\_at` para entender Novos clientes com base na data de registro.

Em uma configuração de pedidos de convidado em que todas as métricas do cliente são baseadas na tabela `orders` para contabilizar pedidos de convidado, você deve garantir que esteja `not counting customers twice`. Se você contar a id da tabela de pedidos, estará contando cada pedido. Se, em vez disso, você contar a ID na tabela `orders` e usar um filtro, `Customer's order number = 1`, então você vai contar cada cliente único `only one time`. Isso é aplicável para todas as métricas no nível do cliente, como `Customer's lifetime revenue` ou `Customer's lifetime number of orders`.

Você pode ver acima que há `customer\_ids` nulo na tabela `orders`. Se você usar a `customer\_email` para identificar clientes únicos, verá que `erin@test.com` fez três (3) pedidos. Portanto, você pode criar uma métrica `New customers` na tabela `orders` com base nas seguintes condições:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
