---
title: Diferenças entre o SQL e o Data Warehouse Manager
description: Saiba mais sobre as diferenças entre o SQL e o Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# Diferenças entre [!DNL SQL] e [!DNL Data Warehouse Manager]

Há duas diferenças principais entre as colunas criadas em [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) e as criadas com o [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Uma é a dependência dos ciclos de atualização e a outra é como as colunas são salvas em sua conta.

## Colunas na [!DNL SQL Report Builder]

As colunas não dependem dos ciclos de atualização, portanto, não é mais necessário aguardar a conclusão de uma para poder iterar na coluna. Se você cometer um erro, basta pressionar algumas teclas para corrigi-lo - não é mais necessário esperar duas atualizações serem concluídas antes que você possa voltar ao trabalho.

>[!IMPORTANT]
>
>As colunas criadas usando o editor [!DNL SQL] não são salvas na Data Warehouse. Você sempre tem acesso à consulta contendo a coluna, mas se quiser usar a coluna em mais de um relatório, será necessário recriá-la na consulta para cada relatório. Isso significa que as colunas criadas usando o editor [!DNL SQL] não podem ser usadas no [!DNL Report Builder] tradicional.

## Colunas no Data Warehouse Manager

As colunas dependem dos ciclos de atualização, portanto, um ciclo completo deve ser concluído antes de serem editadas. Essas colunas são salvas no Gerenciador do Data Warehouse e podem ser usadas no [!DNL Report Builder] ou [!DNL SQL Report Builder] tradicional.
