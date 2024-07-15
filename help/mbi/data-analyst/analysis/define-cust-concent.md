---
title: Definir concentração do cliente
description: Saiba como configurar um painel que ajuda a medir como a receita total é distribuída entre a base de clientes.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Concentração de clientes

Este tópico demonstra como configurar um painel que ajuda a medir como a receita total é distribuída entre a base de clientes. Entenda qual porcentagem dos clientes contribui com que porcentagem da receita e crie listas segmentadas para comercializar melhor e manter seus clientes que contribuem com destaque.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Primeiro, é necessário carregar um arquivo contendo apenas uma chave primária com o valor um. Isso permite a criação de algumas colunas calculadas necessárias para a análise.

Você pode usar o [carregador de arquivos](../importing-data/connecting-data/using-file-uploader.md) e a imagem abaixo para formatar seu arquivo.

## Colunas calculadas

Se você estiver na arquitetura original (por exemplo, se não tiver a opção `Data Warehouse Views` no menu `Manage Data`), entre em contato com a equipe de suporte para criar as colunas abaixo. Na nova arquitetura, essas colunas podem ser criadas na página `Manage Data > Data Warehouse`. As instruções detalhadas são fornecidas abaixo.

Uma outra distinção é feita se sua empresa permite pedidos de hóspedes. Em caso afirmativo, você pode ignorar todas as etapas da tabela `customer_entity`. Se os pedidos de convidado não forem permitidos, ignore todas as etapas da tabela `sales_flat_order`.

Colunas para criar

* Tabela `Sales_flat_order/customer_entity`
* (entrada) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **caso quando A é nulo e depois nulo senão 1 fim**
* [!UICONTROL Datatype]: - `Integer`

* Tabela `Customer concentration` (este é o arquivo carregado com o número `1`)
* Número de clientes
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Coluna selecionada - `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* Tabela `customer_entity`
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
* [!UICONTROL Calculation]: - **caso quando A é nulo e depois nulo else (A/B)* 100 end **
* [!UICONTROL Datatype]: - `Decimal`

* Tabela `Sales_flat_order`
* Número de clientes
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Caminho - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Coluna selecionada - `Number of customers`

* (entrada) Classificação por receita vitalícia do cliente
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietário do evento - `Number of customers`
* Classificação do Evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentil de receita do cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso quando A é nulo e depois nulo else (A/B)* 100 end **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>Os percentis usados são até mesmo divisões de clientes, representando o Xth percentil da base de clientes. Cada cliente está associado a um número inteiro de 1 a 100, que pode ser considerado como sua receita vitalícia *rank*. Por exemplo, se o percentil de receita do cliente para um cliente específico for **5**, este cliente estará no ***quinto percentil*** de todos os clientes em termos de receita vitalícia.

## Métricas

* **Valor total de vida útil do cliente**
* Na tabela `customer_entity`
* Esta métrica executa uma **Soma**
* Na coluna `Customer's lifetime revenue`
* Ordenado pelo carimbo de data/hora `Customer's first order date`

## Relatórios

* **Concentração de clientes**
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

* **10% de concentração mais alta**
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

Se você tiver dúvidas ao criar esta análise, ou se quiser simplesmente envolver a equipe de Serviços Profissionais, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
