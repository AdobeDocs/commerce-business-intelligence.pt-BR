---
title: Recenticidade, frequência, análise monetária (RFM)
description: Saiba como configurar um painel que permita segmentar os clientes de acordo com sua recenticidade, frequência e classificação monetária.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Análise RFM

Este tópico demonstra como configurar um painel que permite segmentar os clientes de acordo com sua recenticidade, frequência e classificação monetária. A análise RFM é uma técnica de marketing que considera os comportamentos do cliente para ajudar você a determinar a segmentação para alcance geral. São três os aspectos em causa:

1. Recenticidade na recente compra de um cliente em sua loja
1. Frequência na frequência com que eles compram de você
1. Valor monetário em quanto o cliente gasta

![Painel de análise RFM mostrando segmentos de recenticidade, frequência e valor monetário](../../assets/blobid0.png)

A análise RFM só poderá ser configurada se você tiver o plano Pro [!DNL Adobe Commerce Intelligence] na nova arquitetura (por exemplo, se você tiver a opção `Data Warehouse Views` no menu `Manage Data`). Essas colunas podem ser criadas na página **[!DNL Manage Data > Data Warehouse]**. As instruções detalhadas são fornecidas abaixo.

## Introdução

Primeiro, é necessário carregar um arquivo contendo apenas uma chave primária com o valor um. Isso permite a criação de algumas colunas calculadas necessárias para a análise.

Você pode usar este [artigo](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar seu arquivo.

## Colunas calculadas

Uma outra distinção é feita se sua empresa permite pedidos de hóspedes. Em caso afirmativo, você pode ignorar todas as etapas da tabela `customer_entity`. Se os pedidos de convidado não forem permitidos, ignore todas as etapas da tabela `sales_flat_order`.

Colunas para criar

* Tabela **`Sales_flat_order/customer_entity`**
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Selecionado [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* &#x200B;
      Segundos desde a última data de pedido do cliente
  * [!UICONTROL Column type]: -     &quot;Mesma tabela > Idade
* Selecionado [!UICONTROL column]: `Customer's last order date`

* (entrada) Referência de contagem
* [!UICONTROL Column type]: `Same table > Calculation`
* &#x200B;
  [!UICONTROL Entradas]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* Tabela **Referência de contagem** (este é o arquivo que você carregou com o número &quot;1&quot;)
* Número de clientes
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` OU `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Selecionado [!UICONTROL column]: `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* Tabela **Customer_entity**
* Número de clientes
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) referência > Concentração de clientes. `Primary Key`
* Selecionado [!UICONTROL column]: `Number of customers`

* (entrada) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Classificação por receita vitalícia do cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* Pontuação monetária do cliente (por percentis)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* (entrada) Classificação por número de ordens vitalícias do cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Classificação por número de ordens vitalícias do cliente
* &#x200B;
  [!UICONTROL Tipo de coluna]: – "Mesma tabela > Cálculo"
* [!UICONTROL Inputs]: - **(entrada) Classificação por tempo de vida do cliente número de pedidos**, **Número de clientes**
* [!UICONTROL Calculation]: - **caso quando A é nulo, então nulo else (B-(A-1)) end**
* [!UICONTROL Datatype]: - Inteiro

* Pontuação de frequência do cliente (por percentis)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* Classificação por segundos desde a última data de pedido do cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Pontuação de recenticidade do cliente (por percentis)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* Pontuação de recenticidade do cliente (por percentis)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* &#x200B;
  [!UICONTROL Tipo de dados]: String

* Tabela **Referência de contagem**
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Selecionado [!UICONTROL column]: `sales_flat_order.customer_email` OU `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Não É Igual A 000

* Tabela **Customer_entity**
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Selecionado [!UICONTROL column]: - `Number of customers`

* Pontuação de recenticidade do cliente `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: - `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* (entrada) Classificação por pontuação RFM geral do cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Não É Igual A 000

* Classificação por pontuação RFM geral do cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

* Grupo RFM do cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* &#x200B;
  [!UICONTROL Tipo de dados]: `Integer`

>[!NOTE]
>
>Os percentis usados são até mesmo divisões de clientes (por exemplo, intervalos de 20% para retornar de 1 a 5). Se você tiver uma maneira personalizada de ponderar isso, informe ao analista quando enviar o ticket.

## Métricas

Nenhuma métrica nova!

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Clientes por agrupamento RFM**
* Métrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Ocultar gráfico
* [!UICONTROL Group by]: `Customer's RFM group`
* &#x200B;
  [!UICONTROL Agrupar por]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Clientes com pontuação de cinco recenticidade**
* Métrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* Ocultar gráfico
* &#x200B;
  [!UICONTROL Agrupar por]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Clientes com uma pontuação de recenticidade**
* Métrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* Ocultar gráfico
* &#x200B;
  [!UICONTROL Agrupar por]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode se parecer com o painel de amostra acima, mas as três tabelas geradas são apenas exemplos dos tipos de segmentação de clientes que você pode executar.
