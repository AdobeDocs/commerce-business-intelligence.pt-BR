---
title: Dados de comércio esperados
description: Explore as principais tabelas de dados que os usuários do Commerce importam para o Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Esperado [!DNL Adobe Commerce] Dados

Depois de ter [conectou o [!DNL Adobe Commerce] loja](../../../data-analyst/importing-data/integrations/magento.md), você pode usar o Gerenciador de Datas Warehouse para rastrear facilmente campos de dados relevantes do banco de dados do Commerce para análise.

Este tópico explora as principais tabelas de dados que os usuários do Commerce importam para o [!DNL Commerce Intelligence].

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Customers` | A variável `customer\_entity` e as tabelas relacionadas descrevem as informações associadas a cada *cliente registrado* no banco de dados, como o endereço de email e a data de registro. Com essas informações, você pode começar a segmentar por atributos e coortes no nível do cliente. |
| `Orders` | A variável `sales\_flat\_order` a tabela registra todos os pedidos, incluindo o `created\_at` carimbo de data e hora em que o pedido foi feito e a `base\_grand\_total` campo que soma a receita. Esses campos são a base para suas métricas no nível do pedido. Se a ordem foi feita por um *cliente registrado*, o `customer\_id` O campo é vinculado de volta à  `customer\_entity` para permitir a análise do comportamento de compra do cliente. |
| `Order items` | A variável `sales\_flat\_order\_item` A tabela registra cada item pertencente a um pedido. Isso inclui a `price` e `qty\_ordered` e a variável `order\_id` campo que se conecta ao `sales\_flat\_order` tabela. Essa tabela é a base de métricas como `Item sold`, e permite segmentar por `product` e `product type`. |
| `Products` | A variável `catalog\_product\_entity` A tabela armazena informações sobre atributos no nível do produto, como categoria, tamanho e cor. |
| `Categories` | Seus produtos pertencem a um ou vários `product categories`, dependendo de como sua build do Commerce está configurada. A variável `catalog\_category\_entity` A tabela armazena a hierarquia dessas categorias (Vestuário > Tops > T-Shirts, por exemplo) e a variável `catalog\_category\_product` A tabela registra as conexões entre seus produtos e essas categorias. |

{style="table-layout:auto"}

## Relacionados

* [Conectando [!DNL Adobe Commerce]](../integrations/magento.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
