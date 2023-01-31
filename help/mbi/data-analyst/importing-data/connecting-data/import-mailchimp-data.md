---
title: Importar dados do MailChimp
description: Saiba como importar dados do MailChimp para o [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Importar `MailChimp` dados

Para obter uma visão abrangente dos seus esforços de campanha, você pode importar seu `MailChimp` enviar dados da campanha por email para [!DNL MBI]. Para concluir a importação, você precisa fazer o seguinte para cada `MailChimp` campanha que você possui:

## Exportar dados de aberturas {#opens}

1. Depois de fazer logon em `MailChimp`, acesse o `Campaigns` guia .

   ![importar mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Clique em **[!UICONTROL View Report]**, ao lado do nome da campanha.

   ![importar mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Clique no botão **[!UICONTROL Opened]** número.

   ![importar mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Clique em **[!UICONTROL Export]** e salve o `.csv` arquivo.

   Você precisará adicionar `primary key`, `date (mm/dd/yyyy)`e `campaign name` para este arquivo. Certifique-se de que o `primary keys` são exclusivas para cada linha.

   ![importar mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportar dados de cliques {#clicks}

1. Navegue de volta para a `View Report` para a campanha.

1. Clique no número que `Clicked`.

   ![importar mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Clique em OU no número sob a variável `Total Clicks` OU `Unique Clicks` coluna.

   ![importar mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Clique em **[!UICONTROL Export]** e salve o `.csv` arquivo.

   Você precisará adicionar `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`e `URL` para este arquivo. Não é necessário adicionar o URL completo, apenas algo que permitirá que você saiba o que foi clicado.

   ![importar mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Repita as etapas 3 e 4 para cada URL clicado em seu email, combinando todos os dados no mesmo `.csv` quando terminar.

## Exportar dados enviados {#sent}

1. Acesse o `Campaigns` guia de MailChimp.

1. Clique em **[!UICONTROL View Report]** ao lado do nome da campanha.

1. Clique no número ao lado de `Recipients`.

   ![importar mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Clique em **[!UICONTROL Export]** e salve o `.csv` arquivo.

   Você precisará adicionar `Primary Key`, `date (mm/dd/yyyy)`e `campaign name` para este arquivo.

   ![importar mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparar arquivos para upload no [!DNL MBI] {#upload}

Cada arquivo - `Opens`, `Clicks`e `Sent` - deve ser carregado para [!DNL MBI] como um arquivo separado. Também recomendamos que você nomeie os arquivos usando essa convenção de nomenclatura: `MailChimp\_ACTION\_DATE`. Substituir `ACTION` com `Open`, `Click`ou `Sent`e substituir `DATE` com a data de exportação.

Quando estiver pronto para fazer upload dos arquivos, use a variável [`File Upload` recurso](../connecting-data/using-file-uploader.md) para trazer os dados para o data warehouse.
