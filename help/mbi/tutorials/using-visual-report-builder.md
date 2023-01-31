---
title: Use o Visual Report Builder
description: Saiba como analisar os dados em seu relatório de um período específico.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Use o `Visual Report Builder`

O [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) O permite explorar visualmente seus dados para obter insights e ajudar a impulsionar decisões de negócios. Este tutorial o orienta pelo processo de criação de um relatório básico.

>[!NOTE]
>
>Para adicionar um relatório a um painel, é necessário `Standard` [permissões do usuário](../administrator/user-management/user-management.md) e `Edit` acesso ao painel.

## Etapa 1: Criar um relatório

Para começar a criar um novo relatório, clique em **[!UICONTROL Report Builder]** na barra lateral ou **[!UICONTROL Add Report]** na parte superior de qualquer painel. Quando a variável `Report Builder` página de seleção é exibida, clique no botão **[!UICONTROL Visual Report Builder]** opção.

Para editar um relatório criado na `Visual Report Builder`, clique no ícone de engrenagem (Opções) no canto superior direito de qualquer gráfico e clique em **[!UICONTROL Edit]**.

## Etapa 2: Adicionar métricas

A primeira etapa na criação de uma análise é selecionar [a métrica](../data-user/reports/ess-manage-data-metrics.md) para analisar. Embora as métricas sejam listadas em ordem alfabética por padrão, também é possível agrupá-las pela tabela que alimenta a métrica.

Você pode adicionar outras métricas depois que a métrica inicial for selecionada e sobrepor todas as métricas em um único relatório ou realizar cálculos de várias métricas adicionando fórmulas.

## Etapa 3: Adição de `Formulas`

`Formulas` são adicionados aos relatórios ao clicar em **[!UICONTROL Add Formula]**, localizado logo acima da lista de métricas no relatório. No [editor de fórmula](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), qualquer métrica incluída no relatório pode ser usada como entradas. Os operadores matemáticos básicos são usados para manipular as diferentes métricas.

Digamos que quisemos criar um relatório que nos mostre a receita média por pedido. Nesse caso, dividiríamos a variável `Revenue` por `Number of orders` métrica.

![](../assets/ave-rev-per-order.png)

## Etapa 4: Definir a `Time Period` e `Interval of Analysis` {#time}

Para zerar em um período específico, é possível definir o período de tempo da análise. Você também pode escolher intervalos de tempo para segmentar os dados (por exemplo, por ano, por trimestre ou por mês). Use os menus no canto superior direito do gráfico para definir o período e o intervalo de tempo.

![](../assets/Time_Options_Report_Builder.png)

Ao definir um intervalo de datas específico para o período de tempo, verifique se a data inicial está no início do intervalo e se a data final está no final do intervalo.

Por exemplo, definir um período de tempo de `January 1st to March 1st` e escolher uma `monthly` o intervalo será mostrado `March` como um datapoint, mas ignorar todos os dias em `March` Except `March 1`. Nesse caso, você deve `Time Period` from `January 1 to March 31`.

## Etapa 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Para segmentar suas métricas por uma dimensão de dados](../best-practices/segment-filter.md), clique no botão **[!UICONTROL Group by]** na parte superior esquerda do gráfico. Isso revelará uma lista suspensa que inclui todas as dimensões disponíveis da primeira métrica incluída na lista.

Você pode escolher `None` para evitar que uma métrica seja segmentada. Por exemplo, talvez você queira uma métrica que retorne a receita total sem ser segmentada, ao mesmo tempo em que tem outra métrica de receita segmentada por região.

Retorne ao exemplo de receita média por pedido e defina o Grupo por para o código promocional. Isso nos mostrará a receita média por pedido de pedidos com e sem um código promocional.

![](../assets/Group_By_Report_Builder.png)

Se as métricas incluídas na análise forem criadas em diferentes tabelas de dados, uma pop-up permitirá selecionar a dimensão de dados correspondente em cada tabela. O objetivo aqui é encontrar dimensões que compartilham o mesmo tipo de valores para segmentação:

![](../assets/Dimension_Editor.png)

## Etapa 6: Configuração `Metric Filters`, `Perspective`e `Time Interval` {#metric-specific}

Para cada métrica adicionada à análise, você pode adicionar filtros, selecionar a perspectiva de dados relevante e definir `time interval` opções. Para acessar esses recursos, clique no funil (`Filter`), olho (`Perspective`) e relógio (`Time`) ícones localizados ao lado das métricas incluídas no relatório.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limite o conjunto de dados incluído na análise. Os filtros são extremamente úteis, por exemplo, ao avaliar canais de aquisição individuais e remover outliers.

