---
title: Dados de difusão esperados
description: Explore as principais tabelas de dados que você pode importar do Spree para o seu [!DNL MBI] conta.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Esperado [!DNL Spree] dados

Depois de ter [conectou o [!DNL Spree] loja](../../../data-analyst/importing-data/integrations/spree.md), você pode usar o [Gerenciador de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes a partir do [!DNL Spree] plataforma para análise.

Este artigo explora as principais tabelas de dados que podem ser importadas do [!DNL Spree] no seu [!DNL MBI] conta, incluindo links para [documentação adicional](https://guides.spreecommerce.org/developer/addresses.html#address) sobre [!DNL Spree] dados.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Users` | A variável `users` A tabela inclui os detalhes da conta de clientes registrados, incluindo email, nome e data de registro do indivíduo. Isso permite analisar diferentes segmentos de clientes e seus comportamentos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | A variável `orders` A tabela serve como base para todas as métricas no nível do pedido. Registrados aqui estão todos os detalhes de pedidos de compras de seu [!DNL Spree] armazenamento, incluindo `completed\_at` (o carimbo de data e hora do pedido), `user\_id` (ID do usuário registrado que fez o pedido). Se o pedido foi feito por um usuário registrado, a variável `user\_id` links para a `users` para permitir a análise do comportamento de compra do usuário. |
| `Line items` | A variável `line\_items` a tabela é filha de `orders` tabela ou `subscriptions`. Ele registra os detalhes do item de linha de um pedido ou de uma assinatura. Para pedidos com vários produtos, cada produto tem sua própria linha de dados nesta tabela, incluindo uma `product\_id` que permite vinculá-lo ao `Products` tabela. |
| `Products` | A variável `products` A tabela registra todos os detalhes do produto para um item vendável no catálogo de Distribuição. Isso permite segmentar suas métricas no nível do item de linha por atributos do produto. |
| `Subscriptions` | Se você tiver uma [!DNL Spree] extensão de subscrições, a variável `subscriptions` A tabela contém as informações de cada assinatura individual, incluindo `created\_at` (a data de início), `cancelled\_at` (a data em que uma assinatura foi cancelada), e a variável `interval` da assinatura. |

{style="table-layout:auto"}

## Relacionados:

* [Conectando [!DNL Spree]](../integrations/spree.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
