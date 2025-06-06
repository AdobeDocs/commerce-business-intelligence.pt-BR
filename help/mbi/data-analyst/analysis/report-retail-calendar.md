---
title: Relatórios sobre um calendário de varejo
description: Saiba como configurar a estrutura para usar um calendário de varejo 4-5-4 na sua conta  [!DNL Commerce Intelligence] .
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Relatórios de um Calendário de varejo

Este tópico demonstra como configurar a estrutura para usar um [4-5-4 calendário de varejo](https://nrf.com/resources/4-5-4-calendar) em sua conta do [!DNL Adobe Commerce Intelligence]. O construtor de relatórios visuais oferece intervalos de tempo, intervalos e configurações independentes incrivelmente flexíveis. No entanto, todas essas configurações funcionam com o calendário mensal tradicional em vigor.

Como muitos clientes alteram seu calendário para usar datas de varejo ou contábeis, as etapas abaixo ilustram como trabalhar com seus dados e criar relatórios usando datas de varejo. Embora as instruções abaixo façam referência ao calendário 4-5-4 Varejo, você pode alterá-lo para qualquer calendário específico que sua equipe use, seja financeiro ou apenas um intervalo de tempo personalizado.

Antes de começar, você deve revisar [o Carregador de Arquivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) e verificar se alongou o arquivo `.csv`. Isso garante que as datas cubram todos os seus dados históricos e insiram as datas no futuro.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Você pode [baixar](../../assets/454-calendar.csv) uma versão `.csv` do calendário de varejo 4-5-4 para os anos de 2014 a 2017. Talvez seja necessário ajustar esse arquivo de acordo com seu calendário de varejo interno e estender o intervalo de datas para oferecer suporte ao seu histórico e período atual. Depois de baixar o arquivo, use o Carregador de Arquivos para criar uma tabela de Calendário de Varejo na Data Warehouse [!DNL Commerce Intelligence]. Se você estiver usando uma versão inalterada do calendário de varejo 4-5-4, verifique se a estrutura e os tipos de dados dos campos nessa tabela correspondem ao seguinte:

| Nome da coluna | Tipo de dados da coluna | Chave primária |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Até 255 Caracteres) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colunas para criar

* tabela **sales\_order**
   * `INPUT` `created\_at` (aaaa-mm-dd 00:00:00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* Tabela de carregamento de arquivos do **Calendário de varejo**
   * **Data atual**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * &#x200B;

        [!UICONTROL Tipo de dados]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >A função `now()` acima é específica do PostgreSQL. Embora a maioria dos data warehouses [!DNL Commerce Intelligence] esteja hospedada no PostgreSQL, alguns podem estar hospedados no Redshift. Se o cálculo acima retornar um erro, talvez seja necessário usar a função Redshift `getdate()` em vez de `now()`.

   * **Ano de varejo atual** (Deve ser criado pelo analista de suporte)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * &#x200B;

        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluído no ano de varejo atual? (Sim/Não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;

        [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluído no ano de varejo anterior? (Sim/Não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;

        [!UICONTROL Tipo de dados]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* tabela **sales\_order**
   * **Criado\_às (ano de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Year Retail`
   * **Criado\_às (semana de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] created\_at (aaaa-mm-dd 00:00:00
         * [!UICONTROL One]: Calendário de Varejo.Data Varejo
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Week Retail`
   * **Criado\_às (mês de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Month Number Retail`
   * **Incluir no ano de varejo anterior? (Sim/Não)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Varejo `Calendar.Date Retail`
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Incluir no ano de varejo atual? (Sim/Não)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Varejo `Calendar.Date Retail`
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Métricas

Observação: nenhuma métrica nova é necessária para essa análise. No entanto, certifique-se de [adicionar as novas colunas que você criou na tabela sales\_order como dimensões](../data-warehouse-mgr/manage-data-dimensions-metrics.md) para todas as métricas na tabela sales\_order antes de continuar com os relatórios.

## Relatórios

* **Pedidos semanais - calendário de varejo (YoY)**
   * Métrica `A`: `2017`
      * [!UICONTROL Metric]: Número de ordens
      * [!UICONTROL Filter]:
         * Criado\_em (Ano de varejo) = 2017
   * Métrica `B`: `2016`
      * [!UICONTROL Metric]: Número de ordens
      * [!UICONTROL Filter]:
         * Criado\_em (Ano de varejo) = 2016
   * Métrica `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail week)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`
      * Desligar `multiple Y-axes`

* **Visão geral do calendário de varejo (ano de varejo atual por mês)**
   * Métrica `A`: `Revenue`
      * &#x200B;

        [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`

* **Visão geral do calendário de varejo (ano de varejo anterior por mês)**
   * Métrica `A`: `Revenue`
      * &#x200B;

        [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: Número de ordens
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`

## Próximas etapas

As informações acima descrevem como configurar um calendário de varejo para ser compatível com qualquer métrica criada na tabela `sales\_order` (como `Revenue` ou `Orders`). Também é possível estender essa opção para oferecer suporte ao calendário de varejo para métricas criadas em qualquer tabela. O único requisito é que essa tabela tenha um campo de data e hora válido que possa ser usado para unir à tabela Calendário de Varejo.

Por exemplo, para exibir as métricas no nível do cliente em um calendário de varejo 4-5-4, crie um cálculo de `Same Table` na tabela `customer\_entity`, semelhante ao `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descrito acima. Você pode usar esta coluna para reproduzir os cálculos `One to Many` JOINED\_COLUMN (como `Created_at (retail year)`) e `Include in previous retail year? (Yes/No)` unindo a tabela `customer\_entity` à tabela `Retail Calendar`.

Não se esqueça de [adicionar todas as novas colunas como dimensões para métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.
