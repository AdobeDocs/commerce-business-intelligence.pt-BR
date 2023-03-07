---
title: Importando Dados de Marketing da Afiliada CJ (Junção de Comissões)
description: Saiba como importar dados de Afiliada do CJ (Junção de comissões) para o [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Importar `CJ Affiliate` dados

Para importar `CJ Affiliate` (Junção da Comissão) em [!DNL MBI], siga as etapas abaixo e anexe o arquivo resultante a um tíquete de suporte. O Adobe configurará a tabela de dados da sua conta e permitirá que você continue carregando dados de forma independente.

## Exportar `CJ Affiliate` Dados

1. No seu `CJ Affiliate` conta, vá para a página `Reports` guia.

1. No `Performance` selecione `Report Options`.

1. Definir `Performance By` igual a `Program`, `Trend` igual a `Daily`, e `Date Range` igual ao intervalo de datas que está sendo auditado.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecionar `Run Report`.

1. No `File Format` selecione `CSV`.  Clique em **[!UICONTROL Download]**.

   ![exportar dados de afiliados do cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Depois de baixar o arquivo, você pode [fazer upload do arquivo](../connecting-data/using-file-uploader.md) ao seu [!DNL MBI] Data Warehouse.

   Isso cria uma tabela no [!DNL MBI] Data Warehouse que você possa continuar a fazer upload de dados novos no periodicamente. Ao fazer upload do arquivo, siga os requisitos de formatação listados em [Uso do carregador de arquivos](../connecting-data/using-file-uploader.md).
