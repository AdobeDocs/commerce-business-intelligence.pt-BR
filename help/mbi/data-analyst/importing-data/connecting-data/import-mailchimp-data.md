---
title: Importar dados do MailChimp
description: Saiba como importar dados do MailChimp para o [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%
---
# Importar dados de [!DNL Mailchimp]

Para obter uma visão abrangente de seus esforços de campanha, você pode importar os dados da campanha por email do [!DNL Mailchimp] para o [!DNL Commerce Intelligence]. Para concluir a importação, é necessário fazer o seguinte para cada campanha do [!DNL Mailchimp] que você tiver:

## Exportar dados de aberturas {#opens}

1. Depois de fazer logon no [!DNL Mailchimp], vá para a guia `Campaigns`.

   ![importar mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Clique em **[!UICONTROL View Report]**, ao lado do nome da campanha.

   ![importar mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Clique no número **[!UICONTROL Opened]**.

   ![importar mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Clique em **[!UICONTROL Export]** e salve o arquivo `.csv`.

   Você deve adicionar `primary key`, `date (mm/dd/yyyy)` e `campaign name` colunas a este arquivo. Verifique se os `primary keys` são exclusivos para cada linha.

   ![importar mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportar dados de cliques {#clicks}

1. Volte para a tela `View Report` da campanha.

1. Clique no número que `Clicked`.

   ![importar mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Clique no número sob a coluna `Total Clicks` OU `Unique Clicks`.

   ![importar mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Clique em **[!UICONTROL Export]** e salve o arquivo `.csv`.

   Você deve adicionar `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` e `URL` colunas a este arquivo. Não é necessário adicionar o URL completo, apenas algo que permite saber o que foi clicado.

   ![importar mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Repita as etapas 3 e 4 para cada URL clicada em seu email, combinando todos os dados no mesmo arquivo `.csv` quando terminar.

## Exportar dados enviados {#sent}

1. Vá para a guia `Campaigns` de [!DNL Mailchimp].

1. Clique em **[!UICONTROL View Report]** ao lado do nome da campanha.

1. Clique no número ao lado de `Recipients`.

   ![importar mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Clique em **[!UICONTROL Export]** e salve o arquivo `.csv`.

   Você deve adicionar `Primary Key`, `date (mm/dd/yyyy)` e `campaign name` colunas a este arquivo.

   ![importar mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparar arquivos para carregá-los em [!DNL Commerce Intelligence] {#upload}

Cada arquivo - `Opens`, `Clicks` e `Sent` - deve ser carregado para [!DNL Commerce Intelligence] como um arquivo separado. A Adobe recomenda nomear os arquivos usando esta convenção de nomenclatura: `MailChimp\_ACTION\_DATE`. Substitua `ACTION` por `Open`, `Click` ou `Sent` e substitua `DATE` pela data de exportação.

Quando estiver pronto para carregar os arquivos, use o recurso [`File Upload`](../connecting-data/using-file-uploader.md) para trazer os dados para sua Data Warehouse.
