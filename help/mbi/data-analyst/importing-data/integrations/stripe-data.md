---
title: Dados esperados do Stripe
description: Explore as principais tabelas de dados que você pode importar do Stripe para o Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/dCiDusso9q9gvZOXKeHcDcuVK-jCXkqR3pQg6eTKzdo
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 0%

---

# Dados [!DNL Stripe] esperados

Depois de [conectar sua [!DNL Stripe] conta](../integrations/stripe.md), você poderá usar o [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico explora as principais tabelas de dados que você pode importar de [!DNL Stripe] para [!DNL Commerce Intelligence]. Após a conclusão da configuração, as tabelas a seguir serão criadas no Data Warehouse. Clique nos links na coluna Nome da tabela para saber mais sobre os atributos em cada tabela.

| **Nome da Tabela** | **Descrição** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Os objetos do cliente permitem que você execute encargos recorrentes e rastreie vários encargos associados ao mesmo cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Esta tabela contém informações sobre encargos com cartões de crédito e débito, incluindo valor, moeda, status, ID do cliente e muito mais. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Esta tabela contém informações sobre um desconto por porcentagem ou por valor que você pode desejar aplicar a um cliente. Os cupons se aplicam apenas a faturas; eles não se aplicam a encargos únicos. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Essa tabela contém informações sobre faturas, incluindo o valor devido, assinaturas, itens de fatura, ajustes de rateio automático e muito mais. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Essa tabela contém as informações de preços para diferentes produtos e níveis de recursos do site. Por exemplo, você pode ter um plano de US$ 10/mês para recursos básicos e um plano de US$ 20/mês para recursos premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Esta tabela contém os detalhes dos planos de assinatura aos quais seus clientes pertencem. Os atributos incluem ID do cliente, status, cancelado/encerrado em datas, percentual de imposto, informações de avaliação e muito mais. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Os eventos informam sobre algo interessante que aconteceu em uma conta do. [Quando um evento interessante ocorre](https://stripe.com/docs/api/events/types), um novo objeto de evento é criado. Por exemplo, quando um evento `charge.succeeded` de cobrança bem-sucedida é criado; ou, quando uma fatura não pode ser paga, um evento `invoice.payment\_failed` é criado. |

{style="table-layout:auto"}

>[!NOTE]
>
>Muitas solicitações de API podem fazer com que vários eventos sejam criados. Por exemplo, se você criar uma assinatura para um cliente, você receberá um evento `customer.subscription.created` e um evento `charge.succeeded`.

## Relacionados:

* [Conectando [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
