---
title: Usar o Report Builder visual
description: Saiba como analisar os dados em seu relatório por um período específico.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Use o `Visual Report Builder`

A variável [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) O permite explorar visualmente seus dados para obter insights e ajudar a impulsionar as decisões de negócios. Este tutorial o guiará pelo processo de criação de um relatório básico.

>[!NOTE]
>
>Para adicionar um relatório a um painel, é necessário `Standard` [permissões de usuário](../administrator/user-management/user-management.md) e `Edit` acesso ao painel.

## Etapa 1: Criação de um relatório

Para começar a criar um relatório, clique em **[!UICONTROL Report Builder]** na barra lateral ou **[!UICONTROL Add Report]** na parte superior de qualquer painel. Quando a variável `Report Builder` for exibida, clique no link **[!UICONTROL Visual Report Builder]** opção.

Para editar um relatório criado na `Visual Report Builder`, clique no ícone de engrenagem (Opções) no canto superior direito de qualquer gráfico e clique em **[!UICONTROL Edit]**.

## Etapa 2: Adição de métricas

A primeira etapa na criação de uma análise é selecionar [a métrica](../data-user/reports/ess-manage-data-metrics.md) para analisar. Embora as métricas sejam listadas alfabeticamente por padrão, você também pode agrupá-las pela tabela que ativa a métrica.

Você pode adicionar outras métricas depois que a métrica inicial for selecionada e sobrepor todas as métricas em um único relatório ou executar cálculos de várias métricas adicionando fórmulas.

## Etapa 3: Adição `Formulas`

`Formulas` são adicionados aos relatórios clicando em **[!UICONTROL Add Formula]**, localizado logo acima da lista de métricas no relatório. No [editor de fórmulas](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), qualquer uma das métricas incluídas no relatório pode ser usada como entradas. Operadores matemáticos básicos são usados para manipular as diferentes métricas.

Digamos que você deseje criar um relatório que mostre a receita média por pedido. Nesse caso, você dividiria a variável `Revenue` métrica por `Number of orders` métrica.

![](../assets/ave-rev-per-order.png)

## Etapa 4: definição de `Time Period` e `Interval of Analysis` {#time}

Para zerar em um período de tempo específico, é possível definir o período da análise. Você também pode escolher intervalos de tempo para segmentar os dados (por exemplo, por ano, por trimestre ou por mês). Use os menus no canto superior direito do gráfico para definir o período e o intervalo.

![](../assets/Time_Options_Report_Builder.png)

Ao definir um intervalo de datas específico para o período, verifique se a data de início está no início do intervalo e a data de término está no final do intervalo.

Por exemplo, definir um período de tempo de `January 1st to March 1st` e escolhendo um `monthly` o intervalo aparece `March` como um ponto de dados, mas ignorar todos os dias no `March` exceto `March 1`. Nesse caso, você deve tornar seus `Time Period` de `January 1 to March 31`.

## Etapa 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Para segmentar suas métricas por uma dimensão de dados](../best-practices/segment-filter.md), clique no link **[!UICONTROL Group by]** na parte superior esquerda do gráfico. Isso revela uma lista suspensa que inclui todas as dimensões disponíveis da primeira métrica incluída na lista.

Você pode escolher `None` para impedir que uma métrica seja segmentada. Por exemplo, você pode querer uma métrica que retorne a receita total sem ser segmentada, enquanto tem outra métrica de receita segmentada por região.

Retorne ao exemplo de receita média por pedido e defina o Group by para o código promocional. Isso mostra a receita média por pedido para pedidos com e sem um código promocional.

![](../assets/Group_By_Report_Builder.png)

Se as métricas incluídas na análise forem criadas em tabelas de dados diferentes, uma janela pop-up permitirá selecionar a dimensão de dados correspondente em cada tabela. O objetivo aqui é encontrar dimensões que compartilham tipos de valores para segmentação:

![](../assets/Dimension_Editor.png)

## Etapa 6: configuração `Metric Filters`, `Perspective`, e `Time Interval` {#metric-specific}

Para cada métrica adicionada à análise, é possível adicionar filtros, selecionar a perspectiva de dados relevante e definir `time interval` opções. Para acessar esses recursos, clique no funil (`Filter`), olho (`Perspective`) e relógio (`Time`) localizados ao lado das métricas incluídas no relatório.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limitar o conjunto de dados incluído na análise. Os filtros são úteis, por exemplo, ao avaliar canais de aquisição individuais e remover outliers.

