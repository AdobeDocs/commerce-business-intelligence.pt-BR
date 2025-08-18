---
title: Dados de difusão esperados
description: Explore as principais tabelas de dados que você pode importar do Spree para sua conta  [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
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
