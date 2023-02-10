---
title: Dados de comércio esperados
description: Explore as principais tabelas de dados que os usuários do Commerce importam para o MBI
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Dados de comércio esperados

Depois de [conectou sua loja do Commerce](../../../data-analyst/importing-data/integrations/magento.md), você pode usar o Gerenciador de Datas Warehouse para rastrear facilmente os campos de dados relevantes do seu banco de dados do Commerce para análise.

Neste artigo, exploramos as principais tabelas de dados que os usuários do Commerce importam para [!DNL MBI].

| **Nome da tabela** | **Descrição** |
|-----|-----|
| `Customers` | O `customer\_entity` e tabelas relacionadas descrevem as informações associadas a cada *cliente registrado* no banco de dados, como o endereço de email e a data de registro. Com essas informações, você pode começar a segmentar por atributos e coortes no nível do cliente. |
| `Orders` | O `sales\_flat\_order` a tabela registra todas as ordens, incluindo a `created\_at` carimbo de data e hora em que o pedido foi feito e a variável `base\_grand\_total` que soma a receita. Esses campos serão a base para suas métricas no nível do pedido. Se o pedido foi feito por um *cliente registrado*, o `customer\_id` voltará ao campo  `customer\_entity` tabela para permitir análise do comportamento de compra do cliente. |
| `Order items` | O `sales\_flat\_order\_item` A tabela registra cada item pertencente a um pedido. Isso inclui a variável `price` e `qty\_ordered` , bem como `order\_id` campo que se conecta à variável `sales\_flat\_order` tabela. Esta tabela é a base para métricas como `Item sold`e permite segmentar por `product` e `product type`. |
| `Products` | O `catalog\_product\_entity` A tabela armazena informações sobre atributos no nível do produto, como categoria, tamanho e cor. |
| `Categories` | Seus produtos pertencerão a um ou vários produtos diferentes `product categories`, dependendo de como a sua build do Commerce está configurada. O `catalog\_category\_entity` A tabela armazena a hierarquia dessas categorias (Apprarel > Tops > T-Shirts, por exemplo) e a variável `catalog\_category\_product` a tabela registra as conexões entre seus produtos e essas categorias. |

{style=&quot;table-layout:auto&quot;}

## Relacionado

* [Conexão [!DNL Adobe Commerce]](../integrations/magento.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
