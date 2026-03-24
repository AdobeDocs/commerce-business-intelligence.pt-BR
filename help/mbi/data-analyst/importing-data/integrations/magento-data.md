---
title: Dados esperados do Commerce
description: Explore as principais tabelas de dados que os usuários do Commerce importam para o Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 239
ht-degree: 0%

---

# Dados [!DNL Adobe Commerce] esperados

Depois de [conectar sua [!DNL Adobe Commerce] loja](../../../data-analyst/importing-data/integrations/magento.md), você poderá usar o Data Warehouse Manager para rastrear facilmente campos de dados relevantes do banco de dados do Commerce para análise.

Este tópico explora as principais tabelas de dados que os usuários do Commerce importam para o [!DNL Commerce Intelligence].

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Customers` | O `customer\_entity` e as tabelas relacionadas descrevem as informações associadas a cada *cliente registrado* no banco de dados, como endereço de email e data de registro. Com essas informações, você pode começar a segmentar por atributos e coortes no nível do cliente. |
| `Orders` | A tabela `sales\_flat\_order` registra todos os pedidos, incluindo o carimbo de data e hora `created\_at` em que o pedido foi feito e o campo `base\_grand\_total` que soma a receita. Esses campos são a base para suas métricas no nível do pedido. Se o pedido foi feito por um *cliente registrado*, o campo `customer\_id` será vinculado de volta à tabela `customer\_entity` para permitir a análise do comportamento de compra do cliente. |
| `Order items` | A tabela `sales\_flat\_order\_item` registra cada item pertencente a um pedido. Isso inclui os campos `price` e `qty\_ordered`, e o campo `order\_id` que se conecta à tabela `sales\_flat\_order`. Esta tabela é a base de métricas como `Item sold` e permite segmentar por `product` e `product type`. |
| `Products` | A tabela `catalog\_product\_entity` armazena informações sobre atributos no nível do produto, como categoria, tamanho e cor. |
| `Categories` | Seus produtos pertencem a um ou vários `product categories` diferentes, dependendo de como sua build do Commerce está configurada. A tabela `catalog\_category\_entity` armazena a hierarquia dessas categorias (Vestuário > Tops > T-Shirts, por exemplo), e a tabela `catalog\_category\_product` registra as conexões entre seus produtos e essas categorias. |

{style="table-layout:auto"}

## Relacionados

* [Conectando [!DNL Adobe Commerce]](../integrations/magento.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
