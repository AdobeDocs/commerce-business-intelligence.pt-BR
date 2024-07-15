---
title: Dados [!DNL Google ECommerce] esperados
description: Saiba quais tipos de dados são compartilhados com o Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
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
