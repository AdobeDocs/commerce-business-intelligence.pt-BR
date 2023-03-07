---
title: Análise do valor vitalício esperado (LTV) (básico)
description: Saiba como criar análises para entender o valor vitalício dos clientes atuais e prever como esse valor aumenta com mais pedidos.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Análise do valor vitalício esperado

Prever o valor vitalício dos clientes à medida que fazem mais pedidos é um dos aspectos mais importantes de qualquer negócio de qualquer porte.

Estas são as etapas para criar análises para entender o valor vitalício dos clientes atuais e prever como esse valor aumenta com mais pedidos:

![valor vitalício esperado](../../assets/expected_ltv_720.png)

## Criar uma métrica

A primeira etapa é criar uma nova métrica com as seguintes etapas:
* Navegue até **[!UICONTROL Manage Data > Metrics]**
   * Visualizar o existente **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >A tabela em que essa métrica é construída (provavelmente `customer_entity` ou `sales_order` dependendo da capacidade da loja de aceitar o check-out do convidado.).

   * Clique em **[!UICONTROL Create New Metric]** e selecione a tabela acima.
   * Essa métrica executa uma **Mediana** no `Customer's lifetime revenue` coluna, ordenada por `created_at`.
      * [!UICONTROL Filters]:
         * Adicione o `Customers we count (Saved Filter Set)` (ou `Registered accounts we count`)
   * Nomeie a métrica, como `Median lifetime revenue`.



## Criar seu painel

Depois que a métrica é criada, é possível **criar um painel** fazendo isso:
* Navegue até **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Nomeie o painel como `Expected LTV`.

* É aqui que você cria e adiciona todos os relatórios.

## Criação de relatórios

>[!NOTE]
>
>Ligado **[!UICONTROL Time Period:]**, o período de tempo para cada relatório é listado como `All-time`. Altere isso para atender às suas necessidades de análise. Adobe recomenda que todos os relatórios desse painel cubram o mesmo período, como `All time`, `Year-to-date`ou `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Não Igual a** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Maior que**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL Tipo de gráfico]: `Line`
   * Desmarcar `Multiple Y-Axes`

* **LTV por número de ordens vitalícias**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL Tipo de gráfico]: `Line`
   >[!NOTE]
   >
   >Não adicione todos os valores de `Customer's lifetime number of orders`. Em vez disso, observe um ponto em que o número de Novos clientes atinge um número pequeno e adicione manualmente o número de vida útil de cada cliente do valor do pedido a esse ponto. Por exemplo, se houver 200 clientes em um pedido, 75 em dois, 15 em três e 3 em quatro, adicione *1, 2 e 3*.

* Adicionar o existente [!UICONTROL Avg customer lifetime revenue by cohort] relatório.

Depois de criar os relatórios, consulte a imagem na parte superior deste tópico para saber como organizar os relatórios em seu painel.
