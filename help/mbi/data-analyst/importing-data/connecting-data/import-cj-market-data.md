---
title: Importação de dados de marketing de afiliados do CJ (Junção da Comissão)
description: Saiba como importar dados de afiliado do CJ (Junção da Comissão) para o [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Importar `CJ Affiliate` dados

Para importar `CJ Affiliate` (Junção da Comissão) dados em [!DNL MBI], siga as etapas abaixo e anexe o arquivo resultante a um tíquete de suporte. Configuraremos a tabela de dados em sua conta e permitiremos que você continue carregando dados de maneira independente.

## Exportar `CJ Affiliate` Dados

1. Em seu `CJ Affiliate` , vá para a `Reports` guia .

1. No `Performance` guia , selecione `Report Options`.

1. Definir `Performance By` equal to `Program`, `Trend` equal to `Daily`e `Date Range` igual ao intervalo de datas que está sendo auditado.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecionar `Run Report`.

1. No `File Format` lista suspensa, selecione `CSV`.  Clique em **[!UICONTROL Download]**.

   ![exportar dados afiliados do cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Após o download do arquivo, é possível [fazer upload do arquivo](../connecting-data/using-file-uploader.md) para [!DNL MBI] data warehouse.

   Isso cria uma nova tabela no [!DNL MBI] data warehouse para o qual você pode continuar carregando dados novos periodicamente. Ao fazer upload do arquivo, siga os requisitos de formatação listados em [Uso do Carregador de Arquivos](../connecting-data/using-file-uploader.md).
