---
title: Gerenciamento de dimensões de dados
description: Saiba o que é uma dimensão e ela pode ser usada para filtrar ou segmentar gráficos com base em uma métrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Gerenciamento de dimensões de dados

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

Uma dimensão é um campo na mesma tabela que uma métrica que pode ser usada para filtrar ou segmentar gráficos com base nessa métrica. Por exemplo, uma métrica de receita pode conter cidade, estado, país, status de pedido, código de cupom e outros tipos de dimensões.

## Adicionar dimensões a várias métricas

Para adicionar uma ou mais dimensões a várias métricas de uma só vez:

1. Ir para **[!UICONTROL Manage Data > Metrics]**.

1. Clique em **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Escolha a tabela que contém as dimensões.

1. No `Choose Metric(s) to Add Dimensions` , selecione as métricas às quais deseja adicionar dimensões. Uma vez selecionado, o `Choose Dimensions to Add` é exibida à direita. Marque as dimensões que deseja adicionar à métrica selecionada.

   ![](../../assets/Add_Dimensions.png)

1. Se você quiser segmentar ou agrupar por qualquer uma das dimensões de dados nos relatórios, certifique-se de indicar que elas são _Agrupável_.

1. Clique em **[!UICONTROL Add]**.

## Excluir dimensões de várias métricas

Para excluir uma ou mais dimensões de várias métricas:

1. Ir para **[!UICONTROL Data > Metrics]**.

1. Clique em **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Escolha a tabela que contém as dimensões.

1. Selecione as métricas das quais você deseja remover as dimensões à esquerda e as dimensões que você deseja remover à direita.

1. Clique em **[!UICONTROL Remove]**.

1. Se as dimensões estiverem em uso em relatórios, um aviso será exibido com a lista de gráficos que estão usando as dimensões. Clique em **[!UICONTROL Delete]** para excluir as dimensões marcadas e todos os seus dependentes, incluindo relatórios.

## Gerenciar dimensões em métricas

**Para adicionar dimensões em uma métrica:**

1. Ir para **[!UICONTROL Data > Metrics]**.

1. Clique em **[!UICONTROL Edit]** na métrica que deseja uma nova dimensão.

1. No `Dimensions` , use o `Add a dimension` selecione uma dimensão para adicionar.

>[!NOTE]
>
>Qualquer dimensão pela qual você deseja filtrar ou agrupar já deve estar rastreada [!DNL Commerce Intelligence]. Se não encontrar a dimensão desejada, talvez seja necessário começar a rastrear uma nova coluna de dados no banco de dados por meio da [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) página.


**Para excluir dimensões de uma métrica:**

1. Ir para **[!UICONTROL Manage Data > Metrics]**.

1. Clique em **[!UICONTROL Edit]** na métrica que deseja uma nova dimensão.

1. No `Dimensions` marque a caixa de seleção na coluna excluir ao lado da(s) dimensão(ões) que deseja remover.

>[!NOTE]
>
>Mesmo depois de excluir uma dimensão, ela ainda existe como uma coluna na tabela na Data Warehouse. Você pode adicioná-la novamente a qualquer métrica e criar novas métricas usando essas dimensões. Para remover a coluna de dados à qual uma dimensão corresponde [!DNL Commerce Intelligence], basta desfazer o rastreamento da coluna de dados por meio da [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) página.

## Documentação relacionada

* [Práticas recomendadas para segmentação e filtragem](../../best-practices/segment-filter.md)
