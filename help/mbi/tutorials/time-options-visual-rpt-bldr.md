---
title: Usar opções de tempo no Visual Report Builder
description: Saiba como analisar os dados em seu relatório de um período específico.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# Use `Time` Opções em `Visual Report Builder`

Um dos recursos do `Visual Report Builder` é global `Time Range` e `Interval` configurações. Essas configurações permitem analisar os dados em seu relatório por um período específico.

No entanto, para algumas análises, pode ser necessário considerar intervalos de tempo ou intervalos de tempo diferentes no mesmo relatório. É aí que está `Time` As opções entram. Para lhe dar uma ideia melhor de como usar `Time` Opções em seus relatórios, este tutorial abordará os seguintes casos de uso:

* [Análise de métricas sem carimbos de data e hora](#notimestamp)
* [Fornecer uma métrica a um intervalo de tempo independente](#independenttimeinterval)
* [Comparação da mesma métrica em intervalos de tempo diferentes](#difftimerange)

Se quiser seguir com alguns dos relatórios de amostra discutidos neste tópico, abra o [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) antes de continuar.

## Análise de métricas sem carimbos de data e hora {#notimestamp}

Algumas métricas simplesmente não podem analisar a tendência ao longo do tempo porque os dados não são coletados ou armazenados com um carimbo de data e hora associado. Por exemplo, uma tabela de inventário geralmente contém apenas uma linha para cada SKU. Nesse caso, você deve [criar a métrica](../data-user/reports/ess-manage-data-metrics.md) sem especificar um carimbo de data e hora.

Ao usar essa métrica em seu relatório, você percebe que adicionar essa métrica a um relatório define automaticamente um relatório independente `Time Interval` de `None` e `Time Range` de `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Fornecer uma métrica a um intervalo de tempo independente {#independenttimeinterval}

`Time` As opções permitem criar gráficos de 100% baseados em tempo para identificar qual dia, semana, mês ou ano contribuiu mais com o valor durante um intervalo de tempo específico. Nesta seção, criamos um gráfico que mostra a porcentagem da receita gerada em cada mês do ano.

Esse tipo de relatório pode ser útil se você quiser comparar a receita gerada ano a ano. Por exemplo, se um gráfico de 2015 revelasse que janeiro contribuiu com 18% da receita do ano e um de 2016 apresentava apenas 8%, você poderia começar a pesquisar o que poderia ter acontecido.

1. Adicione seu `Revenue` para o relatório.
1. Clique em **[!UICONTROL Duplicate]** para fazer uma cópia da métrica.
1. Clique no link global **[!UICONTROL Time Range]** , em seguida **[!UICONTROL Moving Time Range]**. Defina como `Last Year`.
1. Clique no link global **[!UICONTROL Time Interval]** e defina-a como `Monthly`.
1. O Report Builder adiciona automaticamente um segundo eixo Y para uma segunda métrica. Desmarque a opção `Multiple Y-Axes` caixa.
1. Em seguida, aplicamos um `Time Interval` para a primeira métrica. Clique em **[!UICONTROL Time Options]** (ícone de relógio) à direita do `first Revenue metric`.
1. Clique em **[!UICONTROL Time Options]** na janela expandida que é exibida acima do relatório.
1. Na lista suspensa, defina o seguinte:

   * `Time Interval`: defina como `None`.

   * `Time Range`: defina como `Last Year` clicando primeiro em **[!UICONTROL Custom]**, em seguida **[!UICONTROL Moving Range]** e finalmente selecionando o `Last Year` opção.

   * Clique em **[!UICONTROL Apply]** para salvar as configurações de intervalo e intervalo. Isso cria uma métrica que calcula a receita total do ano anterior. Em seguida, usamos essa métrica como denominador em uma fórmula.

   * Para visualizar a porcentagem da receita para cada mês, precisamos adicionar uma fórmula ao relatório. Clique em **[!UICONTROL Add Formula]**.

   * Enter `B/A` no campo da fórmula e selecione `% Percent` na lista suspensa ao lado do campo de texto. Esta fórmula divide a quantia de receita de um mês específico do ano passado pela quantia total de receita do ano passado.

   * Clique em **[!UICONTROL Apply Changes]**.

   * Oculte ambas as métricas de entrada e renomeie a fórmula.

Agora podemos ver o impacto que cada mês teve no ano passado:

![](../assets/Independent_Time_Int.png)

## Comparação da mesma métrica em intervalos de tempo diferentes {#difftimerange}

Esse exemplo usa uma dimensão personalizada chamada `Day number of the month`. Se quiser criar esse relatório e ainda não tiver essa dimensão na Data Warehouse, [entrar em contato com o suporte](../guide-overview.md) para obter assistência.

Os dois exemplos mais comuns nesta categoria são (1) comparação das métricas de crescimento (receita ano a ano ou mês a mês) e (2) melhor compreensão das tendências recentes de vendas de itens ou inventário.

Para demonstrar esse caso de uso, observamos a receita diária do mês anterior em comparação ao mesmo mês do ano anterior. Digamos que queremos ver as receitas de cada dia de janeiro de 2016 e depois compará-las com janeiro de 2015, janeiro de 2014, e assim por diante - este relatório nos mostraria isso.

1. Adicione seu `Revenue` para o relatório.
1. Clique em **[!UICONTROL Duplicate]** para fazer uma cópia da métrica.
1. Renomeie a primeira métrica para `Items sold last 7 days` e a segunda métrica para `Items sold last 28 days`.
1. Clique em **[!UICONTROL Time Range]**, em seguida **[!UICONTROL Moving Time Range]**. Defina como `Last Month`.
1. Clique em **[!UICONTROL Time Interval]** e defina-o como `None`.
1. Clique em **[!UICONTROL Time Options]** (ícone de relógio) ao lado do segundo `Revenue` métrica.
1. Clique em **[!UICONTROL Time Options]** na janela expandida que é exibida acima do relatório.
1. Na lista suspensa, defina o seguinte:

   * `Time Interval`: defina como `None`.

   * `Time Range`: defina como `From 14 Months Ago To 13 Months Ago` clicando primeiro em **[!UICONTROL Custom]** then **[!UICONTROL Moving Range]**. Use os campos e as listas suspensas na parte superior do menu para definir o intervalo. Essa configuração permite visualizar a receita do mês anterior, mas do ano anterior.
   Não se preocupe se a métrica desaparecer do relatório - definir uma opção de hora independente automaticamente ocultará a métrica do relatório. Para exibi-la novamente, clique em **[!UICONTROL Show]** ao lado da métrica.

   ![](../assets/Different_Time_Ranges.gif)

   * Clique em **[!UICONTROL Apply]** para salvar as configurações de intervalo e intervalo.

   * Em seguida, adicionamos nosso personalizado `Day number of the month` ao clicar em **[!UICONTROL Group By]** e selecionando a dimensão. Isso retornará o número do dia do mês de um pedido - por exemplo, um pedido feito em 2 de março retornará `2`.

   * No `Group By` lista suspensa, selecione `Show All` e clique em **[!UICONTROL Apply]**. Isso criará efetivamente os valores do eixo X para o relatório:

   ![](../assets/TO4.png)

   * Renomeie as métricas. No nosso exemplo, a primeira métrica é `Revenue - 2015` e o segundo é `Revenue - 2014`.



Outro uso comum do `Time Options` determina as semanas de fornecimento. Especialmente durante a temporada de festas ou um período promocional especial, você pode considerar os itens vendidos na última semana, mês e período promocional anterior para tomar decisões de compra informadas.

Lembre-se de definir os intervalos de tempo para o que é necessário ao criar esse relatório por conta própria.

1. Adicione seu `Items Sold` para o relatório.
1. Clique em **[!UICONTROL Duplicate]** para fazer uma cópia da métrica.
1. Renomeie as métricas. Você pode usar os mesmos nomes que estamos ou usar algo semelhante:
   1. Renomeie a primeira métrica para `Items sold last 7 days`.
   1. Renomeie a segunda métrica para `Items sold last 28 days`.
1. No `Items sold last 7 days` , clique no link global **[!UICONTROL Time Range]** em seguida **[!UICONTROL Moving Time Range]**. Para este exemplo, definimos como `Last 7 Days`.
1. Clique em **[!UICONTROL Time Interval]** e defina-o como `None`.
1. Em seguida, definimos o `Time Options` para `Items sold last 28 days` métrica. Clique em **[!UICONTROL Time Options]** (ícone de relógio) à direita do `second Items sold` métrica.
1. Clique em **[!UICONTROL Time Options]** na janela expandida que é exibida acima do relatório.
1. Na lista suspensa, defina o seguinte:

   * `Time Interval`: defina como `None`.
   * `Time Range`: defina como `From 29 days to 1 day ago` clicando primeiro em **[!UICONTROL Custom]**, em seguida **[!UICONTROL Moving Range]**. Use os campos e as listas suspensas na parte superior do menu para definir o intervalo.
   * Clique em **[!UICONTROL Apply]** para salvar as configurações de intervalo e intervalo.
   * Duplique o `Items sold last 28 days` e abra o `Time Options`. Defina as opções para o seguinte:

      * `Time Interval`: deixe isso como `None`.
      * `Time Range`: altere isso para o intervalo de datas que se alinha à promoção em que você está interessado clicando em **[!UICONTROL Specific Date Range]** e, em seguida, inserir as datas apropriadas.
      * Renomear a métrica `Items sold during last promotion` ou algo parecido.
      * Adicione seu `Units on hand` métrica.
      * Em seguida, precisamos adicionar os cálculos que nos mostram as semanas, considerando as tendências de vendas, para os períodos (`last 7 days`, `last 28 days`e `last promo` (ponto final) estamos incluídos no relatório. Você precisa fazer isso uma vez para cada período de tempo.

Para criar fórmulas, clique em **[!UICONTROL Add Formula]**. Insira as fórmulas abaixo e clique em **[!UICONTROL Apply Changes]** quando terminar. Repita o procedimento para cada um dos três períodos de tempo:

* Para o `last 7 days time period`, insira `D / A` no `Formula` campo.
* Para o `last 28 days time period`, insira `D / (B/4)` no `Formula` campo.

   >[!NOTE]
   >
   >É importante normalizar os intervalos de tempo selecionados aqui. Neste exemplo, 28 dias devem ser divididos em quatro semanas. Talvez seja necessário aplicar uma lógica diferente à fórmula.

* Para o `last promo period`, insira `D / C` no `Formula` campo.

   ![](../assets/Different_Time_Ranges_2.png)

* Por fim, personalize o relatório ocultando as métricas e adicionando uma `SKU` ou uma dimensão semelhante ao relatório como uma `Group By`.

Este exemplo demonstra que os níveis atuais de inventário estavam bem localizados para uma venda de 14 dias em todo o produto. No entanto, a adição de um período promocional comparável sugere que a empresa precisa fazer algumas alterações - seja encomendando mais inventário e promovendo apenas os itens com unidades suficientes em estoque.

Como seus clientes se comportam de forma diferente ao longo do tempo, é possível observar as variações nos dados ao realizar análises. Definir opções de tempo personalizadas permite que você crie análises complexas rapidamente, permitindo decisões orientadas por dados que afetam tendências históricas.

Veja nossa [vídeo de treinamento](https://support.magento.com/hc/en-us/articles/360016730071-Training-Video-Time-Options-in-the-Visual-Report-Builder) para saber mais.
