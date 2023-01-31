---
title: Dados de distribuição esperados
description: Explore as principais tabelas de dados que você pode importar do Stripe para [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Esperado [!DNL Stripe] dados

Depois [você conectou seu [!DNL Stripe] account](../integrations/stripe.md), você pode usar o [Gerenciador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise.

Neste artigo, exploramos as principais tabelas de dados que podem ser importadas de [!DNL Stripe] em [!DNL MBI]. Depois que a configuração for concluída, as tabelas a seguir serão criadas em seu data warehouse. Clique nos links na coluna Nome da tabela para saber mais sobre os atributos em cada tabela.

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | Os objetos do cliente permitem que você execute encargos recorrentes e rastreie vários encargos que estão associados ao mesmo cliente. |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | Esta tabela contém informações sobre encargos para cartões de crédito e débito, incluindo valor, moeda, status, ID do cliente e muito mais. |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | Esta tabela contém informações sobre um desconto por porcentagem ou quantia de desconto que pode ser aplicado a um cliente. Observe que os cupons se aplicam apenas às faturas; não se aplicam a taxas pontuais. |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | Esta tabela contém informações sobre NFFs, incluindo valor devido, assinaturas, itens de NFF, quaisquer ajustes de pro rata automáticos e muito mais. |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | Esta tabela contém as informações de preços para diferentes produtos e níveis de recursos do site. Por exemplo, você pode ter um plano de US$ 10 por mês para recursos básicos e um plano de US$ 20 por mês para recursos premium. |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | Esta tabela contém os detalhes dos planos de assinatura aos quais seus clientes pertencem. Os atributos incluem ID do cliente, status, cancelado/encerrado em datas, porcentagem de imposto, informações de avaliação e muito mais. |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | Os eventos informam sobre algo interessante que acabou de acontecer em uma conta. [Quando um evento interessante ocorre](https://stripe.com/docs/api/curl#event_types), um novo objeto de evento é criado. Por exemplo, quando uma cobrança é bem-sucedida `charge.succeeded` é criado; ou, quando não for possível pagar uma fatura `invoice.payment\_failed` é criado. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Muitas solicitações de API podem fazer com que vários eventos sejam criados. Por exemplo, se você criar uma nova assinatura para um cliente, você receberá uma `customer.subscription.created` e um  `charge.succeeded` evento.

## Relacionadas:

* [Conexão [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
