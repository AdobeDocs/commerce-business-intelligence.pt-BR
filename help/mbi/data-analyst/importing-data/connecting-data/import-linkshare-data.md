---
title: Importação de dados do Linkshare
description: Saiba como importar dados do Linkshare para [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Importar `Linkshare` dados

Para trazer seus `Linkshare` dados em [!DNL MBI], você precisa fazer duas coisas:

1. [Exportar os dados do Linkshare em ](#export)
1. [Faça upload da planilha em [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Exportar dados do Linkshare {#export}

1. Em seu `Linkshare` conta, vá para **[!UICONTROL Reports** > **Run Reports].**

1. No `Report` lista suspensa, selecione **[!UICONTROL Sales & Activity Report]**.

1. Deixe todas as outras opções suspensas como a seleção padrão.

1. No `Date Range` , selecione a opção que desejar (`Sun - Sat`, `Mon - Sun`) corresponde à sua `Start of Week` configurações em [!DNL MBI].

1. Limpe o `Compare Year-Over-Year Data` caixa de seleção.

1. Em `Data Type`, selecione `Transaction Date`.

   ![importar\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clique em **[!UICONTROL View Report]**.

1. Clique em **[!UICONTROL Download]**.

   Neste ponto, um `.csv` será criado e baixado.

Após o download do arquivo, é possível fazer upload para [!DNL MBI] usando o [`File Upload` recurso](../connecting-data/using-file-uploader.md).
