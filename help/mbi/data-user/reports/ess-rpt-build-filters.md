---
title: Filtros
description: Saiba como usar filtros.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/XnfqSloTGv-hfUbUwPpFbWVsvs8DPrYdzMmTdERSr4Q
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 364
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

1. No painel esquerdo, clique no ícone Filtros (![Ícone Filtro](../../assets/magento-bi-btn-filter.png)).

   ![Adicionar filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Clique em **[!UICONTROL Add Filter]**.

   Os filtros são numerados alfabeticamente, e o primeiro é `[A]`. As duas primeiras partes do filtro são opções suspensas e a terceira parte é um valor.

   ![Interface de filtro mostrando a opção de adição de filtro](../../assets/magento-bi-report-builder-filter-add-a.png)

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
