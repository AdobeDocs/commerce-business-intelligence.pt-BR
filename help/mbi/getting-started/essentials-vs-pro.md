---
title: Commerce Intelligence Essentials versus Pro
description: Saiba como o Commerce Intelligence Essentials difere do Commerce Intelligence Pro.
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
role: Admin, Developer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/5MTFaBTLbZyjDFtMSG0lISoXV8cbMGjSpDvcQ7Syj3o
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: b6ae8fb1a1a7f30e3d56740986f9366e7d1e7f1a
workflow-type: tm+mt
source-wordcount: 77
ht-degree: 5%

---

# [!DNL Commerce Intelligence Essentials] vs [!DNL Commerce Intelligence Pro]

A tabela a seguir descreve os elementos incluídos com uma conta herdada do `Essentials` em comparação a uma conta atual do Commerce Intelligence. A Adobe não oferece mais `Essentials`.

|   | **`Commerce Intelligence Essentials`** | **`Commerce Intelligence Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | Até 100 | Personalizado |
| `Pre-Defined Dashboards` | 5-6 | Personalizado |
| `New Custom Report Creation` | Sim | Sim |
| `Commerce Tables` | 4-6 | Ilimitado |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | Sim | Sim |
| `Data Warehouse Manager` | Indisponível | Disponível |
| `Email Reports` | Sim | Sim |
| `Cohort Report Builder` | Sim | Sim |
| `Google Analytics Live Integration` | Sim | Ilimitado |
| `3rd Party Integrations` | Indisponível | Disponível |
| `Full API Access` | Não | Sim |
| `Access to CS, AM, or Analysts` | Não | Sim |
| `Professional Services` | Disponível | Disponível |

{style="table-layout:auto"}

>[!NOTE]
>
>O número de tabelas depende do check-out do convidado.

**Tabelas incluídas**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

<!--
## Columns Included in Essentials

Items in _italics_ are calculated fields.

* `sales_order` table
  * `entity_id`
  * `base_grand_total`
  * `customer_id`
  * `status`
  * `customer_email`
  * `store_id`
  * `base_currency_code`
  * `billing_address_id`
  * `shipping_address_id`
  * `base_shipping_amount`
  * `base_tax_amount`
  * `coupon_code`
  * `created_at`
  * `updated_at`
  * `base_subtotal`
  * `customer_group_id`
  * `base_discount_amount`
  * `base_discount_invoiced`
  * `increment_id`
  * `Customer's order number`
  * `Customer's first order date`
  * `Customer's lifetime number of orders`
  * `Is customer's last order?`
  * `Billing address region`
  * `Shipping address country`
  * `Customer's lifetime revenue`
  * `Seconds between customer's first order date and this order`
  * `Seconds since previous order`
  * `Store name`
  * `Customer's lifetime number of coupons`
  * `Customer's order number (previous-current)`
  * `Shipping address region`
  * `Number of items in order`
  * `Billing address city`
  * `Shipping address city`
  * `Customer's group code`
  * `Customer's first order's billing region`
  * `Customer's first order's coupon_code`
  * `Customer's creation date`
  * `Billing address country`

* `sales_order_item` table
  * `item_id`
  * `qty_ordered`
  * `base_price`
  * `name`
  * `order_id`
  * `sku`
  * `product_type`
  * `product_id`
  * `created_at`
  * `updated_at`
  * `parent_item_id`
  * `store_id`
  * `base_discount_amount`
  * `base_discount_invoiced`
  * `Order's coupon_code`
  * `Order item total value (quantity * price)`
  * `Order's increment_id`
  * `Customer's email`
  * `Customer's lifetime number of orders`
  * `Store name`
  * `Customer's order number`
  * `Order's status`
  * `Customer's lifetime revenue`

* `sales_order_address` table
  * `entity_id`
  * `city`
  * `region`
  * `country_id`

* `customer_entity` table
  * `entity_id`
  * `email`
  * `group_id`
  * `created_at`
  * `updated_at`
  * `store_id`
  * `Customer's lifetime revenue`
  * `Customer's lifetime number of coupons`
  * `Customer's first order date`
  * `Customer's lifetime number of orders`
  * `Seconds since customer's first order date`
  * `Customer's first 30 day revenue`
  * `Customer's first order's billing region`
  * `Customer's first order's coupon_code`
  * `Customer's group code`
  * `Store name`

* `customer_group` table
  * `customer_group_id`
  * `customer_group_code`

* `store` table
  * `store_id`
  * `name`
-->
