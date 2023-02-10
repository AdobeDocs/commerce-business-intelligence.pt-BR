---
title: Definir taxa de churn do cliente
description: Saiba como configurar um painel que ajudará você a definir o churn para seus clientes transacionais.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Abandono de cliente transacional

Neste artigo, demonstramos como configurar um painel que ajudará você a definir o churn para seus clientes transacionais.

![](../../assets/churn-deashboard.png)

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

Colunas a serem criadas

* `customer_entity` tabela
* `Customer's lifetime number of orders`
* Selecione uma definição: `Count`
* Selecione um [!UICONTROL table]: `sales_flat_order`
* Selecione um [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_plain_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Pedidos contados

* `sales_flat_order` tabela
* `Customer's lifetime number of orders`
* Selecione uma definição: Coluna unida
* Selecione um [!UICONTROL table]: `customer_entity`
* Selecione um [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Selecione uma definição: `Age`
* Selecione um [!UICONTROL column]: `created_at`

* **`Customer's order number`** será criado por um analista como parte de **[DEFINIÇÃO DE CHURN]** ticket
* **`Is customer's last order`** será criado por um analista como parte de **[DEFINIÇÃO DE CHURN]** ticket
* **`Seconds since previous order`** será criado por um analista como parte de **[DEFINIÇÃO DE CHURN]** ticket
* **`Months since order`** será criado por um analista como parte de **[DEFINIÇÃO DE CHURN]** ticket
* **`Months since previous order`** será criado por um analista como parte de **[DEFINIÇÃO DE CHURN]** ticket

## Métricas

Nenhuma métrica nova!

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Probabilidade de ordem de repetição inicial**
* Métrica A: Todas as ordens de repetição
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Todas as ordens de tempo
* [!UICONTROL Metric]: Número de pedidos

* [!UICONTROL Formula]: Probabilidade de ordem de repetição inicial
* 
   [!UICONTROL Fórmula]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Probabilidade de ordem de repetição fornecida meses desde a ordem**
* Métrica A: Repetir pedidos por meses desde a ordem anterior (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Últimos pedidos por meses desde o pedido (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Métrica C: Todas as ordens repetidas de tempo (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Agrupar por]: `Independent`

* Métrica D: Todas as últimas ordens de tempo (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Agrupar por]: `Independent`

* [!UICONTROL Formula]: Probabilidade de ordem de repetição inicial
* 
   [!UICONTROL Fórmula]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostrar top.bottom: 24 categorias principais, classificadas por nome de categoria

* 

   [!UICONTROL Chart type]: `Line`

O relatório de probabilidade da ordem de repetição inicial representa o Total de Pedidos de Repetição / Total de Pedidos. Cada ordem é uma oportunidade para fazer uma ordem repetida; o número de pedidos repetidos é o subconjunto daqueles que realmente fazem isso.

A fórmula usada simplifica para (Total de pedidos repetidos que ocorreram após X meses)/ (Total de pedidos que têm pelo menos X meses). Isso nos mostra que historicamente, visto que há X meses desde um pedido, há uma chance de Y% de o usuário colocar outro pedido.

Depois de criar seu painel, a pergunta mais comum que recebemos é: Como usar isso para determinar um limite de abandono?

**Não há &quot;uma resposta certa&quot; para isto.** No entanto, recomendamos encontrar o ponto em que a linha cruza o valor que é metade da taxa de probabilidade de repetição inicial. Este é o ponto onde podemos dizer &quot;Se um usuário fizesse um pedido repetido, provavelmente já o teriam feito.&quot; Em última análise, o objetivo é selecionar o limite onde faz sentido alternar de esforços de &quot;retenção&quot; para &quot;reativação&quot;.

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior da página

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
