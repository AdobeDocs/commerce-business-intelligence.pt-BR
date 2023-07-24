---
title: Rastrear metas em relação a métricas
description: Saiba como configurar um painel que ajudará você a controlar suas metas comerciais em relação aos dados reais, incluindo a receita, os novos usuários registrados e os pedidos ao longo do tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Rastreamento De Metas Em Relação Às Métricas De Desempenho

A maioria dos clientes gostaria de rastrear seus **metas de negócios**, mas não percebam que isso é possível em [!DNL Adobe Commerce Intelligence]. Este tópico demonstra como configurar um painel que ajudará você a controlar suas metas de negócios em relação aos dados reais, incluindo receita, novos usuários registrados e pedidos ao longo do tempo. Você também aprenderá a comparar o desempenho ano a ano, tudo em um painel como este:

![](../../assets/Goals-_dashboard_2.png)

Antes de começar, você deve revisar o [carregador de arquivo](../importing-data/connecting-data/using-file-uploader.md) e certifique-se de ter definido suas metas comerciais para um determinado período.

## Introdução

Primeiro, faça upload de um arquivo contendo metas diárias/mensais/trimestrais específicas para sua empresa.

Você pode usar o [carregador de arquivo](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar o arquivo. Os alvos mais comuns que os clientes rastreiam [!DNL Commerce Intelligence] inclui Pedidos, Receita e Novas contas registradas.

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
* Ordenado por **`Month`** carimbo de data e hora

* **Público alvo mensal de novas contas registradas**
* No **`Monthly goals`** tabela
* Essa métrica executa uma **Sum**
* No **`New registered accounts target`** coluna
* Ordenado por **`Month`** carimbo de data e hora

## Relatórios

É útil ter uma combinação de valores estáticos e gráficos visuais ao analisar suas metas. Abaixo estão três relatórios de exemplo para começar a rastrear o desempenho da receita.

* **Receita restante para atingir o objetivo**
* Métrica `A`: `Revenue`
* 
  [!UICONTROL Métrica]: `Revenue`

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

* Métrica `C`: `Revenue (amount change since previous year)` (ocultar)
* 
  [!UICONTROL Métrica]: `Revenue`
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
