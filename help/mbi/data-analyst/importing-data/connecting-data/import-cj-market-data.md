---
title: Importando Dados de Marketing da Afiliada CJ (Junção de Comissões)
description: Saiba como importar dados de Afiliada CJ (Junção de Comissões) para o  [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# Importar dados de [!DNL CJ Affiliate]

Para importar dados do [!DNL CJ Affiliate (Commission Junction)] para o [!DNL Adobe Commerce Intelligence], siga as etapas abaixo e anexe o arquivo resultante a um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). O Adobe configurará a tabela de dados para sua conta e permitirá que você continue carregando os dados de forma independente.

## Exportar dados de [!DNL CJ Affiliate]

1. Na conta do [!DNL CJ Affiliate], vá para a guia `Reports`.

1. Na guia `Performance`, selecione `Report Options`.

1. Defina `Performance By` igual a `Program`, `Trend` igual a `Daily` e `Date Range` igual ao intervalo de datas que está sendo auditado.

   ![exportar-cj-afiliar-dados](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecione `Run Report`.

1. Na lista suspensa `File Format`, selecione `CSV`.  Clique em **[!UICONTROL Download]**.

   ![exportar dados de afiliado do cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Depois de baixar o arquivo, você pode [carregá-lo](../connecting-data/using-file-uploader.md) no Data Warehouse [!DNL Commerce Intelligence].

   Isso cria uma tabela no Data Warehouse do [!DNL Commerce Intelligence] na qual você pode continuar carregando dados novos periodicamente. Ao carregar o arquivo, siga os requisitos de formatação listados em [Usando o Carregador de Arquivo](../connecting-data/using-file-uploader.md).
