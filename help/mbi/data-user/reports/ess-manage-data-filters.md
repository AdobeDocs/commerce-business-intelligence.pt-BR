---
title: Criar conjuntos de filtros para métricas
description: Saiba como criar Conjuntos de filtros salvos e aplicá-los às métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Criar conjuntos de filtros

Se você tiver várias métricas em [!DNL MBI] que precisam ser filtrados de maneira semelhante (por exemplo, filtrar pedidos de teste), você pode criar Conjuntos de filtros salvos e aplicá-los às métricas. Isso economiza tempo, pois não é necessário adicionar filtros individuais ao criar ou editar uma métrica.

Veja nossa [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) para saber mais.

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

1. Clique em **[!DNL Manage Data** > **Filter Sets]** na barra lateral.

   ![](../../assets/create-filter-sets.png)

1. Clique em **[!UICONTROL Add Filter Set]** na parte superior da página.

1. Selecione a tabela que contém as métricas que deseja filtrar.

   Por exemplo, se você deseja filtrar o `Total number of orders` e é criada na variável `orders` selecione essa tabela.

1. Nomeie a função `Filter Set`.

1. Adicione todos os filtros relevantes.

   Por exemplo, se quisermos incluir apenas pedidos com um status de concluído em nossa `Total number of orders` métrica, aplicamos um filtro que exclui todos os pedidos que não têm status = `complete`.

1. Verifique a lógica de filtro e se os parênteses e operadores estão colocados corretamente: por exemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Um filtro incorreto geralmente é a causa das discrepâncias de dados entre [!DNL MBI] e seus resultados esperados.

1. Salve as `Filter Set`.

Depois que um conjunto de filtros é salvo, você pode aplicá-lo a qualquer métrica que esteja usando a mesma tabela. Por exemplo, se você criou uma `Filter Set` no `orders` tabela, você pode aplicá-la a *qualquer métrica* criado nessa tabela, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` também pode ser aplicado a colunas calculadas em [!DNL MBI]. Você pode solicitar a aplicação de um conjunto de filtros a uma dimensão de dados criada em [!DNL MBI] por meio do , entrando em contato com o suporte do .

## Relacionado

* [Práticas recomendadas para segmentação e filtragem](../../best-practices/segment-filter.md)
