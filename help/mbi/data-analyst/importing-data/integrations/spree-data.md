---
title: Dados de difusão esperados
description: Explore as principais tabelas de dados que você pode importar do Spree para sua conta  [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI
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
source-wordcount: 263
ht-degree: 0%

---

# Dados [!DNL Spree] esperados

Depois de [conectar seu [!DNL Spree] armazenamento](../../../data-analyst/importing-data/integrations/spree.md), você poderá usar o [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes da sua plataforma [!DNL Spree] para análise.

Este tópico explora as principais tabelas de dados que você pode importar do [!DNL Spree] para sua conta do [!DNL Commerce Intelligence], incluindo links para a [documentação adicional](https://guides.spreecommerce.org/developer/addresses.html#address) sobre os dados do [!DNL Spree].

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Users` | A tabela `users` inclui os detalhes da conta de clientes registrados, incluindo email, nome e data de registro do indivíduo. Isso permite analisar diferentes segmentos de clientes e seus comportamentos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | A tabela `orders` serve como base para todas as suas métricas no nível do pedido. Registrados aqui estão todos os detalhes do pedido de compras da sua loja [!DNL Spree], incluindo `completed\_at` (o carimbo de data e hora do pedido), `user\_id` (ID do usuário registrado que fez o pedido). Se o pedido foi feito por um usuário registrado, o `user\_id` vincula de volta à tabela `users` para permitir a análise do comportamento de compra do usuário. |
| `Line items` | A tabela `line\_items` é filha da tabela `orders` ou `subscriptions`. Ele registra os detalhes do item de linha de um pedido ou de uma assinatura. Para pedidos com vários produtos, cada produto tem sua própria linha de dados nesta tabela, incluindo uma `product\_id` que permite vinculá-la à tabela `Products`. |
| `Products` | A tabela `products` registra todos os detalhes do produto para um item comercializável no catálogo de páginas espelhadas. Isso permite segmentar suas métricas no nível do item de linha por atributos do produto. |
| `Subscriptions` | Se você tiver uma extensão de assinaturas [!DNL Spree], a tabela `subscriptions` conterá as informações de cada assinatura individual, incluindo `created\_at` (a data de início), `cancelled\_at` (a data de cancelamento de uma assinatura) e `interval` da assinatura. |

{style="table-layout:auto"}

## Relacionados:

* [Conectando [!DNL Spree]](../integrations/spree.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
