---
title: Tabelas de comércio comuns
description: Saiba mais sobre algumas das tabelas mais comuns que [!DNL Commerce Intelligence] clientes usam.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Tabelas de comércio comuns

Ao conectar pela primeira vez um [!DNL Adobe Commerce] instância para [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] O replica automaticamente dados de algumas de suas tabelas de comércio (normalmente de 4 a 6 tabelas) para configurar o conjunto inicial de painéis e relatórios. Embora isso ofereça um excelente ponto de partida, a maioria das instâncias de armazenamento gera dezenas, ou centenas, de tabelas adicionais que podem fornecer informações críticas sobre o desempenho de sua empresa.

Abaixo está uma lista de algumas das tabelas mais comuns que [!DNL Commerce Intelligence] clientes usam. Depois que você [conectar sua instância do Commerce ao Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), você pode usar o [Gerenciador de Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear campos de dados relevantes.

| Nome da tabela | Descrição |
|---|---|
| `catalog_category_entity` | Cada linha no `catalog_category_entity` A tabela descreve uma categoria específica. Com o associado `catalog_category_entity_varchar` tabela e o `catalog_category_product` tabela de mapeamento, você pode obter informações de categoria para cada produto. |
| `catalog_category_product` | Cada linha no `catalog_category_product` A tabela lista uma combinação de um produto e uma categoria. Portanto, um determinado produto pode existir nesta tabela várias vezes com categorias diferentes, e uma determinada categoria pode existir nesta tabela várias vezes associada a produtos diferentes. Esta tabela indexa o `catalog_category_entity` tabela (que contém detalhes de nível de categoria) e a variável `catalog_product_entity` (que contém detalhes de nível de produto). |
| `catalog_product_entity` | Cada linha no `catalog_product_entity` A tabela representa um produto específico. Isso inclui quando esse produto foi criado na sua conta do Commerce e seu SKU. |
| `customer_entity` | Cada linha no [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) A tabela representa um usuário registrado em seu site. Detalhes básicos de nível de cliente, como data de registro e endereço de email, estão nesta tabela. |
| `quote` | Cada linha no [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) A tabela representa um carrinho que foi criado no processo de finalização, independentemente de esse carrinho eventualmente ser convertido em um pedido. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias. |
| `quote_item` | Cada linha no [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) A tabela representa um item adicionado a um carrinho, independentemente de o carrinho eventualmente ser convertido em um pedido. Devido ao tamanho potencial dessa tabela, a Adobe recomenda que você exclua periodicamente os registros se determinados critérios forem atendidos, como se houver algum carrinho não convertido com mais de 60 dias. |
| `sales_order` | Cada linha no [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) A tabela representa um pedido feito no site. Essa tabela contém informações no nível do pedido, como a data do pedido, o cliente que fez o pedido, o total do pedido e o uso do código de desconto e cupom. |
| `sales_order_address` | Cada linha no `sales_order_address` A tabela contém informações sobre remessa e faturamento de um pedido específico. No `sales_order` tabela, a variável `billing_address_id` e a variável `shipping_address_id` para uma determinada ordem, consulte uma linha específica (identificada por `entity_id`) no `sales_order_address` tabela. |
| `sales_order_item` | Cada linha no [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) a tabela identifica um item específico de um pedido específico. Cada linha contém detalhes como o produto, a quantidade comprada e a ordem à qual determinado item está associado. |

{style="table-layout:auto"}

## Documentação relacionada

[Diagramas de Relacionamento de Entidade](../data-warehouse-mgr/entity-rel-diag.md)
