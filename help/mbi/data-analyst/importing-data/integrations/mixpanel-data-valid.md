---
title: Validação de dados no Mixpanel
description: Saiba como confirmar que você sincronizou todos os mesmos dados disponíveis diretamente no Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Validação de dados no [!DNL Mixpanel]

Quando [!DNL Adobe Commerce Intelligence] primeiro se conecta ao seu [!DNL Mixpanel] dados, seu Gerente de conta ou Analista pode solicitar que você forneça exportações de dados do [!DNL Mixpanel] para fins de validação. Isso permite confirmar que você sincronizou todos os mesmos dados que estão disponíveis diretamente no [!DNL Mixpanel].

## Processo de exportação de dados: `Events`

1. Visite seu `Segmentation` seção e visualização `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Selecionar `Past 96 Hours` para o intervalo de tempo

   ![](../../../assets/past-96-hours.png)

1. Role para a parte inferior direita do relatório e exporte uma `.csv` arquivo:

   ![](../../../assets/export-csv-mixpanel.png)

1. Envie o `.csv` para o gerente de conta ou analista com o qual você está trabalhando neste processo de validação.
