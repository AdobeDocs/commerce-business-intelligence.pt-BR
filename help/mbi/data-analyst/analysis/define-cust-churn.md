---
title: Definir churn do cliente
description: Saiba como configurar um painel que ajuda a definir a rotatividade para seus clientes transacionais.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Churn transacional do cliente

Este tópico demonstra como configurar um painel que ajuda a definir a rotatividade dos clientes transacionais.

![](../../assets/churn-deashboard.png)

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

Colunas para criar

* `customer_entity` tabela
* `Customer's lifetime number of orders`
* Selecione uma definição: `Count`
* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Pedidos contados

* `sales_flat_order` tabela
* `Customer's lifetime number of orders`
* Selecione uma definição: coluna unida
* Selecione um [!UICONTROL table]: `customer_entity`
* Selecione um [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Selecione uma definição: `Age`
* Selecione um [!UICONTROL column]: `created_at`

* **`Customer's order number`** O é criado por um analista como parte de sua **[DEFINIÇÃO DE CHURN]** tíquete
* **`Is customer's last order`** O é criado por um analista como parte de sua **[DEFINIÇÃO DE CHURN]** tíquete
* **`Seconds since previous order`** O é criado por um analista como parte de sua **[DEFINIÇÃO DE CHURN]** tíquete
* **`Months since order`** O é criado por um analista como parte de sua **[DEFINIÇÃO DE CHURN]** tíquete
* **`Months since previous order`** O é criado por um analista como parte de sua **[DEFINIÇÃO DE CHURN]** tíquete

## Métricas

Nenhuma métrica nova!

>[!NOTE]
>
>Verifique se [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Probabilidade de ordem de repetição inicial**
* Métrica A: Ordens de repetição Ocasionais
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: pedidos a todo momento
* [!UICONTROL Metric]: Número de pedidos

* [!UICONTROL Formula]: probabilidade inicial de ordem de repetição
* 
  [!UICONTROL Fórmula]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Probabilidade de ordem de repetição em determinados meses desde a ordem**
* Métrica A: repetir pedidos por meses desde o pedido anterior (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: últimos pedidos por meses desde o pedido (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Métrica C: ordens de repetição únicas (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 
  [!UICONTROL Agrupar por]: `Independent`

* Métrica D: Últimas encomendas pontuais (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 
  [!UICONTROL Agrupar por]: `Independent`

* [!UICONTROL Formula]: probabilidade inicial de ordem de repetição
* 
  [!UICONTROL Fórmula]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostrar top.bottom: As 24 principais categorias, classificadas por nome de categoria

* 
  [!UICONTROL Chart type]: `Line`

O relatório de probabilidade de ordem de repetição inicial representa o Total de Pedidos Repetidos/Total de Pedidos. Cada pedido é uma oportunidade para fazer um pedido repetido; o número de pedidos repetidos é o subconjunto daqueles que realmente fazem.

A fórmula usada simplifica para (Total de pedidos repetidos que ocorreram após X meses)/ (Total de pedidos que têm pelo menos X meses). Isso nos mostra que historicamente, dado que já se passaram X meses desde um pedido, há uma chance de Y% de o usuário colocar outro pedido.

Depois de criar o painel, a pergunta mais comum é: como usar isso para determinar um limite de churn?

**Não há &quot;uma resposta certa&quot; para isso.** No entanto, Adobe recomenda encontrar o ponto em que a linha cruza o valor que é metade da taxa de probabilidade de repetição inicial. Este é o ponto em que você pode dizer &quot;Se um usuário vai fazer uma ordem repetida, ele provavelmente já teria feito isso&quot;. Em última análise, o objetivo é selecionar o limite no qual faz sentido alternar de esforços de &quot;retenção&quot; para esforços de &quot;reativação&quot;.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior da página

Se você tiver dúvidas ao criar essa análise ou se quiser simplesmente envolver a equipe de serviços profissionais, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
