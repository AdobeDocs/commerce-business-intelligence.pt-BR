---
title: Visual Report Builder
description: Saiba como usar o Visual Report Builder.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# [!DNL Visual Report Builder]

O [!DNL Visual Report Builder] facilita a criação de relatórios rápidos com base em métricas predefinidas. Cada métrica inclui uma consulta que define o conjunto de dados do relatório.

O exemplo a seguir mostra como criar um relatório simples, agrupar os dados por uma dimensão adicional, definir o intervalo de data e hora, alterar o tipo de gráfico e salvar o relatório em um painel.

## Para criar um relatório simples:

1. No menu [!DNL Commerce Intelligence], clique em **[!UICONTROL Report Builder]**.

1. Em [!UICONTROL Visual Report Builder], clique em **[!UICONTROL Create Report]** e faça o seguinte:

   * Clique em **[!UICONTROL Add Metric]**.

     As métricas disponíveis podem ser listadas em ordem alfabética ou por tabela.

     ![Visual Report Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * Escolha a [métrica](../../data-user/reports/ess-manage-data-metrics.md) que descreve o conjunto de dados que você deseja usar para o relatório.

     A métrica `New Customers` usada neste exemplo conta todos os clientes e classifica a lista pela data em que o cliente se inscreveu em uma conta. O relatório inicial inclui um gráfico de linhas simples, seguido pela tabela de dados.

     O resumo à esquerda mostra o nome da métrica atual, seguido do resultado de quaisquer cálculos nos dados da coluna especificados na métrica. Neste exemplo, o resumo exibe a contagem total de clientes.

     ![Visual Report Builder](../../assets/magento-bi-report-builder-untitled.png)

1. No gráfico, passe o mouse sobre cada ponto de dados na linha. Cada ponto de dados mostra o número total de novos clientes que se inscreveram durante esse mês.

1. Siga estas instruções para agrupar os dados, alterar o intervalo de datas e o tipo de gráfico.

   **`Group By`**

   O controle `Group By` oferece a capacidade de adicionar várias dimensões por grupo ou segmento. Dimensões são colunas na tabela que podem ser usadas para agrupar os dados.

   * Escolha uma das dimensões disponíveis na lista de opções `Group By`.

     Neste exemplo, o sistema encontrou cinco códigos de cupom que foram usados pelos clientes ao fazer o primeiro pedido.

     ![Agrupar por](../../assets/magento-bi-report-builder-group-by-dimensions.png)

     O detalhe `Group By` lista cada cupom usado pelos clientes. Os cupons usados para fazer o pedido inicial são marcados com uma caixa de seleção. O gráfico agora tem várias linhas coloridas que representam cada cupom usado para um primeiro pedido. A legenda é codificada por cores para corresponder a cada linha de dados.

   * Clique em **[!UICONTROL Apply]** para fechar o detalhe Agrupar por.

     ![Várias dimensões](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * Passe o mouse sobre alguns pontos de dados em cada linha para ver o número de clientes durante o mês que usaram esse cupom enquanto faziam seu primeiro pedido.

   * A tabela de dados agora tem uma dimensão de adição, com uma coluna para cada mês e uma linha para cada código de cupom.

     ![Agrupar por Dados da Tabela](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * Clique no controle Transpor (![Ícone Transpor](../../assets/magento-bi-btn-transpose.png)), no canto superior direito da tabela, para alterar a orientação dos dados.

     O eixo dos dados é invertido e a tabela agora tem uma coluna para cada código de cupom e uma linha para cada mês. Talvez seja mais fácil ler essa orientação.

     ![Dados Transpostos](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)

   **`Date Range`**

   O controle `Date Range` mostra as configurações atuais de intervalo de datas e intervalo de tempo e está localizado logo acima do gráfico à direita.

   * Clique no controle `Date Range`, que neste exemplo está definido como `All-Time by Month`.

     ![Intervalo de datas](../../assets/magento-bi-report-builder-date-range.png)

   * Faça as seguintes alterações:

      * Para ampliar para uma exibição mais próxima, altere o intervalo de datas para `Last Full Quarter`.
      * Em `Select Time Interval`, escolha `Week`.
      * Quando terminar, clique em **[!UICONTROL Save]**.

     O relatório agora inclui apenas os dados do último trimestre, por semana.

     ![Relatório do último trimestre por semana](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)

   **Tipo de gráfico**

   * Clique nos controles no canto superior direito para encontrar o melhor gráfico para os dados.

     Alguns tipos de gráfico não são compatíveis com dados multidimensionais.

     | | |
     |-----|-----|
     | ![Ícone de gráfico de linhas](../../assets/magento-bi-btn-chart-line.png) | Gráfico de linhas |
     | ![Ícone de barra horizontal](../../assets/magento-bi-btn-chart-horz-bar.png) | Barra horizontal |
     | ![Ícone de barra empilhada horizontal](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | Barra empilhada horizontal |
     | ![Ícone de barra vertical](../../assets/magento-bi-btn-chart-vert-bar.png) | Barra vertical |
     | ![Ícone de barra empilhada vertical](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | Barra empilhada vertical |
     | ![Ícone do gráfico de pizza](../../assets/magento-bi-btn-chart-pie.png) | Pizza |
     | ![Ícone de gráfico de área](../../assets/magento-bi-btn-chart-area.png) | Área |
     | ![ícone do gráfico Funnel](../../assets/magento-bi-btn-chart-funnel.png) | Funil |

     {style="table-layout:auto"}

1. Para dar ao relatório um `title`, substitua o texto `Untitled Report` na parte superior da página por um título descritivo.

1. No canto superior direito, clique em **[!UICONTROL Save]** e faça o seguinte:

   * Para `Type`, aceite a configuração padrão, `Chart`.

   * Escolha o `Dashboard` onde o relatório deve estar disponível.

   * Clique em **[!UICONTROL Save to Dashboard]**.

     ![Salvar no Painel](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. Para exibir o gráfico em um painel, siga um destes procedimentos:

   * Clique em **[!UICONTROL Go to Dashboard]** na mensagem na parte superior da página.

   * No menu, escolha `Dashboards` e clique no nome do painel atual para exibir a lista. Em seguida, clique no nome do painel onde o relatório foi salvo.

     ![Relatório no painel](../../assets/magento-bi-report-builder-my-dashboard.png)