Além dos menus suspensos e da caixa de texto, também é possível usar operadores de filtro especiais, como `LIKE` ou `IN` para criar filtros.

O uso de curingas (`%` ou `_`) em conjunto com `LIKE` instruções são suportadas. O `%` curinga corresponderá a vários caracteres, enquanto `_` somente corresponderá a qualquer caractere único. Por exemplo:

- `affiliate's name Like B%` permitirá somente dados de clientes cujo nome começa com `B`.

- `affiliate's name Like _ake` permitirá somente dados de clientes cujos nomes sejam semelhantes `Jake`, `Rake`ou `Bake` mas não `Drake` ou `Blake`.

Adicionar vários filtros permite um controle rigoroso dos dados do gráfico. Por padrão, todas as condições de filtro devem ser verdadeiras para que um dado seja incluído, mas você pode criar relações OU editando a caixa de texto Regras de filtro .

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` permite alternar facilmente entre diferentes visualizações de seus dados. Vamos analisar o que está disponível:

- `Standard perspective`: A perspectiva padrão mostra o resultado da data correspondente no eixo x (por exemplo, receita em janeiro). Esta é a perspectiva que estamos usando em nosso exemplo de receita média por pedidos.

![](../assets/Standard.png)

- `Amount` OU `Percent Change` versus `Previous Period` perspectiva: Esta perspectiva mostra a mudança de quantidade ou porcentagem de um intervalo para o seguinte e é útil para medir a taxa de mudança em métricas que mudam rapidamente. Há também uma perspectiva para comparar o intervalo ao mesmo período de tempo do ano passado para mostrar o crescimento de ano para ano.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: O `cumulative perspective` mostra a soma contínua ou cumulativa da métrica durante o período de tempo. Isso é usado frequentemente para analisar o total de clientes e planejar a capacidade futura.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Essa perspectiva mostra os dados como uma porcentagem do primeiro intervalo incluído na análise. Isso é útil para medir a eficácia de ações específicas em relação ao desempenho do primeiro período.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: A perspectiva da janela de médias contínuas mostra o valor médio acumulado de uma métrica no intervalo de tempo especificado. O intervalo deve ser igual ao intervalo definido no nível do relatório. Por exemplo, se o relatório estiver mostrando o último trimestre completo de Receita por semana, você poderá definir o intervalo de tempo médio acumulado da janela para 4 semanas, e os três primeiros valores serão nulos e o quarto valor representará a média das primeiras 4 semanas de Receita. Para maior clareza, desligue o `Multiple Y-Axes` caixa de seleção se estiver visualizando a mesma métrica com uma média móvel, como no exemplo abaixo.

![](../assets/rolling_avg_window.png)

### Opções de tempo específicas de métrica

Existem duas opções para as métricas usadas nos relatórios: elas podem analisar a tendência ao longo do tempo de acordo com as opções de tempo global, ou não, o que as exibirá como um número escalar.

Alteração de um intervalo de tempo de métrica para `None` retorna um `scalar` número, que é útil ao criar fórmulas que envolvem a divisão de uma métrica de tendência de tempo por um `scalar` número. Além disso, também é possível alterar o intervalo de tempo da variável `scalar` para um intervalo de tempo independente do relatório.

Por exemplo, queríamos ver as receitas mensais de 2019 expressas em percentagem das receitas totais de 2019. Podemos adicionar dois `Revenue` métricas para um relatório com um intervalo de tempo global de 1º de janeiro de 2019 a 31 de dezembro de 2019, segmentado por intervalo mensal.

>[!NOTE]
>
>Se você adicionar `group by` , escolha uma nova visualização ou ajuste o intervalo de tempo e salve apenas o Número (`scalar`), esses ajustes não serão mantidos na próxima vez que você abrir o relatório de um painel, somente o intervalo de tempo será mantido.

Para saber mais sobre o uso de opções de tempo em seus relatórios, consulte esta seção [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Etapa 7: Salvar o relatório

Ao criar um novo gráfico, você pode salvá-lo clicando em **[!UICONTROL Save]** no canto superior direito do `Visual Report Builder`.

Você pode optar por salvar um gráfico, tabela ou número (`scalar`) usando o `Type` lista suspensa e o painel no qual o relatório deve ser salvo usando o `Location` lista suspensa.

Você pode salvar o relatório clicando em **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Resultados dos relatórios

Para ajudá-lo a decidir qual resultado do relatório escolher, consulte o seguinte:

### Gráfico

![](../assets/RB_Chart.png)

### Tabela

![](../assets/RB_Table.png)

### Número (`scalar`)

![](../assets/RB_Scalar.png)

Parabéns! Você terminou.
