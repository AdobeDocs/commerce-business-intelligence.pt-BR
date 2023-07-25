---
title: Criar conjuntos de filtros para métricas
description: Saiba como criar Conjuntos de filtros salvos e aplicá-los às métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Criar conjuntos de filtros

Se você tiver várias métricas no [!DNL Commerce Intelligence] que precisam ser filtrados de uma maneira semelhante (por exemplo, filtrar ordens de teste), é possível criar Conjuntos de filtros salvos e aplicá-los às métricas. Isso economiza tempo, pois não é necessário adicionar filtros individuais ao criar ou editar uma métrica.

Consulte a [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) para obter mais informações.

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

1. Clique em **[!DNL Manage Data** > **Filter Sets]** na barra lateral.

   ![](../../assets/create-filter-sets.png)

1. Clique em **[!UICONTROL Add Filter Set]** na parte superior da página.

1. Selecione a tabela que contém as métricas que você deseja filtrar.

   Por exemplo, se você deseja filtrar seu `Total number of orders` e é criada no `orders` selecione essa tabela.

1. Nomeie o `Filter Set`.

1. Adicione todos os filtros relevantes.

   Por exemplo, se você quiser incluir apenas pedidos com um status de concluído em seu `Total number of orders` , você aplicaria um filtro que exclui todos os pedidos que não têm status = `complete`.

1. Verifique a lógica do filtro e se os parênteses e operadores estão colocados corretamente: por exemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Um filtro incorreto geralmente é a causa das discrepâncias de dados entre [!DNL Commerce Intelligence] relatórios e os resultados esperados.

1. Salve o `Filter Set`.

Depois que um conjunto de filtros é salvo, é possível aplicá-lo a qualquer métrica que esteja usando a mesma tabela. Por exemplo, se você criou um `Filter Set` no `orders` tabela, é possível aplicá-la a *qualquer métrica* criado nessa tabela, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` também pode ser aplicado a colunas calculadas em [!DNL Commerce Intelligence]. Você pode solicitar a aplicação de um conjunto de filtros a uma dimensão de dados criada no [!DNL Commerce Intelligence] via entrando em contato com o suporte.

## Relacionados

* [Práticas recomendadas para segmentação e filtragem](../../best-practices/segment-filter.md)
