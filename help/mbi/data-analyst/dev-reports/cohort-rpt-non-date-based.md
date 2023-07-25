---
title: Report Builder de coorte para coortes não baseadas em data
description: Saiba como agrupar usuários por uma atividade ou atributo semelhante.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] para coortes não baseados em data

A variável [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) O é excelente para ajudar os comerciantes a estudar como diferentes subconjuntos de usuários se comportam ao longo do tempo. No passado, a `Cohort Report Builder` foi otimizado para agrupar usuários por uma `cohort date` (por exemplo, o conjunto de todos os clientes que fizeram sua primeira compra em um determinado mês). A variável `Non-Date Based Cohort` O recurso agora permite agrupar usuários por uma atividade ou atributo semelhante. Veja alguns casos de uso para esse recurso.

## Casos de uso

Esta não é uma lista abrangente, mas aqui estão algumas análises potenciais que podem ser realizadas com esse recurso.

* Examinar a receita dos clientes adquiridos do [!DNL Google] versus [!DNL Facebook]
* Análise de clientes cuja primeira compra foi feita nos EUA e no Canadá
* Observar o comportamento dos clientes adquiridos de várias campanhas de publicidade

## Como criar sua análise

1. Clique em **[!UICONTROL Report Builder]** na guia esquerda ou **[!UICONTROL Add Report** > **Create Report]** em qualquer painel.

1. No `Report Builder Selection` clique em **[!UICONTROL Create Report]** ao lado da `Visual Report Builder` opção.

### Adição de uma métrica

Agora que você está no `Report Builder`, você adiciona a métrica em que deseja executar a análise (exemplo: `Revenue` ou `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] as métricas não são compatíveis com o `Cohort Report Builder`. O objetivo deste exemplo é observar a receita ao longo do tempo de clientes de primeira ordem que foram adquiridos por meio de diferentes [!DNL Google Analytics] fontes.

### Alternar `Metric View` para `Cohort`

![1-alternar exibição de métrica para coorte](../../assets/1-toggle-metric-view-to-cohort.png)

Isso abre uma nova janela, onde é possível configurar os detalhes do Relatório de coorte.

Cinco especificações são necessárias para criar um relatório de coorte:

1. Como agrupar os coortes
1. Seleção de coortes
1. Carimbo de data e hora da ação
1. Intervalo de tempo da primeira ação do coorte
1. Intervalo de tempo após a ocorrência da coorte

![grupos de coorte](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### 1. Agrupamento `cohorts`

`Cohorts` são agrupados por uma característica de comportamento, neste exemplo `Customer's first order GA source`. As opções disponíveis aqui são colunas que já estão designadas como `groupable` para a métrica.

#### 2. Seleção de coortes

É possível mostrar todos os resultados para a característica fornecida. Como isso pode resultar em muitos `cohorts`, é possível selecionar as opções específicas `cohorts` (que corresponde aos vários valores disponíveis para `Customer's first order GA source`) de que você precisa.

![grupos de coorte](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

Isso permite escolher uma coluna baseada em data diferente da coluna na qual a métrica é criada. Abaixo, você procura selecionar o intervalo de tempo que se aplica ao `action timestamp`.

#### 4. `Cohort first action time range`

Aqui é onde você seleciona o intervalo de datas que contém a variável `cohorts action timestamp` (então, clientes que tiveram o primeiro pedido de novembro de 2017 a outubro de 2018). Pode ser um intervalo de datas móvel ou fixo.

#### 5. `Time range after cohort occurrence`

Deseja ver o `cohorts` ao longo do tempo por mês, semana ou ano? Aqui é onde você faz essas seleções. Abaixo dessa seção, você selecionará o `time range` depois que a variável `cohort action timestamp` ocorreu. Por exemplo, isso mostra 12 meses de dados para os clientes que fizeram o primeiro pedido durante o intervalo de tempo da ação.

![coorte-primeira-ação-intervalo de tempo](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] aplicadas às suas métricas permanecem intactas ao alternar entre `Standard` e `Cohort` exibições.

### Relacionados

Consulte [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
