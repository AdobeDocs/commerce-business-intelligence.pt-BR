---
title: Esperado[!DNL Google ECommerce]dados
description: Saiba quais tipos de dados são compartilhados com o Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Esperado[!DNL Google ECommerce] dados

Depois que o [!DNL Google ECommerce] a conta foi conectada com sucesso [!DNL Commerce Intelligence], o sistema começará a importar dados para uma tabela denominada `ecommerce`. Esta tabela registra uma linha de dados para cada transação. Isso inclui as seguintes colunas de dados no nível do pedido:

| Nome da coluna | Descrição |
|-----|-----|
| `\_id` | Essa coluna é a chave primária. |
| `accountId` | Essa coluna contém a ID da conta associada à [!DNL Google Analytics] Conta de comércio eletrônico. |
| `profileName` | Essa coluna contém os [!DNL Google Analytics] nome do perfil. |
| `profileId` | Essa coluna contém os [!DNL Google Analytics] ID do perfil. |
| `socialNetwork` | Essa coluna contém o nome da rede social (por exemplo, [!DNL Facebook]ou [!DNL YouTube]) |
| `campaign` | Essa coluna contém o nome da campanha (por exemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Essa coluna contém o nome da mídia (por exemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Essa coluna contém o nome de origem. (por exemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Essa coluna contém a descrição da palavra-chave (por exemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Essa coluna contém a ID do pedido. Isso é usado para unir os dados de referência de volta aos dados de pedidos. |
| `updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. |

{style="table-layout:auto"}
