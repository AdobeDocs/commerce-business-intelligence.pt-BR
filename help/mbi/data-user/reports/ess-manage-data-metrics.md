---
title: Métricas Criar
description: Aprenda a usar métricas para criar gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Métricas Criar

>[!NOTE]
>
>Requer [ permissões ](../../administrator/user-management/user-management.md) de administrador.

Uma métrica é uma medida. Nas estruturas SQL e banco de dados, um métrica é curtir um query armazenado durante um período variável.

No [!DNL Commerce Intelligence] , você pode usar métricas para [ criar gráficos ](../../data-user/reports/ess-rpt-build-visual.md) . Por exemplo, a métrica `revenue` é o número total de pedidos. O métrica `average customer revenue per order` é o que o cliente médio gasta por solicitar.

Quando usado em relatórios, as métricas podem ser analisadas em um período especificado e [ filtradas ou segmentadas ](../../best-practices/segment-filter.md) por categorias diferentes. Considere analisar o cliente médio receita agrupados por gênero-neste caso, `average customer revenue per order` o métrica e o gênero são o agrupamento.

## Definição da métrica {#define}

1. Para criar uma métrica, clique em **[!UICONTROL Data** > **Metrics]** .

1. Clique em **[!UICONTROL Create New Metric]** .

1. Na lista suspensa, clique na tabela que inclui a nativo ou a coluna calculada que deseja usar para o métrica.

1. Nomeie o métrica.

   Adobe Systems recomenda um nome que, em um relance, indique o que é o métrica. Por exemplo: `Average Order Revenue` .

1. A próxima etapa é definir o que a métrica faz. Usando os menus suspensos, defina a operação do métrica, a `operation` coluna e um `date` Dimensão:

   * Escolha uma operação:
      * `Count` -Esta operação conta o número de linhas em uma tabela de dados
      * `Max` -Max retorna o valor máximo de uma coluna de dados específica
      * `Min` -Min retorna o valor mínimo de uma coluna de dados específica
      * `Sum` -Esta operação soma os valores de uma coluna de dados específica
      * `Average` -Esta operação calcula a média dos valores da coluna de dados
      * `Count Distinct Value` -Isso conta o número exclusivo de valores em uma coluna de dados específica
      * `Median` -Esta operação calcula a mediana dos valores da coluna de dados
      * `First and Third Quartiles` -Essas operações calculam os 25 e 75 percentils dos valores da coluna de dados, respectivamente
      * `Tenth and Ninetieth Percentiles` -Essas operações calculam os 10º e 90th percentil dos valores da coluna de dados, respectivamente
   * Escolha uma coluna para executar a operação. Por exemplo, se você quisesse encontrar seu total receita, realizaria uma operação de soma na `order total` coluna.

      Se você estiver editando uma métrica existente, também [ poderá alterar a tabela ](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) operacional do métrica nessa seção.

   * Escolha uma data dimensão que possa ser usada para analisar a tendência da métrica. Por exemplo, `order date` .


## Adicionar filtros {#filters}

A `Filter` seção permite criar um filtro ou aplicar um [ conjunto ](../../data-user/reports/ess-manage-data-filters.md) de filtros salvo à métrica.

Para o `average order revenue` métrica, você não desejaria incluir pedidos de teste que possam ter sido feitos ao configurar o armazenamento-isso nos forneceria um resultado incorreto. Pode aplicar um conjunto de filtros para remover esses pedidos do conjunto de dados. Após a criação do filtro, ele será aplicado a todos os gráficos criados com essa métrica.

A `Filter Logic` seção é onde você pode definir mais como um métrica deve se comportar.

* &quot;\ [ `A` \] ou \ [ `B` \]&quot; permite que qualquer dado que satisfaça a filtros \ [ `A` \] ou \ [ `B` \]
* &quot;\ [ `A` \] e \ [ `B` \]&quot; só permite que os dados satisfaçam ambos filtros \ [ `A` \] e \ [ `B` \]
* &quot;(\ [ `A` \] e \ [ `B` \]) ou \ [ `C` \]&quot; só permite que os dados atendam apenas a filtros \ [ `A` \] e \ [ `B` \], ou satisfaçam o filtro \ [ `C` \] sozinho

## Adição de dimensões {#dimensions}

A [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) seção mostra todas as dimensões de dados disponíveis para filtragem ou agrupamento; por padrão, todas as colunas de dados disponíveis são listadas como dimensões. Continuando com o exemplo, se você quisesse segmento seu receita por referência fonte, é possível fazer isso aqui.

Além de listar todas as colunas de dados disponíveis como dimensões, [!DNL Commerce Intelligence] adivinhe em quais colunas são agrupadas. *Para segmento ou grupo dados em relatórios* , as colunas devem ser marcadas como agrupadas.

## Concluindo {#finish}

Além de definir como o métrica se comporta, você também pode definir níveis de permissão na `User Rights` seção. Embora `Admin` os usuários tenham acesso a todas as métricas, é necessário indicar os usuários que podem usar essa métrica marcando a caixa ao lado do grupo apropriado.

Se você estiver editando uma métrica existente, poderá visualização uma lista de gráficos (e quem as possui) que usam essa métrica na `Dependent Charts` seção.

As alterações são salvas automaticamente e o métrica agora é bom go.
