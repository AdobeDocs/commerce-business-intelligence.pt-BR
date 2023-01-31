---
title: Análise do valor vitalício (LTV) esperado (básico)
description: Saiba como criar análises para entender o valor da vida útil de seus clientes atuais e prever como o valor da vida útil aumentará com mais pedidos.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Análise de valor vitalício esperada

Previsão do valor vitalício dos clientes à medida que eles colocam mais pedidos é um dos aspectos mais importantes de qualquer negócio de qualquer tamanho.

Estas são as etapas para criar análises para entender o valor da vida útil de seus clientes atuais e prever como o valor da vida útil aumentará com mais pedidos:

![valor vitalício esperado](../../assets/expected_ltv_720.png)

## Criar uma métrica

A primeira etapa será construir uma nova métrica com as seguintes etapas:
* Navegar para **[!UICONTROL Manage Data > Metrics]**
   * Visualize o **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >A tabela em que essa métrica é construída (provavelmente `customer_entity` ou `sales_order` dependendo da capacidade da sua loja de aceitar o check-out de convidado.).

   * Clique em **[!UICONTROL Create New Metric]** e selecione a tabela acima.
   * Essa métrica executa um **Mediana** no `Customer's lifetime revenue` coluna, ordenada por `created_at`.
      * [!UICONTROL Filters]:
         * Adicione o `Customers we count (Saved Filter Set)` ou `Registered accounts we count`)
   * Dê um nome à métrica, como `Median lifetime revenue`.



## Criar seu painel

Depois que a métrica tiver sido criada, é possível **criar um painel** ao fazer isso:
* Navegar para **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Dê um nome ao painel, como `Expected LTV`.

* Será aqui que criaremos e adicionaremos todos os relatórios.

## Criação de relatórios

* Caso ainda não tenha feito, faça check-out [este vídeo](https://fast.wistia.net/embed/iframe/24zz7wmjrt) sobre o uso do **[!UICONTROL Visual Report Builder] para criar gráficos, tabelas e valores escalares.

>[!NOTE]
>
>Ligado **[!UICONTROL Time Period:]**, o período de tempo de cada relatório é listado como `All-time`. Você pode alterar isso para atender às suas necessidades de análise. Recomendamos que todos os relatórios neste painel cubram o mesmo período de tempo, como `All time`, `Year-to-date`ou `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalo]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Adicionar [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Diferente de** `Not Logged In`
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

* **LTV por número de pedidos por duração**
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
   >Não adicione todos os valores para `Customer's lifetime number of orders`, em vez disso, verifique um ponto em que o número de Novos clientes atinge um número pequeno e adicione manualmente o número de vida útil de cada cliente do valor do pedido a esse ponto. Por exemplo, se houver 200 clientes em um pedido, 75 em dois, 15 em três e 3 em quatro, adicione *1, 2 e 3*.

* Adicione o [!UICONTROL Avg customer lifetime revenue by cohort] relatório.

Depois de criar os relatórios, consulte a imagem na parte superior deste tópico para saber como organizar os relatórios no painel.
