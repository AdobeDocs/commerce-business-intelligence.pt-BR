---
title: Rastreamento de metas em relação às métricas
description: Aprenda a configurar um painel que ajudará a faixa suas metas de negócios em relação aos dados reais-incluindo receita, novos usuários registrados e pedidos ao longo do tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Rastreamento de metas em relação às métricas de desempenho

A maioria dos clientes curtir a faixa suas **metas** de negócios, mas não é possível perceber que isso é possível em [!DNL Adobe Commerce Intelligence] . Este tópico demonstra como configurar um painel que ajudará você a faixa suas metas de negócios em relação aos dados reais-incluindo receita, novos usuários registrados e pedidos ao longo do tempo. Você também aprenderá a comparar o desempenho ano a ano, tudo em um painel como este:

![](../../assets/Goals-_dashboard_2.png)

Antes de começar, você deve analisar o carregador ](../importing-data/connecting-data/using-file-uploader.md) de [ arquivos e certificar-se de ter definido suas metas de negócios para determinado período.

## Introdução

Você precisa primeiro upload um arquivo contendo metas diárias/mensais/trimestrais específicas para sua empresa.

Você pode usar o carregador ](../importing-data/connecting-data/using-file-uploader.md) de [ arquivos e a imagem abaixo para formatar o arquivo. Os alvos mais comuns que os clientes faixa [!DNL Commerce Intelligence] incluem pedidos, receita e novo contas registradas.

![](../../assets/Goals-_Excel.png)

## Métricas

Crie uma nova métrica para cada target. Por exemplo, se você fizer upload dos destinos mensais de receita e pedidos, será necessário criar duas novas métricas:

* **Meta de receita mensal**
* No **`Monthly goals`** tabela
* Essa métrica executa uma **Sum**
* No **`Revenue target`** coluna
* Ordenado por **`Month`** carimbo de data e hora

* **Público alvo de pedidos mensal**
* No **`Monthly goals`** tabela
* Essa métrica executa uma **Sum**
* No **`Orders target`** coluna
* Solicitado pelo carimbo de **`Month`** data e hora

* **Contas novas e mensais Direcionamento**
* **`Monthly goals`** Na tabela
* Este métrica executa uma **soma**
* **`New registered accounts target`** Na coluna
* Ordenado por **`Month`** carimbo de data e hora

## Relatórios

É útil ter uma mistura de valores estáticos e gráficos visuais ao analisar seus destinos. Abaixo estão três relatórios de exemplo para ajudá-lo a começar a rastreamento o desempenho da receita.

* **Receita restante para atingir Direcionamento**
* Métrica `A` : `Revenue`
* 

   [! Métrica UICONTROL]: `Revenue`

* Métrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL Fórmula]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (qualquer período relevante que você desejar)
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Metas de receita**
* Métrica `A`: `Revenue`
* 

   [!UICONTROL Métrica]: `Revenue`

* Métrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Métrica `C` : `Revenue (amount change since previous year)` (ocultar)
* 
   [! Métrica UICONTROL]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Este mês no ano passado)
* 
   [!UICONTROL Fórmula]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* Desativar `Multiple Y-Axes`
* [!UICONTROL Time period]: (qualquer período relevante que você desejar)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Depois de concluir os relatórios acima para metas de receita, você pode criar relatórios idênticos para metas sobre pedidos, contas registradas ou quaisquer outros valores incluídos no upload do arquivo de metas.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior desta página.
