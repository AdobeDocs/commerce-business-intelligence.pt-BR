---
title: Importação de dados do Linkshare
description: Saiba como importar dados do Linkshare para o [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# Importar [!DNL Linkshare] dados

Para trazer o seu [!DNL Linkshare] entrada de dados [!DNL Adobe Commerce Intelligence], você precisa fazer duas coisas:

1. [Exportar os dados do Linkshare no ](#export)
1. [Faça upload da planilha em [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exportar dados do Linkshare {#export}

1. No seu [!DNL Linkshare] conta, vá para **[!UICONTROL Reports** > **Run Reports].**

1. No `Report` selecione **[!UICONTROL Sales & Activity Report]**.

1. Deixe todas as outras opções suspensas como a seleção padrão.

1. No `Date Range` selecione a opção que desejar (`Sun - Sat`, `Mon - Sun`) corresponde ao seu `Start of Week` configurações em [!DNL Commerce Intelligence].

1. Limpe a `Compare Year-Over-Year Data` caixa de seleção

1. Em `Data Type`, selecione `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clique em **[!UICONTROL View Report]**.

1. Clique em **[!UICONTROL Download]**.

   Neste ponto, uma `.csv` arquivo e baixado.

Depois que o arquivo for baixado, você poderá carregá-lo no [!DNL Commerce Intelligence] usando o [`File Upload` recurso](../connecting-data/using-file-uploader.md).