Além dos menus suspensos e da caixa de texto, também é possível usar operadores de filtro especiais, como `LIKE` ou `IN` para criar filtros.

O uso de curingas (`%` ou `_`) com `LIKE` é compatível. A variável `%` o curinga corresponde a vários caracteres, enquanto `_` corresponde apenas a qualquer caractere único. Por exemplo:

- `affiliate's name Like B%` permite somente dados de clientes cujo nome começa com `B`.

- `affiliate's name Like _ake` O permite somente dados de clientes cujos nomes sejam semelhantes a `Jake`, `Rake`ou `Bake` mas não `Drake` ou `Blake`.

A adição de vários filtros permite um controle rígido dos dados do gráfico. Por padrão, todas as condições de filtro devem ser verdadeiras para que um pedaço de dados seja incluído, mas você pode criar relações OR editando a caixa de texto Regras de filtro.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Permitem alternar facilmente entre diferentes visualizações dos dados. Veja o que está disponível:

- `Standard perspective`: a perspectiva padrão mostra o resultado para a data correspondente no eixo x (por exemplo, receita em janeiro). Essa é a perspectiva que você usa no exemplo de Receita média por pedidos.

![](../assets/Standard.png)

- `Amount` OU `Percent Change` versus `Previous Period` perspectiva: essa perspectiva mostra a quantidade ou a alteração percentual de um intervalo para o próximo e é útil para medir a taxa de alteração em métricas de rápida alteração. Também há uma perspectiva para comparar o intervalo com o mesmo período do ano passado para mostrar o crescimento ano a ano.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: A variável `cumulative perspective` mostra o valor da soma contínua ou cumulativa da métrica durante o período. Isso é usado com frequência para analisar o total de clientes e planejar a capacidade futura.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: essa perspectiva mostra os dados como um percentual do primeiro intervalo incluído na análise. Isso é útil para medir a eficácia de ações específicas em relação ao desempenho do primeiro período.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: a perspectiva da janela de médias contínuas mostra o valor da média contínua de uma métrica no intervalo de tempo especificado. O intervalo deve ser igual ao intervalo definido no nível de relatório. Por exemplo, se o relatório estiver mostrando o último trimestre completo de Receita por semana, você pode definir o intervalo de tempo da janela média acumulada para quatro semanas. Isso faz com que os três primeiros valores sejam nulos e o quarto valor represente a média das quatro primeiras semanas de Receita. Para maior clareza, desative o `Multiple Y-Axes` se você estiver visualizando a mesma métrica com uma média variável, como no exemplo abaixo.

![](../assets/rolling_avg_window.png)

### Opções de tempo específicas da métrica

Existem duas opções para as métricas usadas nos relatórios: elas podem analisar a tendência ao longo do tempo de acordo com as opções de tempo global, que as exibirão como um número escalar.

Alteração do intervalo de tempo de uma métrica para `None` retorna um `scalar` número, que é útil ao criar fórmulas que envolvem a divisão de uma métrica de tendência de tempo por uma `scalar` número. Além disso, também é possível alterar o intervalo de tempo da variável `scalar` para um intervalo de tempo independente daquele do relatório.

Por exemplo, você gostaria de ver a receita mensal de 2019 expressa como uma porcentagem da receita geral de 2019. Você pode adicionar dois `Revenue` para um relatório com um intervalo de tempo global de 1 de janeiro de 2019 a 31 de dezembro de 2019, segmentado por intervalo mensal.

>[!NOTE]
>
>Se você adicionar `group by` dimensões, escolha uma nova visualização ou ajuste o intervalo de tempo e salve apenas o Número (`scalar`). Esses ajustes não são mantidos na próxima vez que você abrir esse relatório em um painel; somente o intervalo de tempo será mantido.

Para saber mais sobre como usar as opções de tempo em seus relatórios, consulte esta [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Etapa 7: Salvar o relatório

Ao criar um gráfico, você pode salvá-lo clicando em **[!UICONTROL Save]** no canto superior direito da `Visual Report Builder`.

Você pode optar por salvar um gráfico, tabela ou número (`scalar`) utilizando o `Type` e o painel no qual o relatório deve ser salvo usando o `Location` lista suspensa.

É possível salvar o relatório clicando em **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Saídas do relatório

Para ajudá-lo a decidir qual saída de relatório escolher, consulte o seguinte:

### Gráfico

![](../assets/RB_Chart.png)

### Tabela

![](../assets/RB_Table.png)

### Número (`scalar`)

![](../assets/RB_Scalar.png)

Parabéns! Você terminou.
