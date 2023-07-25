---
title: Fórmulas
description: Saiba como usar fórmulas.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Fórmulas

Uma fórmula combina várias métricas e lógica matemática para responder a uma pergunta. Por exemplo, quanto da receita por produto durante a temporada de festas foi gerado por novos clientes?

![Vendas de Feriados no Painel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Etapa 1: criar o relatório básico

1. No menu, escolha `Report Builder`.

1. Clique em **[!UICONTROL Add Metric]** e escolha a primeira métrica para o relatório.

   Neste exemplo, a variável `Revenue by products ordered` será utilizada.

1. Clique em **[!UICONTROL Add Metric]** novamente e escolha a segunda métrica para o relatório.

   Neste exemplo, a variável `New Customers` será utilizada.

1. Na barra lateral, clique em **[!UICONTROL Details]** para exibir informações sobre cada métrica.

   ![Receita por produtos solicitados](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. Na barra lateral, clique no nome de cada métrica para abrir a página de configurações em uma nova guia do navegador. Role para baixo para ver cada componente da métrica, incluindo a consulta da métrica, o filtro e as dimensões.

   ![Configurações de métrica](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Para retornar ao relatório, clique na guia anterior do navegador.

1. No gráfico, passe o mouse sobre alguns pontos de dados em cada linha para ver os valores associados a cada métrica.

## Etapa 2: Adicionar uma Fórmula

1. Na parte superior da barra lateral, clique em **[!UICONTROL Add Formula]**.

   A caixa de fórmulas mostra as métricas como entradas disponíveis `A` e `B`, e inclui uma caixa de entrada onde você pode inserir a fórmula.

   Faça o seguinte:

   * No `Enter your Formula` caixa de entrada, insira `A/B`.

     Isso divide a receita por produtos solicitados pelo número de novos clientes.

   * Definir `Select format` para `123Number`.

   * Na barra lateral, substitua `Untitled` com um nome para a fórmula.

   ![Configurações da Fórmula](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Quando terminar, clique em **[!UICONTROL Apply]**.

   O relatório agora tem uma nova linha para a fórmula, `New Customer Revenue`, e a barra lateral mostra o valor total da receita gerada por novos clientes.

   ![Relatório com Fórmula](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Etapa 3: adicionar um intervalo de datas

1. Clique em **[!UICONTROL Date Range]** no canto superior direito.

1. No `Fixed Date Range` faça o seguinte:

   * Nos calendários, escolha o intervalo de datas.

     Neste exemplo, a temporada de festas é de `November 1` até `December 31`.

   * Em `Select Time Interval`, escolha `Day`.

     ![Intervalo de datas fixo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Quando terminar, clique em **[!UICONTROL Apply]**.

   O relatório agora está limitado à temporada de festas, com um ponto de dados para cada dia.

   ![Intervalo de datas fixo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Etapa 4: Salvar o relatório

Nesta etapa, você salva o relatório como um gráfico e também como uma tabela.

1. Clique em `Untitled Report` na parte superior da página e insira um título descritivo. Neste exemplo, o título do relatório é `2017 Holiday Sales`.

   Em seguida, faça o seguinte:

   * No canto superior direito, clique em **[!UICONTROL Save]**.

   * Para `Type`, aceitar o padrão `Chart` configuração.

   * Escolha o `Dashboard` onde o relatório deve estar disponível.

   * Clique em **[!UICONTROL Save to Dashboard]**.

1. Clique no título do relatório e altere o nome. Neste exemplo, o título do relatório é alterado para `2017 Holiday Sales Data`.

   Em seguida, faça o seguinte:

   * No canto superior direito, clique em **[!UICONTROL Save a Copy]**.

   * Definir `Type` para `Table`.

   * Escolha o `Dashboard` onde o relatório deve estar disponível.

   * Clique em **[!UICONTROL Save a Copy to Dashboard]**.

1. Para ver os relatórios no painel, siga um destes procedimentos:

   * Clique em **[!UICONTROL Go to Dashboard]** na mensagem na parte superior da página.

   * No menu, escolha **[!UICONTROL Dashboards]**. Clique no nome do painel atual para exibir a lista. Em seguida, clique no nome do painel onde o relatório foi salvo.
