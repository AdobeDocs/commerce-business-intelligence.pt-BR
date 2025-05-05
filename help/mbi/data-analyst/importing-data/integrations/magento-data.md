---
title: Dados esperados do Commerce
description: Explore as principais tabelas de dados que os usuários do Commerce importam para o Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Dados [!DNL Adobe Commerce] esperados

Depois de [conectar seu [!DNL Adobe Commerce] armazenamento](../../../data-analyst/importing-data/integrations/magento.md), você poderá usar o Gerenciador de Data Warehouse para rastrear facilmente campos de dados relevantes do banco de dados do Commerce para análise.

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
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
