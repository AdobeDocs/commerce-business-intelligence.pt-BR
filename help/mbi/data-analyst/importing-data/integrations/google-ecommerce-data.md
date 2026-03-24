---
title: Dados [!DNL Google ECommerce] esperados
description: Saiba quais tipos de dados são compartilhados com o Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# Dados [!DNL Google ECommerce] esperados

Depois que sua conta do [!DNL Google ECommerce] for conectada com êxito ao [!DNL Commerce Intelligence], o sistema começará a importar dados para uma tabela denominada `ecommerce`. Esta tabela registra uma linha de dados para cada transação. Isso inclui as seguintes colunas de dados no nível do pedido:

| Nome da coluna | Descrição |
|-----|-----|
| `\_id` | Essa coluna é a chave primária. |
| `accountId` | Essa coluna contém a ID da conta associada à sua conta de eCommerce do [!DNL Google Analytics]. |
| `profileName` | Esta coluna contém seu nome de perfil [!DNL Google Analytics]. |
| `profileId` | Esta coluna contém sua ID de perfil do [!DNL Google Analytics]. |
| `socialNetwork` | Esta coluna contém o nome da rede social (por exemplo, [!DNL Facebook] ou [!DNL YouTube]) |
| `campaign` | Esta coluna contém o nome da campanha (por exemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Esta coluna contém o nome médio (por exemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Essa coluna contém o nome de origem. (por exemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Esta coluna contém a descrição da palavra-chave (por exemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Essa coluna contém a ID do pedido. Isso é usado para unir os dados de referência de volta aos dados de pedidos. |
| `updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. |

{style="table-layout:auto"}
