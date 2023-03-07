---
title: Dados de distribuição esperados
description: Explore as principais tabelas de dados que você pode importar do Stripe para o [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Esperado [!DNL Stripe] dados

Depois [você conectou o [!DNL Stripe] account](../integrations/stripe.md), você pode usar o [Gerenciador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este artigo explora as principais tabelas de dados que podem ser importadas do [!DNL Stripe] em [!DNL MBI]. Após a conclusão da configuração, as tabelas a seguir serão criadas no Data Warehouse. Clique nos links na coluna Nome da tabela para saber mais sobre os atributos em cada tabela.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Os objetos do cliente permitem que você execute encargos recorrentes e rastreie vários encargos associados ao mesmo cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Esta tabela contém informações sobre encargos com cartões de crédito e débito, incluindo valor, moeda, status, ID do cliente e muito mais. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Esta tabela contém informações sobre um desconto por porcentagem ou por valor que você pode desejar aplicar a um cliente. Os cupons se aplicam apenas a faturas; eles não se aplicam a encargos únicos. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Essa tabela contém informações sobre faturas, incluindo o valor devido, assinaturas, itens de fatura, ajustes de rateio automático e muito mais. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Essa tabela contém as informações de preços para diferentes produtos e níveis de recursos do site. Por exemplo, você pode ter um plano de US$ 10/mês para recursos básicos e um plano de US$ 20/mês para recursos premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Esta tabela contém os detalhes dos planos de assinatura aos quais seus clientes pertencem. Os atributos incluem ID do cliente, status, cancelado/encerrado em datas, percentual de imposto, informações de avaliação e muito mais. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Os eventos informam sobre algo interessante que aconteceu em uma conta do. [Quando um evento interessante ocorre](https://stripe.com/docs/api/events/types), um novo objeto de evento será criado. Por exemplo, quando um encargo tem êxito `charge.succeeded` evento for criado; ou, quando uma fatura não puder ser paga, um `invoice.payment\_failed` evento é criado. |

{style="table-layout:auto"}

>[!NOTE]
>
>Muitas solicitações de API podem fazer com que vários eventos sejam criados. Por exemplo, se você criar uma assinatura para um cliente, você receberá uma `customer.subscription.created` evento e um  `charge.succeeded` evento.

## Relacionados:

* [Conectando [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
