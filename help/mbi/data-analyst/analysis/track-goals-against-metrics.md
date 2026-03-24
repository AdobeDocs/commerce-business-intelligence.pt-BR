---
title: Rastrear metas em relação a métricas
description: Saiba como configurar um painel que ajudará você a controlar suas metas comerciais em relação aos dados reais, incluindo a receita, os novos usuários registrados e os pedidos ao longo do tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
TQID: https://experienceleague.adobe.com/gT-FJxqVg3X9fuXe-4kWErttYJ6qSMD4eqNvOITNNtQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Rastreamento De Metas Em Relação Às Métricas De Desempenho

A maioria dos clientes gostaria de acompanhar suas **metas comerciais**, mas não percebe que isso é possível em [!DNL Adobe Commerce Intelligence]. Este tópico demonstra como configurar um painel que ajudará você a controlar suas metas de negócios em relação aos dados reais, incluindo receita, novos usuários registrados e pedidos ao longo do tempo. Você também aprenderá a comparar o desempenho ano a ano, tudo em um painel como este:

![Painel mostrando o rastreamento de metas em relação ao desempenho real das métricas](../../assets/Goals-_dashboard_2.png)

Antes de começar, você deve revisar o [carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e verificar se definiu suas metas comerciais para um determinado período.

## Introdução

Primeiro, faça upload de um arquivo contendo metas diárias/mensais/trimestrais específicas para sua empresa.

Você pode usar o [carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar o arquivo. Os destinos mais comuns que os clientes monitoram em [!DNL Commerce Intelligence] incluem Pedidos, Receita e Novas contas registradas.

![Modelo de planilha do Excel para métricas e metas de rastreamento](../../assets/Goals-_Excel.png)

## Métricas

Crie uma nova métrica para cada target. Por exemplo, se você fizer upload dos destinos mensais de receita e pedidos, será necessário criar duas novas métricas:

* **Meta de receita mensal**
* Na tabela **`Monthly goals`**
* Esta métrica executa uma **Soma**
* Na coluna **`Revenue target`**
* Ordenado pelo carimbo de data/hora **`Month`**

* **Destino de pedidos mensais**
* Na tabela **`Monthly goals`**
* Esta métrica executa uma **Soma**
* Na coluna **`Orders target`**
* Ordenado pelo carimbo de data/hora **`Month`**

* **Público alvo mensal de novas contas registradas**
* Na tabela **`Monthly goals`**
* Esta métrica executa uma **Soma**
* Na coluna **`New registered accounts target`**
* Ordenado pelo carimbo de data/hora **`Month`**

## Relatórios

É útil ter uma combinação de valores estáticos e gráficos visuais ao analisar suas metas. Abaixo estão três relatórios de exemplo para começar a rastrear o desempenho da receita.

* **Receita restante para atingir o destino**
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

* [!UICONTROL Time period]: (Qualquer período de tempo relevante que você desejar)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL Tipo de gráfico]: `Scalar`

* **Destinos de receita**
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

* Desligar `Multiple Y-Axes`
* [!UICONTROL Time period]: (Qualquer período relevante que você desejar)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Depois de concluir os relatórios acima para metas de receita, você pode criar relatórios idênticos para metas sobre pedidos, contas registradas ou quaisquer outros valores incluídos no upload do arquivo de metas.

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior desta página.
