---
title: Dados de propagação esperados
description: Explore as principais tabelas de dados que você pode importar do Spree para o seu [!DNL MBI] conta.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Esperado [!DNL Spree] dados

Depois de [conectou seu [!DNL Spree] loja](../../../data-analyst/importing-data/integrations/spree.md), você pode usar o [Gerenciador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes da [!DNL Spree] plataforma para análise.

Neste artigo, exploramos as principais tabelas de dados que podem ser importadas de [!DNL Spree] em seu [!DNL MBI] , incluindo links para [documentação adicional](https://guides.spreecommerce.org/developer/addresses.html#address) about [!DNL Spree] dados.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Users` | O `users` A tabela inclui os detalhes da conta para clientes registrados, incluindo o email do indivíduo, o nome e a data de registro. Isso permite analisar diferentes segmentos de clientes e seus comportamentos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | O `orders` A tabela serve como base para todas as métricas no nível do pedido. Registrados aqui estão todos os detalhes de compra de [!DNL Spree] armazenamento, incluindo `completed\_at` (o carimbo de data e hora do pedido), `user\_id` (id do usuário registrado que fez o pedido). Se o pedido foi feito por um usuário registrado, a variável `user\_id` voltará ao link para `users` tabela para permitir a análise do comportamento de compra do usuário. |
| `Line items` | O `line\_items` é um filho de `orders` tabela ou `subscriptions`. Ele registra os detalhes do item de linha de um pedido ou de uma assinatura. Para pedidos com vários produtos, cada produto terá sua própria linha de dados nesta tabela, incluindo uma `product\_id` que permite vinculá-lo ao `Products` tabela. |
| [`Products`](https://guides.spreecommerce.com/developer/products.html#overview) | O `products` A tabela registra todos os detalhes do produto para um item que pode ser vendido no catálogo do Spree. Isso permite segmentar suas métricas em nível de item por atributos de produto. |
| `Subscriptions` | Se você tiver uma [!DNL Spree] extensão de assinaturas, o `subscriptions` tabela contém as informações de cada assinatura individual, incluindo `created\_at` (a data de início), `cancelled\_at` (a data em que uma assinatura foi cancelada), e a variável `interval` da assinatura. |

{style=&quot;table-layout:auto&quot;}

## Relacionadas:

* [Conexão [!DNL Spree]](../integrations/spree.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
