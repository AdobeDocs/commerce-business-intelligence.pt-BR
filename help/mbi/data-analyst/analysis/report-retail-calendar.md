---
title: Relatório de um calendário de retalho
description: Saiba como configurar a estrutura para usar um calendário de varejo 4-5-4 em seu [!DNL MBI] conta.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Gerar relatórios em um calendário de varejo

Neste artigo, demonstramos como configurar a estrutura para usar um [Calendário de varejo 4-5-4](https://nrf.com/resources/4-5-4-calendar) em seu [!DNL MBI] conta. O Construtor de relatórios visual fornece intervalos de tempo, intervalos e configurações independentes incrivelmente flexíveis. Nossa equipe também pode ajudá-lo a alterar o dia de início da semana para se alinhar às suas preferências comerciais. No entanto, todas essas configurações funcionam com o calendário mensal tradicional em vigor.

Como muitos de nossos clientes alteram seu calendário para usar datas de varejo ou de contabilidade, as etapas abaixo ilustram como trabalhar com seus dados e criar relatórios usando datas de varejo. Embora as instruções abaixo façam referência ao calendário fiscal 4-5-4, você pode alterá-las para qualquer calendário específico que sua equipe usa, seja financeiro ou apenas personalizado.

Antes de começar, você quer se familiarizar com [o Carregador de arquivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) e certifique-se de que tenha alongado a `.csv` para que as datas cubram todos os seus dados históricos, bem como as datas sejam enviadas para o futuro.

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introdução

Você pode [download](../../assets/454-calendar.csv) a `.csv` versão do calendário fiscal 4-5-4 para os anos de retalho de 2014 até 2017. Observe que talvez seja necessário ajustar esse arquivo de acordo com seu calendário de varejo interno, bem como estender o intervalo de datas para suportar seu período histórico e atual. Após baixar o arquivo, use o Carregador de arquivo para criar uma tabela de Calendário de varejo em [!DNL MBI] data warehouse. Se estiver usando uma versão inalterada do calendário de varejo 4-5-4, verifique se a estrutura e os tipos de dados dos campos nesta tabela correspondem ao seguinte:

| Nome da coluna | Tipo de dados da coluna | Chave primária |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Até 255 caracteres) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style=&quot;table-layout:auto&quot;}

## Colunas a serem criadas

* **sales\_order** tabela
   * `INPUT` `created\_at` (aaaa-mm-dd 00:00:00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendário fiscal** tabela de upload de arquivo
   * **Data atual**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL Tipo de dados]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >O `now()` A função acima é específica do PostgreSQL. Embora a maioria [!DNL MBI] data warehouses são hospedados no PostgreSQL, alguns podem ser hospedados no Redshift. Se o cálculo acima retornar um erro, talvez seja necessário usar a função Redshift `getdate()` em vez de `now()`.
   * **Ano de varejo atual** (Deve ser criado pelo analista de suporte)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluído no ano de varejo atual? (Sim/Não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo de dados]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluído no ano fiscal anterior? (Sim/Não)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo de dados]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** tabela
   * **Criado\_at (ano de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Year Retail`
   * **Criado\_at (semana de varejo)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Caminho -
         * [!UICONTROL Many]:sales\_order.\[INPUT\] criado\_at (aaaa-mm-dd 00:00:00
         * [!UICONTROL One]:Calendário de varejo.Retenção de data
      * Selecione um [!UICONTROL table]: `Retail Calendar`
      * Selecione um [!UICONTROL column]: `Week Retail`
   * **Criado\_at (mês de varejo)**
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

Observação: Nenhuma métrica nova é necessária para essa análise. No entanto, certifique-se de [adicione as novas colunas que você criou na tabela sales\_order como dimensões](../data-warehouse-mgr/manage-data-dimensions-metrics.md) para todas as métricas na tabela sales\_order antes de continuar com os relatórios.

## Relatórios

* **Pedidos semanais - calendário de varejo (YoY)**
   * Métrica `A`: `2017`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Criado\_at (Ano de varejo) = 2017
   * Métrica `B`: `2016`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Criado\_at (ano de varejo) = 2016
   * Métrica `C`: `2015`
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
      * Desligar `multiple Y-axes`

* **Visão geral do calendário de varejo (ano de varejo atual por mês)**
   * Métrica `A`: `Revenue`
      * 
         [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
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
   * Métrica `A`: `Revenue`
      * 
         [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
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

## Próximas etapas

A descrição acima descreve como configurar um calendário de varejo para ser compatível com qualquer métrica criada no `sales\_order` tabela (por exemplo,`Revenue` e `Orders`), mas você também pode estender isso para suportar o calendário de varejo para métricas criadas em qualquer tabela. O único requisito é que esta tabela tenha um campo de data e hora válido que possa ser usado para unir à tabela Calendário de varejo.

Assim, por exemplo, para exibir métricas no nível do cliente em um calendário de varejo 4-5-4, crie um novo `Same Table` no `customer\_entity` tabela, semelhante a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descrito acima. É possível usar essa coluna para reproduzir todas as variáveis `One to Many` JOINED\_COLUMN (como `Created_at (retail year)` e `Include in previous retail year? (Yes/No)` unindo-se ao `customer\_entity` à tabela `Retail Calendar` tabela.

Não se esqueça de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.
