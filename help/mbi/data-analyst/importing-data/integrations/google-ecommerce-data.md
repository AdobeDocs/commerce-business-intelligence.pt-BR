---
title: Esperado[!DNL Google ECommerce]dados
description: Saiba quais tipos de dados são compartilhados com o Google Commerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Esperado[!DNL Google ECommerce] dados

Depois de [!DNL Google ECommerce] a conta foi conectada com êxito ao [!DNL MBI], o sistema começará a importar dados em uma tabela denominada `ecommerce`. Esta tabela registrará uma linha de dados para cada transação. Isso inclui as seguintes colunas de dados no nível do pedido:

| Nome da coluna | Descrição |
|-----|-----|
| `\_id` | Essa coluna é a chave primária. |
| `accountId` | Essa coluna contém a ID da conta associada à [!DNL Google Analytics] conta de comércio eletrônico. |
| `profileName` | Essa coluna contém seu [!DNL Google Analytics] nome do perfil. |
| `profileId` | Essa coluna contém seu [!DNL Google Analytics] ID do perfil. |
| `socialNetwork` | Essa coluna contém o nome da rede social (por exemplo, [!DNL Facebook]ou [!DNL YouTube]) |
| `campaign` | Essa coluna contém o nome da campanha (por exemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Essa coluna contém o nome médio (por exemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Essa coluna contém o nome de origem. (por exemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Essa coluna contém a descrição da palavra-chave (por exemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Essa coluna contém a ID do pedido. Isso será usado para unir os dados de referência aos dados de seus pedidos. |
| `updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. |

{style=&quot;table-layout:auto&quot;}
