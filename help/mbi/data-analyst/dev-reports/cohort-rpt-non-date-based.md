---
title: Report Builder de coorte para coortes não baseadas em data
description: Saiba como agrupar usuários por uma atividade ou atributo semelhante.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# `Cohort Report Builder for Non-Date-Based Cohorts`

Nosso [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) O tem sido excelente em ajudar comerciantes a estudar como diferentes subconjuntos de usuários se comportam ao longo do tempo. No passado, o `Cohort Report Builder` foi otimizada principalmente para agrupar usuários por um `cohort date` (por exemplo, o conjunto de todos os clientes que fizeram sua primeira compra em um determinado mês). O `Non-Date Based Cohort` O recurso agora oferece o poder de agrupar usuários por uma atividade ou atributo semelhante. Consulte alguns casos de uso para esse recurso.

## Casos de uso

Esta não é uma lista abrangente, mas aqui estão algumas análises potenciais que podem ser realizadas com esse recurso:

* Análise das receitas dos clientes adquiridas com [!DNL Google] versus [!DNL Facebook]
* Analisando clientes cuja primeira compra foi feita nos EUA em comparação ao Canadá
* Análise do comportamento dos clientes adquiridos em várias campanhas de anúncios

## Como criar sua análise

1. Clique em **[!UICONTROL Report Builder]** na guia esquerda ou **[!UICONTROL Add Report** > **Create Report]** em qualquer painel.

1. No `Report Builder Selection` , clique em **[!UICONTROL Create Report]** ao lado do `Visual Report Builder` opção.

### Adicionar uma métrica

Agora que estamos no `Report Builder`, adicionamos a métrica na qual queremos executar a análise (por exemplo: `Revenue` ou `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] não são compatíveis com a `Cohort Report Builder`. Nosso objetivo para este exemplo é observar a receita ao longo do tempo para clientes de primeiro pedido que foram adquiridos por meio de diferentes fontes de DG.

### Alternar `Metric View` para `Cohort`

![Alterar a exibição de métrica de 1 para a coorte](../../assets/1-toggle-metric-view-to-cohort.png)

Isso abre uma nova janela onde podemos configurar os detalhes do Relatório de coorte.

São necessárias cinco especificações para criar um relatório de coorte:

1. Como agrupar os coortes
1. Seleção de coortes
1. Carimbo de data e hora da ação
1. Intervalo de tempo da primeira ação da coorte
1. Intervalo de tempo após ocorrência de coorte

![grupos de coorte](../../assets/2-cohort-groups.png){: width=&quot;200&quot; height=&quot;224&quot;}

![intervalo de tempo da primeira ação da coorte](../../assets/3-cohort-first-action-time-range.png){: width=&quot;400&quot; height=&quot;554&quot;}

#### 1. Agrupamento `cohorts`

`Cohorts` são agrupadas por uma característica de comportamento, neste exemplo `Customer's first order GA source`. Observe que as opções disponíveis aqui são colunas já designadas como `groupable` para a métrica.

#### 2. Seleção de coortes

Você tem a opção de mostrar todos os resultados para determinada característica. Como isso pode resultar em um grande número de `cohorts`, você pode selecionar a variável `cohorts` (que corresponderá aos vários valores disponíveis para `Customer's first order GA source`) que você precisa.

![grupos de coorte](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

Isso permitirá escolher uma coluna baseada em data diferente da coluna em que a métrica é criada. Abaixo, observamos a seleção do intervalo de tempo que se aplica a um dado `action timestamp`.

#### 4. `Cohort first action time range`

Aqui é onde você selecionará o intervalo de datas que contém a variável `cohorts action timestamp` (assim, clientes que tiveram o primeiro pedido de novembro de 2017 a outubro de 2018). Pode ser um intervalo de datas móvel ou fixo.

#### 5. `Time range after cohort occurrence`

Deseja ver o `cohorts` ao longo do tempo por mês, semana ou ano? Aqui é onde você fará essas seleções. Abaixo dessa seção, você selecionará a variável `time range` após a `cohort action timestamp` ocorreu. Por exemplo, isso mostrará doze meses de dados para os clientes que fizeram o primeiro pedido durante o intervalo de tempo de ação.

![intervalo de tempo da primeira ação da coorte](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

### Outras observações

* [!UICONTROL Filters]: aplicadas às suas métricas permanecerão intactas ao alternar entre `Standard` e `Cohort` exibições
* Consulte [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
