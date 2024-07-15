---
title: Importação de dados do Linkshare
description: Saiba como importar dados do Linkshare para o  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importar dados de [!DNL Linkshare]

Para trazer seus dados do [!DNL Linkshare] para o [!DNL Adobe Commerce Intelligence], você precisa fazer o seguinte:

1. [Exportar os dados do Linkshare no ](#export)
1. [Carregar a planilha em  [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exportar dados do Linkshare {#export}

1. Na sua conta do [!DNL Linkshare], vá para **[!UICONTROL Reports** > **Run Reports].**

1. Na lista suspensa `Report`, selecione **[!UICONTROL Sales & Activity Report]**.

1. Deixe todas as outras opções suspensas como a seleção padrão.

1. Na lista suspensa `Date Range`, selecione qualquer opção (`Sun - Sat`, `Mon - Sun`) que corresponda às suas configurações de `Start of Week` em [!DNL Commerce Intelligence].

1. Desmarque a caixa de seleção `Compare Year-Over-Year Data`.

1. Em `Data Type`, selecione `Transaction Date`.

   ![importação\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clique em **[!UICONTROL View Report]**.

1. Clique em **[!UICONTROL Download]**.

   Neste ponto, um arquivo `.csv` foi baixado.

Depois que o arquivo for baixado, você poderá carregá-lo para [!DNL Commerce Intelligence] usando o recurso [`File Upload`](../connecting-data/using-file-uploader.md).
