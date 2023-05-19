---
title: Criar métricas
description: Saiba como usar métricas para criar gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Criar métricas

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

Uma métrica é uma medida. Em estruturas SQL e de banco de dados, uma métrica é como uma consulta armazenada em um período variável.

Entrada [!DNL Commerce Intelligence], você pode usar métricas para [criar gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por exemplo, a métrica `revenue` é o número total de pedidos. A métrica `average customer revenue per order` é o que o cliente médio gasta por pedido.

Quando usadas em relatórios, as métricas podem ser analisadas por um período específico e [filtrado ou segmentado](../../best-practices/segment-filter.md) por categorias diferentes. Considere analisar a receita média do cliente agrupada por gênero - neste caso, `average customer revenue per order` é a métrica e gênero é o agrupamento.

## Definição da métrica {#define}

1. Para criar uma métrica, clique em **[!UICONTROL Data** > **Metrics]**.

1. Clique em **[!UICONTROL Create New Metric]**.

1. Na lista suspensa, clique na tabela que inclui a coluna nativa ou calculada que deseja usar para sua métrica.

1. Nomeie sua métrica.

   Adobe recomenda um nome que informa qual é a métrica. Por exemplo: `Average Order Revenue`.

1. A próxima etapa é definir o que sua métrica faz. Usando os menus suspensos, defina a operação da métrica, a variável `operation` e uma `date` dimensão:

   * Escolha uma operação:
      * `Count` - Essa operação conta o número de linhas em uma tabela de dados
      * `Max` - Max retorna o valor máximo de uma coluna de dados específica
      * `Min` - Mín retorna o valor mínimo de uma coluna de dados específica
      * `Sum` - Essa operação soma os valores de uma coluna de dados específica
      * `Average` - Essa operação calcula a média dos valores da coluna de dados
      * `Count Distinct Value` - Isso conta o número exclusivo de valores em uma coluna de dados específica
      * `Median` - Essa operação calcula a mediana dos valores da coluna de dados
      * `First and Third Quartiles` - Essas operações calculam os percentis 25 e 75 dos valores da coluna de dados, respectivamente.
      * `Tenth and Ninetieth Percentiles` - Essas operações calculam os percentis 10 e 90 dos valores da coluna de dados, respectivamente.
   * Escolha uma coluna na qual executar a operação. Por exemplo, se você quisesse encontrar sua receita total, executaria uma operação de soma na variável `order total` coluna.

      Se você estiver editando uma métrica existente, também poderá [alterar a tabela operacional da métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) nesta seção.

   * Escolha uma dimensão de data que possa ser usada para analisar a tendência da métrica. Por exemplo, `order date`.


## Adição de filtros {#filters}

A variável `Filter` permite criar um filtro ou aplicar um [conjunto de filtros salvo](../../data-user/reports/ess-manage-data-filters.md) para sua métrica.

Para o `average order revenue` , você não desejaria incluir pedidos de teste que poderiam ter sido feitos durante a configuração de sua loja, isso nos daria um resultado impreciso. É possível aplicar um conjunto de filtros para remover esses pedidos do conjunto de dados. Depois que o filtro for criado, ele será aplicado a todos os gráficos criados usando essa métrica.

A variável `Filter Logic` é onde você pode definir melhor como uma métrica deve se comportar.

* &quot;\[`A`\] ou \[`B`\]&quot; permite quaisquer dados que satisfaçam aos filtros \[`A`\] OU \[`B`\]
* &quot;\[`A`\] e \[`B`\]&quot; permite somente dados que satisfaçam a ambos os filtros \[`A`\] e \[`B`\]
* &quot;(\[`A`\] e \[`B`\]) OU \[`C`\]&quot; permite somente dados que satisfaçam a ambos os filtros \[`A`\] e \[`B`\], ou satisfaz o filtro \[`C`\] sozinho

## Adicionar Dimension {#dimensions}

A variável [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) A seção mostra todas as dimensões de dados disponíveis para filtragem ou agrupamento; por padrão, todas as colunas de dados disponíveis são listadas como dimensões. Continuando com o exemplo, se você quiser segmentar sua receita por fonte de referência, faça isso aqui.

Além de listar todas as colunas de dados disponíveis como dimensões, [!DNL Commerce Intelligence] adivinha quais colunas podem ser agrupadas. *Para segmentar ou agrupar dados em relatórios*, as colunas devem ser marcadas como agrupáveis.

## Terminando {#finish}

Além de definir como sua métrica se comporta, você também pode definir níveis de permissão na variável `User Rights` seção. Enquanto `Admin` Se os usuários tiverem acesso a todas as métricas, será necessário indicar os usuários que podem usar essa métrica marcando a caixa ao lado do grupo apropriado.

Se você estiver editando uma métrica existente, poderá exibir uma lista de gráficos (e quem é o proprietário deles) que usam essa métrica na `Dependent Charts` seção.

As alterações são salvas automaticamente e sua métrica está pronta para ser usada.
