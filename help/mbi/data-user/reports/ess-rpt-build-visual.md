---
title: Report Builder visual
description: Saiba como usar o Visual Report Builder.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# `Visual Report Builder`

`Visual Report Builder` facilita a criação de relatórios rápidos com base em métricas predefinidas. Cada métrica inclui uma consulta que define o conjunto de dados do relatório.

O exemplo a seguir mostra como criar um relatório simples, agrupar os dados por uma dimensão adicional, definir a data e o intervalo de tempo, alterar o tipo de gráfico e salvar o relatório em um painel.

## Para criar um relatório simples:

1. No [!DNL MBI] , clique em **[!UICONTROL Report Builder]**.

1. Em `Visual Report Builder`, clique em **[!UICONTROL Create Report]** e faça o seguinte:

   * Clique em **[!UICONTROL Add Metric]**.

      As métricas disponíveis podem ser listadas em ordem alfabética ou por tabela.

      ![Report Builder visual](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * Escolha a [métrica](../../data-user/reports/ess-manage-data-metrics.md) que descreve o conjunto de dados que deseja usar para o relatório.

      O `New Customers` A métrica usada neste exemplo conta todos os clientes e classifica a lista pela data em que o cliente se inscreveu para uma conta. O relatório inicial inclui um gráfico de linhas simples, seguido pela tabela de dados.

      O resumo à esquerda mostra o nome da métrica atual, seguido pelo resultado de quaisquer cálculos nos dados da coluna especificados na métrica. Neste exemplo, o resumo exibe a contagem total de clientes.

      ![Report Builder visual](../../assets/magento-bi-report-builder-untitled.png)

1. No gráfico, passe o mouse sobre cada ponto de dados na linha. Cada ponto de dados mostra o número total de novos clientes que se inscreveram durante esse mês.

1. Siga estas instruções para agrupar os dados, alterar o intervalo de datas e o tipo de gráfico.

   **`Group By`**

   O `Group By` O controle oferece a capacidade de adicionar várias dimensões por grupo ou segmento. Dimension são colunas na tabela que podem ser usadas para agrupar os dados.

   * Escolha uma das dimensões disponíveis na lista de `Group By` opções.

      Neste exemplo, o sistema encontrou cinco códigos de cupom que foram usados pelos clientes ao fazer seu primeiro pedido.

      ![Agrupar por](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      O `Group By` detalha lista cada cupom usado pelos clientes. Os cupons usados para colocar o pedido inicial são marcados com uma caixa de seleção. O gráfico agora tem várias linhas coloridas que representam cada cupom que foi usado para um primeiro pedido. A legenda é codificada por cores para corresponder a cada linha de dados.

   * Clique em **[!UICONTROL Apply]** para fechar o detalhe Agrupar por.

      ![Vários Dimension](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * Passe o mouse sobre alguns pontos de dados em cada linha para ver o número de clientes durante o mês que usaram esse cupom ao fazer seu primeiro pedido.

   * A tabela de dados agora tem uma dimensão de adição, com uma coluna para cada mês e uma linha para cada código de cupom.

      ![Agrupar por dados da tabela](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * Clique em Transpor (![](../../assets/magento-bi-btn-transpose.png)) no canto superior direito da tabela para alterar a orientação dos dados.

      O eixo dos dados é virado e a tabela agora tem uma coluna para cada código de cupom e uma linha para cada mês. Você pode achar essa orientação mais fácil de ler.

      ![Dados transpostos](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   O `Date Range` controle mostra o intervalo de datas atual e as configurações de intervalo de tempo, e está localizado logo acima do gráfico à direita.

   * Clique no botão `Date Range` , que neste exemplo está definido como `All-Time by Month`.

      ![Intervalo de datas](../../assets/magento-bi-report-builder-date-range.png)

   * Faça as seguintes alterações:

      * Para ampliar para uma exibição mais próxima, altere o intervalo de datas para `Last Full Quarter`.
      * Em `Select Time Interval`, escolha `Week`.
      * Ao concluir, clique em **[!UICONTROL Save]**.

      O relatório agora inclui apenas os dados do último trimestre, por semana.

      ![Relatório do último trimestre por semana](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **Tipo de gráfico**

   * Clique nos controles no canto superior direito para encontrar o melhor gráfico para os dados.

      Alguns tipos de gráfico não são compatíveis com dados multidimensionais.

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | Gráfico de linhas |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | Barra horizontal |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | Barra empilhada horizontal |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | Barra vertical |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | Barra empilhada vertical |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | Pizza |
      | ![](../../assets/magento-bi-btn-chart-area.png) | Área |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | Funil |

      {style=&quot;table-layout:auto&quot;}




1. Para dar ao relatório uma `title`, substitua o `Untitled Report` texto na parte superior da página com um título descritivo.

1. No canto superior direito, clique em **[!UICONTROL Save]** e faça o seguinte:

   * Para `Type`, aceitar a configuração padrão, `Chart`.

   * Escolha a `Dashboard` se o relatório estiver disponível.

   * Clique em **[!UICONTROL Save to Dashboard]**.

      ![Salvar no painel](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. Para exibir o gráfico em um painel, siga um destes procedimentos:

   * Clique em **[!UICONTROL Go to Dashboard]** na mensagem na parte superior da página.

   * No menu , escolha `Dashboards` e clique no nome do painel atual para exibir a lista. Em seguida, clique no nome do painel onde o relatório foi salvo.

      ![Relatório no painel](../../assets/magento-bi-report-builder-my-dashboard.png)
