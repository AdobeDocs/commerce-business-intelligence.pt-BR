---
title: Importar dados de gasto de anúncio do Bing
description: Saiba como importar dados de gastos com publicidade do Bing para  [!DNL Commerce Intelligence]  para análise.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 0%

---

# Importar dados de [!DNL Bing]

Para importar dados de gastos com publicidade do [!DNL Bing] para o [!DNL Adobe Commerce Intelligence] para análise, basta exportar os dados do [!DNL Bing Ads Editor] em um formato `.csv` e carregá-los no [!DNL Commerce Intelligence] de acordo com as etapas abaixo.

## [!DNL Bing Ads Editor]

Para exportar os dados do [!DNL Bing Ads], é necessário ter o [!DNL Bing Ads Editor] instalado. Você pode encontrar um download gratuito para [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## Exportação de dados de [!DNL Bing Ads]

1. No painel `Browser` de [!DNL Bing Ads Editor], clique com o botão direito do mouse na campanha ou no grupo de anúncios que você deseja exportar e clique em **[!UICONTROL Export]**.
1. Na caixa de diálogo `Export`, clique em **[!UICONTROL Export]**.
1. Na caixa de diálogo `Save As`, clique na pasta onde deseja salvar o arquivo de exportação.
1. Na caixa `File name`, escolha um nome para sua exportação de arquivo.
1. Clique em **[!UICONTROL Save]**.
1. Depois que o arquivo for baixado, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) para realizar um primeiro carregamento em seu nome e configurar as dimensões de back-end necessárias.
