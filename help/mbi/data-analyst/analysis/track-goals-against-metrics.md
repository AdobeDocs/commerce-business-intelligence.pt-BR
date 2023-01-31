---
title: Rastreamento de metas em relação a métricas
description: Saiba como configurar um painel que ajudará você a rastrear suas metas comerciais em relação aos dados reais, incluindo receita, novos usuários registrados e pedidos ao longo do tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Rastreamento de metas em relação às métricas de desempenho

Uma grande maioria de nossos clientes geralmente gostaria de rastrear seus **objetivos de negócios**, mas não percebam que isso é possível em [!DNL MBI]. Neste artigo, demonstramos como configurar um painel que ajudará você a rastrear suas metas comerciais em relação aos dados reais, incluindo receita, novos usuários registrados e pedidos ao longo do tempo. Também mostramos como comparar o desempenho ano após ano, tudo em um painel como este:

![](../../assets/Goals-_dashboard_2.png)

Antes de começar, você quer se familiarizar com nossas [carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e certifique-se de ter definido suas metas de negócios por um determinado período.

## Introdução

Primeiro, será necessário fazer upload de um arquivo contendo metas específicas diárias/mensais/trimestrais para sua empresa.

Você pode usar o [carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar o arquivo. Os alvos mais comuns que nossos clientes rastreiam [!DNL MBI] incluir Pedidos, Receita e Novas contas registradas.

![](../../assets/Goals-_Excel.png)

## Métricas

É necessário criar uma nova métrica para cada target. Por exemplo, se você fizer upload das metas de receita e pedidos mensais, será necessário criar duas novas métricas:

* **Objetivo de receita mensal**
* No **`Monthly goals`** tabela
* Essa métrica executa um **Soma**
* No **`Revenue target`** column
* Solicitado pela **`Month`** timestamp

* **Objetivo das ordens mensais**
* No **`Monthly goals`** tabela
* Essa métrica executa um **Soma**
* No **`Orders target`** column
* Solicitado pela **`Month`** timestamp

* **Objetivo para novas contas registradas mensais**
* No **`Monthly goals`** tabela
* Essa métrica executa um **Soma**
* No **`New registered accounts target`** column
* Solicitado pela **`Month`** timestamp

## Relatórios

Como sempre, é útil ter uma combinação de valores estáticos e gráficos visuais ao analisar seus destinos. Abaixo estão três exemplos de relatórios para começar a rastrear o desempenho da receita.

* **Receita restante para atingir o target**
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

* [!UICONTROL Time period]: (Qualquer período relevante que você desejar)
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

* Desligar `Multiple Y-Axes`
* [!UICONTROL Time period]: (Qualquer período relevante que você desejar)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Após concluir os relatórios acima para alvos de receita, você pode criar relatórios idênticos para metas em pedidos, contas registradas ou quaisquer outros valores incluídos no upload de arquivo de metas.

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior desta página.
