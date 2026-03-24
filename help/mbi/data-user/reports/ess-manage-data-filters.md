---
title: Criar conjuntos de filtros para métricas
description: Saiba como criar Conjuntos de filtros salvos e aplicá-los às métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Y3SA-ypB62c0mwZ6uqAOQUyrISc5Tu8yqClrGwXspoU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# Criar conjuntos de filtros

Se você tiver várias métricas em [!DNL Commerce Intelligence] que precisam ser filtradas de maneira semelhante (por exemplo, filtrar ordens de teste), poderá criar Conjuntos de Filtros salvos e aplicá-los às métricas. Isso economiza tempo, pois não é necessário adicionar filtros individuais ao criar ou editar uma métrica.

Consulte o [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) para obter mais informações.

>[!NOTE]
>
>Requer [permissões de administrador](../../administrator/user-management/user-management.md).

1. Clique em **[!DNL Manage Data** > **Filter Sets]** na barra lateral.

   ![Criar interface de conjuntos de filtros com opção adicionar conjunto de filtros](../../assets/create-filter-sets.png)

1. Clique em **[!UICONTROL Add Filter Set]** na parte superior da página.

1. Selecione a tabela que contém as métricas que você deseja filtrar.

   Por exemplo, se você deseja filtrar sua métrica `Total number of orders` e ela está incorporada na tabela `orders`, selecione essa tabela.

1. Nomeie o `Filter Set`.

1. Adicione todos os filtros relevantes.

   Por exemplo, se você quiser incluir apenas pedidos com status de concluído na métrica `Total number of orders`, você aplicará um filtro que exclui todos os pedidos que não têm status = `complete`.

1. Verifique a lógica do filtro e se os parênteses e operadores estão posicionados corretamente: por exemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Um filtro incorreto geralmente é a causa das discrepâncias de dados entre os relatórios do [!DNL Commerce Intelligence] e os resultados esperados.

1. Salve o `Filter Set`.

Depois que um conjunto de filtros é salvo, é possível aplicá-lo a qualquer métrica que esteja usando a mesma tabela. Por exemplo, se você criou uma `Filter Set` na tabela `orders`, é possível aplicá-la a *qualquer métrica* criada nessa tabela, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` também pode ser aplicado às colunas calculadas em [!DNL Commerce Intelligence]. Você pode solicitar a aplicação de um conjunto de filtros a uma dimensão de dados criada em [!DNL Commerce Intelligence] via entrando em contato com o suporte.

## Relacionados

* [Práticas recomendadas para segmentação e filtragem](../../best-practices/segment-filter.md)
