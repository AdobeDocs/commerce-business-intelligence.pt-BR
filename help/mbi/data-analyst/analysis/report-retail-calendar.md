---
title: Relatórios em um calendário de varejo
description: Aprenda a configurar a estrutura para usar um calendário de varejo 4-5-4 em seu  [!DNL Commerce Intelligence]  conta.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Relatórios em um calendário de varejo

Este tópico demonstra como configurar a estrutura para usar um [ calendário ](https://nrf.com/resources/4-5-4-calendar) de varejo 4-5-4 no [!DNL Adobe Commerce Intelligence] conta. O construtor de relatórios Visual oferece intervalos de tempo, intervalos e configurações independentes de incrivelmente flexível. No entanto, todas essas configurações funcionam com o calendário mensal tradicional no local.

Como muitos clientes alteram o calendário para usar datas de varejo ou de contabilidade, as etapas abaixo ilustram como trabalhar com seus dados e criar relatórios usando datas de varejo. Embora as instruções abaixo façam referência ao calendário de varejo 4-5-4, você pode alterá-los para qualquer calendário específico que seu equipe usa, sejam eles financeiros ou apenas uma intervalo de tempo personalizada.

Antes de começar, você deve analisar [ o upload ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) do arquivo e garantir que o `.csv` arquivo seja alongado. Isso garante que as datas abranjam todas as suas dados históricos e empurrem as datas para o futuro.

Esta análise contém [ colunas ](../data-warehouse-mgr/adv-calc-columns.md) calculadas avançadas.

## Introdução

Você pode [ baixar ](../../assets/454-calendar.csv) uma `.csv` versão do calendário de varejo 4-5-4 para os anos de varejo de 2014 a 2017. Talvez seja necessário ajustar esse arquivo de acordo com o calendário de varejo interno e estender o intervalo de datas para oferecer suporte aos intervalo de tempo históricos e atuais. Após baixar o arquivo, use o carregador de Arquivo para criar uma tabela de calendário de varejo no [!DNL Commerce Intelligence] data warehouse. Se você estiver usando uma versão inalterada do calendário de varejo 4-5-4, certifique-se de que a estrutura e os tipos de dados dos campos nessa tabela correspondam ao seguinte:

| Nome da coluna | DataType da coluna | Chave primária |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Até 255 caracteres) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colunas para Criar

* **tabela de vendas \ _order**
   * `INPUT``created\_at`(aaaa-mm-dd 00 :00: 00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Tabela de upload de arquivo de calendário** de varejo
   * **Data atual**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [! UICONTROL DataType]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >A função acima é específica do `now()` PostgreSQL. Embora a maioria dos [!DNL Commerce Intelligence] data warehouses esteja hospedada no PostgreSQL, alguns podem ser hospedados no Query no redshift. Se o cálculo acima retornar um erro, talvez seja necessário usar a função `getdate()` Query no redshift em vez de `now()` .
   * **Ano** de varejo atual (deve ser criado pelo analista de suporte)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluído no ano de varejo atual? (Sim/não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [! UICONTROL DataType]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluído no ano de varejo anterior? (Sim/não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [! UICONTROL DataType]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **tabela de vendas \ _order**
   * **Criado \ _at (ano de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho-
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecione a [!UICONTROL table] : `Retail Calendar`
      * Selecione a [!UICONTROL column] : `Year Retail`
   * **Criado \ _at (semana de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho-
         * [!UICONTROL Many]: vendas \ _order.\ [INPUT \] criado \ _at (aaaa-mm-dd 00 :00: 00
         * [!UICONTROL One]: Calendário de varejo. Data comercial
      * Selecione a [!UICONTROL table] : `Retail Calendar`
      * Selecione a [!UICONTROL column] : `Week Retail`
   * **Criado \ _at (mês de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecione a [!UICONTROL table] : `Retail Calendar`
      * Selecione a [!UICONTROL column] : `Month Number Retail`
   * **Incluir no ano de varejo anterior? (Sim/não)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho-
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:Varejo `Calendar.Date Retail`
      * Selecione a [!UICONTROL table] : `Retail Calendar`
      * Selecione a [!UICONTROL column] : `Include in previous retail year? (Yes/No)`
   * **Incluir no ano de varejo atual? (Sim/não)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho-
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:Varejo `Calendar.Date Retail`
      * Selecione a [!UICONTROL table] : `Retail Calendar`
      * Selecione a [!UICONTROL column] : `Include in current retail year? (Yes/No)`

## Métricas

Observação: nenhuma nova métrica é necessária para esta análise. No entanto, certifique-se [ de adicionar as novas colunas que você criou na tabela vendas \ _order como dimensões ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) para todas as métricas na tabela vendas \ _order antes de continuar os relatórios.

## Relatórios

* **Pedidos semanais-calendário de varejo (YoY)**
   * Métrica `A` : `2017`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Criado \ _at (ano de varejo) = 2017
   * Métrica `B` : `2016`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Criado \ _at (ano de varejo) = 2016
   * Métrica `C` : `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * Desativar `multiple Y-axes`

* **Visão geral do calendário de varejo (ano atual de varejo por mês)**
   * Métrica `A` : `Revenue`
      * 
         [! Métrica UICONTROL]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B` : `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C` : `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **Visão geral do calendário de varejo (ano de varejo anterior por mês)**
   * Métrica `A` : `Revenue`
      * 
         [! Métrica UICONTROL]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B` : `Orders`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C` : `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## Próximo etapas

O acima descreve como configurar um calendário de varejo para ser compatível com qualquer métrica criado em sua `sales\_order` tabela ( `Revenue` como ou `Orders` ). Você também pode estender isso para oferecer suporte ao calendário de varejo para métricas criadas em qualquer tabela. O único requisito é que esta tabela tenha um campo data e hora válido que pode ser usado para ingressar na tabela de calendário de varejo.

Por exemplo, para visualização métricas no nível do cliente em um calendário de varejo 4-5-4, crie um `Same Table` cálculo na `customer\_entity` tabela, semelhante ao `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descrito acima. Em seguida, você pode usar essa coluna para reproduzir os `One to Many` cálculos \ _COLUMN associados (curtir `Created_at (retail year)` ) e `Include in previous retail year? (Yes/No)` ingressar na `customer\_entity` tabela `Retail Calendar` .

Não esqueça de [ Adicionar todas as novas colunas como dimensões para métricas ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.
