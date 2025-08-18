---
title: Importar dados de gasto de anúncio do Bing
description: Saiba como importar dados de gastos com publicidade do Bing para  [!DNL Commerce Intelligence]  para análise.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '131'
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
1. Depois que o arquivo for baixado, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para realizar um primeiro carregamento em seu nome e configurar as dimensões de back-end necessárias.
