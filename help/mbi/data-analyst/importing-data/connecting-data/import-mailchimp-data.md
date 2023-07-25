---
title: Importar dados do MailChimp
description: Saiba como importar dados do MailChimp para o [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Importar [!DNL Mailchimp] dados

Para obter uma visão abrangente de seus esforços de campanha, você pode importar seus [!DNL Mailchimp] enviar dados da campanha por email para o [!DNL Commerce Intelligence]. Para concluir a importação, é necessário fazer o seguinte para cada [!DNL Mailchimp] campanha que você tem:

## Exportar dados de aberturas {#opens}

1. Depois de fazer logon no [!DNL Mailchimp], vá para a `Campaigns` guia.

   ![importar mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Clique em **[!UICONTROL View Report]**, ao lado do nome da campanha.

   ![importar mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Clique em **[!UICONTROL Opened]** número.

   ![importar mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Clique em **[!UICONTROL Export]** e salve a variável `.csv` arquivo.

   É necessário adicionar `primary key`, `date (mm/dd/yyyy)`, e `campaign name` para esse arquivo. Verifique se `primary keys` são exclusivos para cada linha.

   ![importar mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportar dados de cliques {#clicks}

1. Volte para a `View Report` para a campanha.

1. Clique no número que `Clicked`.

   ![importar mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Clique no número sob o `Total Clicks` OU `Unique Clicks` coluna.

   ![importar mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Clique em **[!UICONTROL Export]** e salve a variável `.csv` arquivo.

   É necessário adicionar `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`, e `URL` para esse arquivo. Não é necessário adicionar o URL completo, apenas algo que permite saber o que foi clicado.

   ![importar mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Repita as etapas 3 e 4 para cada URL clicado em seu email, combinando todos os dados no mesmo `.csv` arquivo quando concluído.

## Exportar dados enviados {#sent}

1. Acesse o `Campaigns` guia de [!DNL Mailchimp].

1. Clique em **[!UICONTROL View Report]** ao lado do nome da campanha.

1. Clique no número ao lado de `Recipients`.

   ![importar mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Clique em **[!UICONTROL Export]** e salve a variável `.csv` arquivo.

   É necessário adicionar `Primary Key`, `date (mm/dd/yyyy)`, e `campaign name` para esse arquivo.

   ![importar mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparar arquivos para upload no [!DNL Commerce Intelligence] {#upload}

Cada arquivo - `Opens`, `Clicks`, e `Sent` - deve ser carregado para [!DNL Commerce Intelligence] como um arquivo separado. O Adobe recomenda nomear os arquivos usando esta convenção de nomenclatura: `MailChimp\_ACTION\_DATE`. Substituir `ACTION` com `Open`, `Click`ou `Sent`e substitua `DATE` data de exportação.

Quando estiver pronto para fazer upload dos arquivos, use o [`File Upload` recurso](../connecting-data/using-file-uploader.md) para trazer os dados para a Data Warehouse.
