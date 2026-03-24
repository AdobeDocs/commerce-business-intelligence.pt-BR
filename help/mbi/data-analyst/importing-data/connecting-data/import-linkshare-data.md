---
title: Importação de dados do Linkshare
description: Saiba como importar dados do Linkshare para o  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 94
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
