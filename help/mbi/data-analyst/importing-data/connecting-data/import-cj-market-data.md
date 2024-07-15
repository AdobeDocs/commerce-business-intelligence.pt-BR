---
title: Importando Dados de Marketing da Afiliada CJ (Junção de Comissões)
description: Saiba como importar dados de Afiliada CJ (Junção de Comissões) para o  [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Importar dados de [!DNL CJ Affiliate]

Para importar dados do [!DNL CJ Affiliate (Commission Junction)] para o [!DNL Adobe Commerce Intelligence], siga as etapas abaixo e anexe o arquivo resultante a um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). O Adobe configurará a tabela de dados da sua conta e permitirá que você continue carregando dados de forma independente.

## Exportar dados de [!DNL CJ Affiliate]

1. Na conta do [!DNL CJ Affiliate], vá para a guia `Reports`.

1. Na guia `Performance`, selecione `Report Options`.

1. Defina `Performance By` igual a `Program`, `Trend` igual a `Daily` e `Date Range` igual ao intervalo de datas que está sendo auditado.

   ![exportar-cj-afiliar-dados](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecione `Run Report`.

1. Na lista suspensa `File Format`, selecione `CSV`.  Clique em **[!UICONTROL Download]**.

   ![exportar dados de afiliado do cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Depois de baixar o arquivo, você pode [carregá-lo](../connecting-data/using-file-uploader.md) na Data Warehouse [!DNL Commerce Intelligence].

   Isso cria uma tabela na Data Warehouse do [!DNL Commerce Intelligence] na qual você pode continuar carregando dados novos periodicamente. Ao carregar o arquivo, siga os requisitos de formatação listados em [Usando o Carregador de Arquivo](../connecting-data/using-file-uploader.md).
