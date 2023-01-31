---
title: Tabelas de comércio comuns
description: Saiba mais sobre algumas das tabelas mais comuns que [!DNL MBI] Os clientes do usam o .
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Tabelas de comércio comuns

Ao conectar pela primeira vez uma instância do Commerce a [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] replica automaticamente dados de algumas de suas tabelas de comércio (normalmente de 4 a 6 tabelas) para configurar o conjunto inicial de painéis e relatórios. Embora isso ofereça um excelente ponto de partida, a maioria das instâncias de armazenamento gera dezenas ou centenas de tabelas adicionais, o que pode fornecer insight crítico sobre o desempenho de sua empresa.

Abaixo está uma lista de algumas das tabelas mais comuns que [!DNL MBI] Os clientes do usam o . Depois de [conectar sua instância do Commerce ao MBI](../../data-analyst/importing-data/integrations/magento.md), você pode usar o [Gerenciador de Datas Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear campos de dados relevantes.

| Nome da tabela | Descrição |
|---|---|
| `catalog_category_entity` | Cada linha no `catalog_category_entity` a tabela descreve uma categoria específica. Com o `catalog_category_entity_varchar` e a `catalog_category_product` na tabela de mapeamento, é possível obter informações de categoria para cada produto. |
| `catalog_category_product` | Cada linha no `catalog_category_product` tabela lista uma combinação de um produto e uma categoria. Portanto, um determinado produto pode existir nessa tabela várias vezes com categorias diferentes, e uma determinada categoria pode existir nessa tabela várias vezes associada a produtos diferentes. Essa tabela indexa os `catalog_category_entity` tabela (que contém detalhes do nível da categoria) e a variável `catalog_product_entity` tabela (que contém detalhes do nível do produto). |
| `catalog_product_entity` | Cada linha no `catalog_product_entity` representa um produto específico. Isso inclui quando esse produto foi criado em sua conta comercial e em seu SKU. |
| `customer_entity` | Cada linha no [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) tabela representa um usuário registrado em seu site. Detalhes básicos de nível de cliente, como data de registro e endereço de email, estão nessa tabela. |
| `quote` | Cada linha no [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representa um carrinho criado no processo de finalização, seja esse carrinho convertido ou não em um pedido. Devido ao tamanho potencial desta tabela, recomendamos que você exclua registros periodicamente se determinados critérios forem atendidos, como se houvesse algum carrinho não convertido com mais de 60 dias. |
| `quote_item` | Cada linha no [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representa um item adicionado ao carrinho, seja ele convertido ou não em um pedido. Devido ao tamanho potencial desta tabela, recomendamos que você exclua registros periodicamente se determinados critérios forem atendidos, como se houvesse algum carrinho não convertido com mais de 60 dias. |
| `sales_order` | Cada linha no [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representa um pedido colocado em seu site. Esta tabela contém informações no nível do pedido, como a data do pedido, o cliente que fez o pedido, o total do pedido e o uso do código de desconto e cupom. |
| `sales_order_address` | Cada linha no `sales_order_address` A tabela contém informações de envio e faturamento de uma ordem específica. No `sales_order` tabela, a `billing_address_id` e `shipping_address_id` para uma determinada ordem, consulte uma linha específica (identificada por `entity_id`) na `sales_order_address` tabela. |
| `sales_order_item` | Cada linha no [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) tabela identifica um item específico de uma ordem específica. Cada linha contém detalhes como o produto, a quantidade comprada e o pedido ao qual o determinado item está associado. |

{style=&quot;table-layout:auto&quot;}

## Documentação relacionada

[[!DNL Magento] Diagramas de Relação de Entidade](../data-warehouse-mgr/entity-rel-diag.md)
