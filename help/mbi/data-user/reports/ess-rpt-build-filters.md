---
title: Filtros
description: Saiba como usar filtros.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 0854d644cb72b3fc8b8b31a0bf7e8dca4cc99724
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Filtros

Um ou mais filtros podem ser adicionados para limitar os dados usados para produzir um relatório. Cada filtro é uma expressão que inclui uma coluna da tabela associada, um operador e um valor. Por exemplo, para incluir apenas clientes repetidos, você pode criar um filtro que inclua apenas clientes que fizeram mais de um pedido. Vários filtros podem ser usados com operadores `AND/OR` lógicos para adicionar lógica ao relatório.

>[!TIP]
>
>Um relatório pode ter no máximo 3.500 pontos de dados. Para reduzir o número de pontos de dados, use um filtro para reduzir a quantidade de dados usada para gerar o relatório.

O [!DNL Adobe Commerce Intelligence] inclui uma seleção de filtros que você pode usar &quot;prontos para uso (OOTB)&quot; ou modificar para atender às suas necessidades. Não há limite para o número de filtros que você pode criar.

## Para adicionar um filtro:

1. No gráfico, passe o mouse sobre cada ponto de dados.

   Neste relatório, cada ponto de dados mostra o número total de clientes do mês.

1. No painel esquerdo, clique no ícone Filtros (![](../../assets/magento-bi-btn-filter.png)).

   ![Adicionar filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Clique em **[!UICONTROL Add Filter]**.

   Os filtros são numerados alfabeticamente, e o primeiro é `[A]`. As duas primeiras partes do filtro são opções suspensas e a terceira parte é um valor.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Clique na primeira parte do filtro e escolha a coluna que deseja usar como assunto da expressão.

     ![Escolher a Primeira Parte do Filtro](../../assets/magento-bi-report-builder-filter-part1.png)

   * Clique na segunda parte do filtro e escolha o operador.

     ![Escolher o operador](../../assets/magento-bi-report-builder-filter-part2.png)

   * Na terceira parte do filtro, insira o valor necessário para concluir a expressão.

     ![Insira o valor](../../assets/magento-bi-report-builder-filter-part3.png)

   * Quando o filtro estiver concluído, clique em **[!UICONTROL Apply]**.

     O relatório agora inclui apenas clientes repetidos e o número de registros de clientes recuperados para o relatório foi reduzido de 33.000 para 12.600.

     ![Relatório Filtrado](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Na barra lateral, clique no ícone de perspectiva (![ícone de Perspectiva](../../assets/magento-bi-btn-perspective.png)).

   ![Perspectiva](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Na lista de configurações, escolha `Cumulative`. Em seguida, clique em **[!UICONTROL Apply]**.

   ![Perspectiva Cumulativa](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   A perspectiva `Cumulative` distribui a alteração ao longo do tempo, em vez de mostrar as atualizações e reduções irregulares de cada mês.

1. Insira um `Title` para o relatório e clique **[!UICONTROL Save]** nele como `Chart` para o seu painel.

   ![Salvar no Painel](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
