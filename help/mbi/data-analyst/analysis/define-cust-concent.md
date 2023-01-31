---
title: Definir concentração do cliente
description: Saiba como configurar um painel que ajudará a medir como a receita total é distribuída entre a base de clientes.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Concentração do cliente

Neste artigo, demonstramos como configurar um painel que ajudará você a medir como a receita total é distribuída entre a base de clientes. Entenda qual porcentagem de clientes contribui com qual porcentagem da receita e crie listas segmentadas para o melhor mercado e retenha seus clientes que mais contribuem.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Primeiro, será necessário carregar um arquivo contendo apenas uma chave primária com o valor de um. Isso permitirá a criação de algumas colunas calculadas necessárias para a análise.

Você pode aproveitar [o carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) bem como a imagem abaixo para formatar o arquivo.

## Colunas calculadas

Se você estiver na arquitetura original (por exemplo, se não tiver a variável `Data Warehouse Views` sob a `Manage Data` ), entre em contato com a equipe de suporte para criar as colunas abaixo. Na nova arquitetura, essas colunas podem ser criadas no `Manage Data > Data Warehouse` página. Abaixo são fornecidas instruções detalhadas.

Outra distinção é feita se sua empresa permite pedidos de convidado. Nesse caso, você pode ignorar todas as etapas da variável `customer_entity` tabela. Se os pedidos de convidado não forem permitidos, ignore todas as etapas para a variável `sales_flat_order` tabela.

Colunas a serem criadas

* `Sales_flat_order/customer_entity` tabela
* (entrada) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **caso em que A é nulo, então null else 1 end**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` tabela (este é o arquivo que você acabou de carregar com o número `1`)
* Número de clientes
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Coluna selecionada - `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* `customer_entity` tabela
* Número de clientes
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Caminho - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Coluna selecionada - `Number of customers`

* (entrada) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietário do evento - `Number of customers`
* Classificação do evento - `Customer's lifetime revenue`

* Percentil de receita do cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso em que A é nulo, depois null else (A/B)* 100 final **
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` tabela
* Número de clientes
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Coluna selecionada - `Number of customers`

* (entrada) Classificação por receita vitalícia do cliente
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietário do evento - `Number of customers`
* Classificação do evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentil de receita do cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso em que A é nulo, depois null else (A/B)* 100 final **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>Os percentis usados são até mesmo divisões de clientes, representando o Xth percentil da base de clientes. Cada cliente será associado a um número inteiro de 1 a 100, que pode ser considerado como sua receita vitalícia *classificação*. Por exemplo, se o percentil de receita do Cliente para um cliente específico for **5**, este cliente está no ***5º percentil*** de todos os clientes em termos de receita vitalícia.

## Métricas

* **Valor vitalício total do cliente**
* No `customer_entity` tabela
* Essa métrica executa um **Soma**
* No `Customer's lifetime revenue` column
* Solicitado pela `Customer's first order date` timestamp

## Relatórios

* **Concentração do cliente**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL Agrupar por]: `Independent`
* Métrica `A`: `Total customer lifetime revenue by percentile`
* Métrica `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Mostrar parte superior/inferior: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **Concentração superior a 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Métrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
   [!UICONTROL Agrupar por]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentração inferior de 50% com apenas uma compra**

* Métrica `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
   [!UICONTROL Agrupar por]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentração inferior a 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Métrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
   [!UICONTROL Agrupar por]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com o painel de amostra acima.

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](../../guide-overview.md).
