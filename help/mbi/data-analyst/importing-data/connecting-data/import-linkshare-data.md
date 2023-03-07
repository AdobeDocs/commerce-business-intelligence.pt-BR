---
title: Importação de dados do Linkshare
description: Saiba como importar dados do Linkshare para o [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importar `Linkshare` dados

Para trazer o seu `Linkshare` entrada de dados [!DNL MBI], você precisa fazer duas coisas:

1. [Exportar os dados do Linkshare no ](#export)
1. [Faça upload da planilha em [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Exportar dados do Linkshare {#export}

1. No seu `Linkshare` conta, vá para **[!UICONTROL Reports** > **Run Reports].**

1. No `Report` selecione **[!UICONTROL Sales & Activity Report]**.

1. Deixe todas as outras opções suspensas como a seleção padrão.

1. No `Date Range` selecione a opção que desejar (`Sun - Sat`, `Mon - Sun`) corresponde ao seu `Start of Week` configurações em [!DNL MBI].

1. Limpe a `Compare Year-Over-Year Data` caixa de seleção

1. Em `Data Type`, selecione `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clique em **[!UICONTROL View Report]**.

1. Clique em **[!UICONTROL Download]**.

   Neste ponto, uma `.csv` arquivo e baixado.

Depois que o arquivo for baixado, você poderá carregá-lo no [!DNL MBI] usando o [`File Upload` recurso](../connecting-data/using-file-uploader.md).
