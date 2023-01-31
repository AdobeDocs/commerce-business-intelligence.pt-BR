---
title: Pedidos de convidado
description: Saiba mais sobre o impacto que os pedidos de convidado têm em seus dados e quais opções você tem para contabilizar corretamente os pedidos de convidado em seus [!DNL MBI] data warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Pedidos de convidado

Ao revisar seus pedidos, se você perceber que muitos `customer\_id` são nulos ou não têm um valor para unir de volta à `customers` tabela, isso geralmente indica que sua loja permite pedidos de convidado. Isso significa que a variável `customers` provavelmente não inclui todos os seus clientes.

Neste tópico, discutimos o impacto que os pedidos de convidado têm em seus dados e quais opções você tem para considerar corretamente os pedidos de convidado em seu [!DNL MBI] data warehouse.

## Impacto dos pedidos de convidado nos dados

No banco de dados de comércio típico, há um `orders` tabela que une a um `customers` tabela. Cada linha no `orders` a tabela tem um `customer\_id` coluna que é exclusiva a uma linha na `customers` tabela.

* **Se todos os clientes estiverem registrados** e pedidos de hóspedes não são permitidos, isso significa que cada registro no `orders` tem um valor na variável `customer\_id` coluna. Como resultado, cada pedido é associado ao `customers` tabela. Você pode ver isso na imagem abaixo.

   ![](../../assets/guest-orders-4.png)

* **Se os pedidos de convidado forem permitidos**, isso significa que alguns pedidos não têm um valor na variável `customer\_id` coluna. Somente clientes registrados recebem um valor para a variável `customer\_id` na coluna `orders` tabela. Os clientes que não estiverem registrados receberão uma `NULL` (ou em branco) para essa coluna. Como resultado, nem todos os registros de pedido terão registros correspondentes na variável `customers` tabela.

   >[!NOTE]
   >
   >Para identificar o indivíduo exclusivo que fez o pedido, precisa haver outro atributo de usuário exclusivo ao lado `customer\_id` anexado a um pedido. Normalmente, o endereço de email do cliente é usado.

## Como contabilizar pedidos de convidado na configuração do data warehouse

Normalmente, o Engenheiro de Vendas que implementa sua conta levará os pedidos de convidado em consideração ao criar a base do data warehouse.

A melhor maneira de contabilizar pedidos de convidado é basear todas as métricas no nível do cliente na `orders` tabela. Essa configuração usará uma ID exclusiva do cliente que todos os clientes possuem, incluindo convidados (normalmente, o email do cliente é usado). Isso ignora os dados de registro do `customers` tabela. Com essa opção, somente os clientes que fizeram pelo menos uma compra serão incluídos nos relatórios no nível do cliente. Usuários registrados que ainda não fizeram uma compra não serão incluídos. Com essa opção, seu `New customer` será baseada na data do primeiro pedido do cliente na variável `orders` tabela.

Você pode notar que a variável `Customers we count` o filtro definido nesse tipo de configuração tem um filtro para `Customer's order number = 1`. Vamos pensar no porquê disso.

![](../../assets/guest-orders-filter-set.png)

Em uma situação sem pedidos de convidado, cada cliente existe como uma linha única na tabela do cliente (consulte a Imagem 1). Uma métrica como `New customers` O pode simplesmente contar a id desta tabela com base em `created\_at` data para entender Novos clientes com base na data de registro.

Em uma configuração de pedidos de convidado, onde todas as métricas do cliente se baseiam na variável `orders` tabela para considerar pedidos de convidado, você precisa garantir que `not counting customers twice`. Se contar a id da tabela de pedidos, você estará contando cada pedido. Se, em vez disso, você contar a id no `orders` tabela e use um filtro, `Customer's order number = 1`, você contará cada cliente único `only one time`. Isso é aplicável para todas as métricas no nível do cliente, como `Customer's lifetime revenue` ou `Customer's lifetime number of orders`.

Na Imagem 2 acima, você pode ver que há um valor nulo `customer\_ids` no `orders` tabela. Se usarmos a variável `customer\_email` para identificar clientes únicos, é possível observar que `erin@test.com` fez três (3) pedidos. Portanto, podemos criar um `New customers` na sua métrica `orders` tabela com base nas seguintes condições:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
