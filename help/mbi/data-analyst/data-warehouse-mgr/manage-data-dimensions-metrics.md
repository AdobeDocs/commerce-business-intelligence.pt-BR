---
title: Gerenciamento de dimensões de dados
description: Saiba o que é uma dimensão e ela pode ser usada para filtrar ou segmentar gráficos com base em uma métrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Gerenciamento de dimensões de dados

>[!NOTE]
>
>Requer [permissões de administrador](../../administrator/user-management/user-management.md).

Uma dimensão é um campo na mesma tabela que uma métrica que pode ser usada para filtrar ou segmentar gráficos com base nessa métrica. Por exemplo, uma métrica de receita pode conter cidade, estado, país, status de pedido, código de cupom e outros tipos de dimensões.

## Adicionar dimensões a várias métricas

Para adicionar uma ou mais dimensões a várias métricas de uma só vez:

1. Ir para **[!UICONTROL Manage Data > Metrics]**.

1. Clique em **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Escolha a tabela que contém as dimensões.

1. Na coluna `Choose Metric(s) to Add Dimensions`, selecione as métricas às quais deseja adicionar dimensões. Depois de selecionada, a coluna `Choose Dimensions to Add` aparece à direita. Marque as dimensões que deseja adicionar à métrica selecionada.

   ![Caixa de diálogo Adicionar Dimensões mostrando as opções de dimensão disponíveis](../../assets/Add_Dimensions.png)

1. Se você quiser segmentar ou agrupar por qualquer uma das dimensões de dados nos relatórios, certifique-se de indicar que elas são _Agrupáveis_.

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

1. Clique em **[!UICONTROL Edit]** na métrica desejada para uma nova dimensão.

1. Na seção `Dimensions`, use a lista suspensa `Add a dimension` para selecionar uma dimensão a ser adicionada.

>[!NOTE]
>
>Qualquer dimensão pela qual você deseja filtrar ou agrupar já deve estar rastreada em [!DNL Commerce Intelligence]. Se você não encontrar a dimensão desejada, talvez precise começar a rastrear uma nova coluna de dados no banco de dados por meio da página [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).


**Para excluir dimensões de uma métrica:**

1. Ir para **[!UICONTROL Manage Data > Metrics]**.

1. Clique em **[!UICONTROL Edit]** na métrica desejada para uma nova dimensão.

1. Na seção `Dimensions`, marque a caixa de seleção na coluna de exclusão ao lado da(s) dimensão(ões) que deseja remover.

>[!NOTE]
>
>Mesmo depois de excluir uma dimensão, ela ainda existe como uma coluna na tabela no Data Warehouse. Você pode adicioná-la novamente a qualquer métrica e criar novas métricas usando essas dimensões. Para remover a coluna de dados à qual uma dimensão corresponde de [!DNL Commerce Intelligence], basta desfazer o rastreamento da coluna de dados por meio da página [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).

## Documentação relacionada

* [Práticas recomendadas para segmentação e filtragem](../../best-practices/segment-filter.md)
