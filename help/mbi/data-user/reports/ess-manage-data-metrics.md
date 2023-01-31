---
title: Criar métricas
description: Saiba como usar métricas para criar gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Criar métricas

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).

Simplificando, uma métrica é uma medida. Em estruturas de banco de dados e SQL, uma métrica é como uma consulta armazenada em um período de tempo variável.

Em [!DNL MBI], você pode usar as métricas para [criar gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por exemplo, a métrica `revenue` é a quantidade total de ordens. A métrica `average customer revenue per order` é o que o cliente médio gasta por pedido.

Quando usadas em relatórios, as métricas podem ser analisadas ao longo de um período de tempo especificado e [filtrado ou segmentado](../../best-practices/segment-filter.md) por categorias diferentes. Considere analisar a receita média do cliente agrupada por gênero - nesse caso, `average customer revenue per order` é a métrica e gênero é o agrupamento.

## Definição da métrica {#define}

1. Para criar uma nova métrica, clique em **[!UICONTROL Data** > **Metrics]**.

1. Clique em **[!UICONTROL Create New Metric]**.

1. Na lista suspensa, clique na tabela que inclui a coluna nativa ou calculada que deseja usar para sua métrica.

1. Nomeie sua métrica.

   Recomendamos um nome que, de relance, informe o que é a métrica. Por exemplo: `Average Order Revenue`.

1. A próxima etapa é definir o que sua métrica faz. Usando os menus suspensos, defina a operação da métrica, a `operation` e uma `date` dimensão:

   * Escolha uma operação :
      * `Count` - Essa operação conta o número de linhas em uma tabela de dados
      * `Max` - Max retorna o valor máximo de uma coluna de dados específica
      * `Min` - Min retorna o valor mínimo de uma coluna de dados específica
      * `Sum` - Essa operação soma os valores de uma coluna de dados específica
      * `Average` - Essa operação calcula a média dos valores da coluna de dados
      * `Count Distinct Value` - Conta o número exclusivo de valores em uma coluna de dados específica
      * `Median` - Esta operação calcula a mediana dos valores da coluna de dados
      * `First and Third Quartiles` - Estas operações calculam os percentis 25 e 75 dos valores da coluna de dados, respectivamente
      * `Tenth and Ninetieth Percentiles` - Estas operações calculam os percentis 10 e 90 dos valores da coluna de dados, respectivamente
   * Escolha uma coluna na qual executar a operação. Por exemplo, se você quiser encontrar sua receita total, você executaria uma operação de soma na variável `order total` coluna.

      Se você estiver editando uma métrica existente, também poderá [alterar a tabela operacional da métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) nesta seção.

   * Escolha uma dimensão de data que possa ser usada para analisar a tendência da métrica. Por exemplo, `order date`.


## Adicionar filtros {#filters}

O `Filter` seção permite criar um novo filtro ou aplicar um [conjunto de filtros salvo](../../data-user/reports/ess-manage-data-filters.md) para sua métrica.

Para nosso `average order revenue` métrica, não gostaríamos de incluir quaisquer pedidos de teste que pudessem ter sido feitos durante a configuração de nossa loja - isso nos daria um resultado impreciso. Podemos aplicar um conjunto de filtros para remover esses pedidos do conjunto de dados. Depois que o filtro for criado, ele será aplicado a todos os gráficos criados usando essa métrica.

O `Filter Logic` é onde você pode definir mais detalhadamente como uma métrica deve se comportar.

* &quot;\[`A`\] ou \[`B`\]&quot; permitirá dados que atendam aos filtros \[`A`\] OU \[`B`\]
* &quot;\[`A`\] e \[`B`\]&quot; permitirá somente dados que satisfaçam ambos os filtros \[`A`\] e \[`B`\]
* &quot;(\[`A`\] e \[`B`\] OU \[`C`\]&quot; permitirá somente dados que atendam a ambos os filtros \[`A`\] e \[`B`\] ou filtro de satisfação \[`C`\] sozinho

## Adicionar Dimension {#dimensions}

O [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) mostra todas as dimensões de dados disponíveis para filtragem ou agrupamento; por padrão, todas as colunas de dados disponíveis são listadas como dimensões. Continuando com nosso exemplo, se quisermos segmentar nossa receita por fonte de referência, poderemos fazer isso aqui.

Além de listar todas as colunas de dados disponíveis como dimensões, [!DNL MBI] O também visualizará quais colunas são agrupáveis. *Para segmentar ou agrupar dados em relatórios*, as colunas devem ser marcadas como agrupáveis.

## Concluindo {#finish}

Além de definir o comportamento da sua métrica, você também pode definir níveis de permissão no `User Rights` seção. Ao `Admin` Se os usuários tiverem acesso a todas as métricas, será necessário indicar os usuários que podem usar essa métrica marcando a caixa ao lado do grupo apropriado.

Se você estiver editando uma métrica existente, poderá exibir uma lista de gráficos (e de quem possui) que utilizam essa métrica na variável `Dependent Charts` seção.

As alterações são salvas automaticamente e sua métrica agora está boa.
