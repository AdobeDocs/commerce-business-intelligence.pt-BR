---
title: Formatando e Importando Dados Financeiros
description: Saiba como formatar e importar dados financeiros.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Formatar e importar dados financeiros

Este tópico discute a melhor maneira de importar dados financeiros para análise no [!DNL Adobe Commerce Intelligence].

Uma tabela de dados bidimensional entre guias geralmente é o formato usado para dados financeiros. Com valores categorizados por rótulos em colunas e linhas, esse tipo de layout pode ser fácil de visualizar com olhos humanos e ferramentas de planilha, mas não é amigável para bancos de dados.

![Formato de tabela de referência cruzada mostrando dados no layout da tabela dinâmica](../../mbi/assets/crosstab.png)

Para importar e analisar esses dados em [!DNL Commerce Intelligence], a tabela deve ser nivelada em uma lista unidimensional. Quando nivelado, cada valor de dados é categorizado por vários rótulos, todos em uma única linha, onde cada linha é única ou teria um identificador exclusivo, por exemplo, uma coluna de chave primária.

![Formato nivelado mostrando dados no layout de colunas](../../mbi/assets/flattened.png)

## Formatação de arquivos do Excel para importação

Para nivelar uma tabela bidimensional usando uma tabela dinâmica [!DNL Excel]:

1. Abra o arquivo com a tabela de dados bidimensional.
1. Abra o Assistente de Tabela Dinâmica. Em [!DNL Windows], o atalho é `Alt-D`. Em [!DNL Mac OS], digite `Command-Option-P`.
1. Selecione **[!UICONTROL Multiple consolidated ranges]** e clique em **[!UICONTROL Next]**.
1. Selecione **[!UICONTROL I will create the page fields]** e clique em **[!UICONTROL Next]**.
1. Selecione todo o conjunto de dados na tabela bidimensional, incluindo os rótulos. Verifique se `0` está selecionado para o número de campos de página desejados e clique em **[!UICONTROL Next]**.
1. Crie a tabela dinâmica em uma nova planilha e clique em **[!UICONTROL Finish]**.
1. Desmarque os campos de coluna e linha da lista de campos.
1. Clique duas vezes no valor numérico resultante para mostrar os dados de origem nivelados em uma nova planilha.
   ![Lista de campos da tabela dinâmica do Excel mostrando um clique duplo para expandir](../../mbi/assets/pivot-table-double-click.png)
1. Salvar como arquivo `CSV`.

## Encapsulamento

A tabela de dados foi convertida em um formato de lista, preservando todas as suas informações originais, e agora pode ser [importada para [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) para análise.
