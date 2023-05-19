---
title: Importando Dados de Marketing da Afiliada CJ (Junção de Comissões)
description: Saiba como importar dados de Afiliada do CJ (Junção de comissões) para o [!DNL Commerce Intelligence].L Commerce Intelligence] (em inglês).
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importar [!DNL CJ Affiliate] dados

Para importar [!DNL CJ Affiliate (Commission Junction)] entrada de dados [!DNL Adobe Commerce Intelligence], siga as etapas abaixo e anexe o arquivo resultante a um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). O Adobe configurará a tabela de dados da sua conta e permitirá que você continue carregando dados de forma independente.

## Exportar [!DNL CJ Affiliate] Dados

1. No seu [!DNL CJ Affiliate] conta, vá para a página `Reports` guia.

1. No `Performance` selecione `Report Options`.

1. Definir `Performance By` igual a `Program`, `Trend` igual a `Daily`, e `Date Range` igual ao intervalo de datas que está sendo auditado.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecionar `Run Report`.

1. No `File Format` selecione `CSV`.  Clique em **[!UICONTROL Download]**.

   ![exportar dados de afiliados do cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Depois de baixar o arquivo, você pode [fazer upload do arquivo](../connecting-data/using-file-uploader.md) ao seu [!DNL Commerce Intelligence] Data Warehouse.

   Isso cria uma tabela no [!DNL Commerce Intelligence] Data Warehouse que você possa continuar a fazer upload de dados novos no periodicamente. Ao fazer upload do arquivo, siga os requisitos de formatação listados em [Uso do carregador de arquivos](../connecting-data/using-file-uploader.md).
