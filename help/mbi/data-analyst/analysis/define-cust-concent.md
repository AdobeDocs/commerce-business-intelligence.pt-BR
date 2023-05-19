---
title: Definir concentração do cliente
description: Saiba como configurar um painel que ajuda a medir como a receita total é distribuída entre a base de clientes.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Concentração de clientes

Este tópico demonstra como configurar um painel que ajuda a medir como a receita total é distribuída entre a base de clientes. Entenda qual porcentagem dos clientes contribui com que porcentagem da receita e crie listas segmentadas para comercializar melhor e manter seus clientes que contribuem com destaque.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Primeiro, é necessário carregar um arquivo contendo apenas uma chave primária com o valor um. Isso permite a criação de algumas colunas calculadas necessárias para a análise.

Você pode usar [o carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar o arquivo.

## Colunas calculadas

Se você estiver na arquitetura original (por exemplo, se não tiver o `Data Warehouse Views` opção no campo `Manage Data` ), você deseja entrar em contato com a equipe de suporte para criar as colunas abaixo. Na nova arquitetura, essas colunas podem ser criadas no `Manage Data > Data Warehouse` página. As instruções detalhadas são fornecidas abaixo.

Uma outra distinção é feita se sua empresa permite pedidos de hóspedes. Em caso afirmativo, você pode ignorar todas as etapas da `customer_entity` tabela. Se as ordens do convidado não forem permitidas, ignore todas as etapas da `sales_flat_order` tabela.

Colunas para criar

* `Sales_flat_order/customer_entity` tabela
* (entrada) `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]: - **caso quando A é nulo, senão nulo 1 fim**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` tabela (este é o arquivo que você carregou com o número `1`)
* Número de clientes
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Coluna selecionada - `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* `customer_entity` tabela
* Número de clientes
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Caminho - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Coluna selecionada - `Number of customers`

* (entrada) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* Proprietário do evento - `Number of customers`
* Classificação do evento - `Customer's lifetime revenue`

* Percentil de receita do cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso quando A é nulo, então nulo else (A/B)* fim de 100 **
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` tabela
* Número de clientes
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Coluna selecionada - `Number of customers`

* (entrada) Classificação por receita vitalícia do cliente
* [!UICONTROL Column type]: – `Same table > Event Number`
* Proprietário do evento - `Number of customers`
* Classificação do evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentil de receita do cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso quando A é nulo, então nulo else (A/B)* fim de 100 **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>Os percentis usados são até mesmo divisões de clientes, representando o Xth percentil da base de clientes. Cada cliente está associado a um número inteiro de 1 a 100, que pode ser considerado sua receita vitalícia *classificação*. Por exemplo, se o percentil de receita do Cliente para um cliente específico for **5**, este cliente está na ***quinto percentil*** de todos os clientes em termos de receita vitalícia.

## Métricas

* **Valor total vitalício do cliente**
* No `customer_entity` tabela
* Essa métrica executa uma **Sum**
* No `Customer's lifetime revenue` coluna
* Ordenado por `Customer's first order date` carimbo de data e hora

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
* Mostrar superior/inferior: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **Concentração superior de 10%**
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

* **Concentração de 50% inferior com apenas uma compra**

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

* **Concentração de 10% inferior**
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

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode se parecer com o painel de amostra acima.

Se você tiver dúvidas ao criar essa análise ou se quiser simplesmente envolver a equipe de serviços profissionais, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
