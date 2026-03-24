---
title: Criar métricas
description: Saiba como usar métricas para criar gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xPbHndhmDdKugylEyPC3yXwMQHHF7FdMvJI7ZNDk-Yo
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 612
ht-degree: 0%

---

# Criar métricas

>[!NOTE]
>
>Requer [permissões de administrador](../../administrator/user-management/user-management.md).

Uma métrica é uma medida. Em estruturas SQL e de banco de dados, uma métrica é como uma consulta armazenada em um período variável.

Em [!DNL Commerce Intelligence], você pode usar métricas para [criar gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por exemplo, a métrica `revenue` é o número total de pedidos. A métrica `average customer revenue per order` é o que o cliente médio gasta por pedido.

Quando usadas em relatórios, as métricas podem ser analisadas por um período específico e [filtradas ou segmentadas](../../best-practices/segment-filter.md) por categorias diferentes. Considere analisar a receita média do cliente agrupada por gênero. Nesse caso, `average customer revenue per order` é a métrica e gênero é o agrupamento.

## Definição da métrica {#define}

1. Para criar uma métrica, clique em **[!UICONTROL Data** > **Metrics]**.

1. Clique em **[!UICONTROL Create New Metric]**.

1. Na lista suspensa, clique na tabela que inclui a coluna nativa ou calculada que deseja usar para sua métrica.

1. Nomeie sua métrica.

   A Adobe recomenda um nome que, resumidamente, informa qual é a métrica. Por exemplo: `Average Order Revenue`.

1. A próxima etapa é definir o que sua métrica faz. Usando os menus suspensos, defina a operação da métrica, a coluna `operation` e uma dimensão `date`:

   * Escolha uma operação:
      * `Count` - Essa operação conta o número de linhas em uma tabela de dados
      * `Max` - Max retorna o valor máximo de uma coluna de dados específica
      * `Min` - Mín retorna o valor mínimo de uma coluna de dados específica
      * `Sum` - Esta operação soma os valores de uma coluna de dados específica
      * `Average` - Esta operação calcula a média dos valores da coluna de dados
      * `Count Distinct Value` - Conta o número exclusivo de valores em uma coluna de dados específica
      * `Median` - Essa operação calcula a mediana dos valores da coluna de dados
      * `First and Third Quartiles` - Essas operações calculam os percentis 25 e 75 dos valores da coluna de dados, respectivamente
      * `Tenth and Ninetieth Percentiles` - Essas operações calculam os percentis 10 e 90 dos valores da coluna de dados, respectivamente

   * Escolha uma coluna na qual executar a operação. Por exemplo, se você quiser encontrar sua receita total, execute uma operação de soma na coluna `order total`.

     Se você estiver editando uma métrica existente, também poderá [alterar a tabela operacional da métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) nesta seção.

   * Escolha uma dimensão de data que possa ser usada para analisar a tendência da métrica. Por exemplo, `order date`.

## Adição de filtros {#filters}

A seção `Filter` permite criar um filtro ou aplicar um [conjunto de filtros salvos](../../data-user/reports/ess-manage-data-filters.md) à sua métrica.

Para a métrica `average order revenue`, você não deseja incluir pedidos de teste que possam ter sido feitos durante a configuração de sua loja, isso nos daria um resultado impreciso. É possível aplicar um conjunto de filtros para remover esses pedidos do conjunto de dados. Depois que o filtro for criado, ele será aplicado a todos os gráficos criados usando essa métrica.

A seção `Filter Logic` é onde você pode definir melhor como uma métrica deve se comportar.

* &quot;\[`A`\] ou \[`B`\]&quot; permite quaisquer dados que satisfaçam aos filtros \[`A`\] OU \[`B`\]
* &quot;\[`A`\] e \[`B`\]&quot; permite somente dados que satisfaçam ambos os filtros \[`A`\] e \[`B`\]
* &quot;(\[`A`\] e \[`B`\]) OU \[`C`\]&quot; permite somente dados que satisfazem os filtros \[`A`\] e \[`B`\] ou satisfazem o filtro \[`C`\] sozinho

## Adição de dimensões {#dimensions}

A seção [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) mostra todas as dimensões de dados disponíveis para filtragem ou agrupamento. Por padrão, todas as colunas de dados disponíveis são listadas como dimensões. Continuando com o exemplo, se você quiser segmentar sua receita por fonte de referência, faça isso aqui.

Além de listar todas as colunas de dados disponíveis como dimensões, [!DNL Commerce Intelligence] adivinha quais colunas são agrupáveis. *Para segmentar ou agrupar dados em relatórios*, as colunas devem ser marcadas como agrupáveis.

## Terminando {#finish}

Além de definir o comportamento da métrica, você também pode definir níveis de permissão na seção `User Rights`. Embora `Admin` usuários tenham acesso a todas as métricas, é necessário indicar os usuários que podem usar essa métrica marcando a caixa ao lado do grupo apropriado.

Se você estiver editando uma métrica existente, poderá ver uma lista de gráficos (e quem é o proprietário deles) que usam essa métrica na seção `Dependent Charts`.

As alterações são salvas automaticamente e sua métrica está pronta para ser usada.
