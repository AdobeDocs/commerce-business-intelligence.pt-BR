---
title: Tabelas comuns do Commerce
description: Saiba mais sobre algumas das tabelas mais comuns que  [!DNL Commerce Intelligence]  clientes usam.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Tabelas comuns do Commerce

Quando você conecta uma instância do [!DNL Adobe Commerce] pela primeira vez ao [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), o [!DNL Commerce Intelligence] replica automaticamente dados de algumas tabelas de comércio (geralmente de 4 a 6 tabelas) para configurar o conjunto inicial de painéis e relatórios. Embora isso ofereça um excelente ponto de partida, a maioria das instâncias de armazenamento gera dezenas, ou centenas, de tabelas adicionais que podem fornecer informações críticas sobre o desempenho de sua empresa.

Veja abaixo uma lista de algumas das tabelas mais comuns que [!DNL Commerce Intelligence] clientes usam. Depois de [conectar a instância do Commerce ao Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), você poderá usar o [Gerenciador de Datas Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear campos de dados relevantes.

| Nome da tabela | Descrição |
|---|---|
| `catalog_category_entity` | Cada linha da tabela `catalog_category_entity` descreve uma categoria específica. Com a tabela `catalog_category_entity_varchar` associada e a tabela de mapeamento `catalog_category_product`, você pode obter informações de categoria para cada produto. |
| `catalog_category_product` | Cada linha na tabela `catalog_category_product` lista uma combinação de um produto e uma categoria. Portanto, um determinado produto pode existir nesta tabela várias vezes com categorias diferentes, e uma determinada categoria pode existir nesta tabela várias vezes associada a produtos diferentes. Esta tabela indexa a tabela `catalog_category_entity` (que contém detalhes de nível de categoria) e a tabela `catalog_product_entity` (que contém detalhes de nível de produto). |
| `catalog_product_entity` | Cada linha na tabela `catalog_product_entity` representa um produto específico. Isso inclui quando esse produto foi criado na sua conta da Commerce e seu SKU. |
| `customer_entity` | Cada linha na tabela [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) representa um usuário registrado em seu site. Detalhes básicos de nível de cliente, como data de registro e endereço de email, estão nesta tabela. |
| `quote` | Cada linha na tabela [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representa um carrinho que foi criado no processo de finalização, independentemente de esse carrinho eventualmente ser convertido em um pedido. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias. |
| `quote_item` | Cada linha na tabela [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representa um item adicionado a um carrinho, independentemente de o carrinho eventualmente ser convertido em um pedido. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias. |
| `sales_order` | Cada linha na tabela [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representa um pedido feito no site. Essa tabela contém informações no nível do pedido, como a data do pedido, o cliente que fez o pedido, o total do pedido e o uso do código de desconto e cupom. |
| `sales_order_address` | Cada linha da tabela `sales_order_address` contém informações sobre remessa e cobrança de um pedido específico. Na tabela `sales_order`, o `billing_address_id` e o `shipping_address_id` de um determinado pedido referem-se a uma linha específica (identificada por `entity_id`) na tabela `sales_order_address`. |
| `sales_order_item` | Cada linha na tabela [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifica um item específico de uma ordem específica. Cada linha contém detalhes como o produto, a quantidade comprada e a ordem à qual determinado item está associado. |

{style="table-layout:auto"}

## Documentação relacionada

[Diagramas de Relacionamento de Entidade](../data-warehouse-mgr/entity-rel-diag.md)
