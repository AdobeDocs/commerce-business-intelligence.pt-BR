---
title: Criar uma análise qualitativa de coorte
description: Saiba o que é uma coorte qualitativa, por que você pode estar interessado em criar essa análise e como criá-la no Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Criar um `Qualitative Cohort Analysis`

Você sabe como os segmentos de clientes adquiridos pelo [!DNL Google Adwords] aumentam o LTV em comparação aos clientes adquiridos da pesquisa orgânica? Você já pensou em executar uma análise `cohort` em diferentes segmentos de clientes lado a lado no mesmo relatório? Em caso afirmativo, um `qualitative cohort analysis` o ajudará a responder essas perguntas.

Este tópico aborda o que é uma coorte qualitativa, por que você pode estar interessado em criar essa análise e como criá-la em [!DNL Commerce Intelligence].

## O que são `qualitative cohorts`, afinal? {#whatare}

A análise do `Cohort` em geral pode ser definida como a análise de grupos de usuários que compartilham características semelhantes em seus ciclos de vida. Ele permite identificar tendências comportamentais em diferentes grupos de usuários.

Consulte [análise de coorte](https://www.cohortanalysis.com/).

A maioria dos `cohort` analisa em [!DNL Commerce Intelligence] usuários em grupo por uma data comum (por exemplo, o conjunto de todos os clientes que fizeram sua primeira compra em um determinado mês). Um `qualitative cohort` é um pouco diferente: é um grupo de usuários definido por uma característica que não é baseada no tempo. Os exemplos incluem:

* O conjunto de todos os usuários adquiridos de uma campanha publicitária
* O conjunto de todos os usuários cuja primeira compra incluiu um cupom (ou não)
* O conjunto de todos os usuários com determinada idade

## Como isso difere do construtor `cohort` normal? {#different}

O [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) é otimizado para agrupar coortes usando uma característica baseada em tempo. Isso é ótimo para análises com foco em um segmento específico de usuário (por exemplo, todos os usuários que foram adquiridos por meio de uma campanha de pesquisa paga). No `Cohort Analysis Builder`, você pode (1) se concentrar nesse grupo de usuários específico e (2) `cohort` em uma data (como a data da primeira ordem).

Entretanto, se você quiser analisar o comportamento da coorte de vários segmentos de usuários no mesmo relatório de coorte (`paid` pesquisa versus `organic` pesquisa versus tráfego direto, talvez?), essa análise mais avançada pode ser construída no `Report Builder`.

## Quais informações devo enviar para o suporte para configurar minha análise? {#support}

A criação de um relatório `qualitative cohort` no `Report Builder` envolve a equipe de analistas Adobe criando algumas [colunas calculadas avançadas](../data-warehouse-mgr/creating-calculated-columns.md) nas tabelas necessárias.

Para criar isso, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (e consulte este artigo!). Veja o que você precisa saber:

* O `metric` com o qual você deseja realizar sua análise de coorte e qual tabela ele usa (exemplo: `Revenue`, criado na tabela `orders`).

* O `user segments` que você deseja definir e onde essas informações estão no banco de dados (exemplo: valores diferentes de `User's referral source`, nativos da tabela `users` e realocados para o `orders`).

* O `cohort date` que você deseja que sua análise use (exemplo: o carimbo de data e hora `User's first order date`). Este exemplo nos permitiria examinar cada segmento e perguntar `How does a user's revenue grow in the months following their first order date?`.

* O `time interval` sobre o qual você deseja ver a análise (exemplo: `weeks`, `months` ou `quarters` após `User's first order date`).

Assim que a equipe de analistas do Adobe responder à pergunta acima, você terá algumas novas colunas calculadas avançadas para criar seu relatório. Em seguida, siga as instruções abaixo para fazer isso.

## Criação da análise qualitativa de coorte {#create}

Primeiro, adicione a métrica em que está interessado na coorte uma vez para cada `cohort` que estiver analisando. Neste exemplo, você deseja ver o `Revenue` cumulativo feito nos meses seguintes à primeira encomenda de um cliente, segmentado pelo `User's referral source`. Isso significa que, para cada segmento, você adiciona uma métrica `Revenue` e filtra pelo segmento específico:

![](../../assets/qualcohort1.gif)

Em segundo lugar, você deve fazer duas alterações nas opções de tempo do relatório:

1. Defina o `time interval` como `None`. Isso ocorre porque você eventualmente agrupa pelo intervalo de tempo como uma dimensão em vez de usar as opções de tempo normais.

1. Defina o `time range` como a janela de tempo que você deseja que o relatório cubra.

Neste exemplo, você vê uma `all time` de `Revenue`. Depois disso, você deve terminar com uma série de pontos:

![](../../assets/qualcohort2.gif)

Terceiro, ajuste para configurar o `cohorts`. Com base nos `cohort date` e `time interval` que você especificou para a equipe de analistas Adobe, você tem uma dimensão em sua conta que executa a data `cohort`. Neste exemplo, essa dimensão personalizada é chamada `Months between this order and customer's first order date`. Usando essa dimensão, você deve:

* `Group by` a dimensão com a opção `group by`

* Selecione todos os valores de `dimension` em que você está interessado

* Com o `Show top/bottom option`, selecione os X meses principais em que você está interessado e classifique pela dimensão `Months between this order and customer's first order date`

Agora é possível ver uma linha para cada `cohort` que você especificou. Confira o exemplo agora — você verá a contribuição de `Revenue` dos usuários de cada fonte de referência, `grouped by` o número de meses entre sua primeira ordem e qualquer ordem subsequente. O exemplo também adicionou um `Cumulative perspective` para ver o crescimento agregado de `cohorts'` - examine a tabela de resultados para obter mais granularidade.

O que isso nos diz? Aqui, a fonte de referência específica `Paid search` é valiosa no primeiro mês de vida útil de compra de um cliente, mas não mantém sua base de clientes com receitas repetidas. Enquanto `Direct Traffic` começa com uma quantidade menor, a receita nos meses seguintes acumula-se em um ritmo semelhante.

Não importa como você o faça, a análise `cohort` é uma ferramenta poderosa na sua caixa de ferramentas de análise. Esse tipo de análise pode fornecer alguns insights interessantes sobre sua empresa, que o `time-based cohorts` tradicional pode não fornecer, permitindo que você tome melhores decisões orientadas por dados.
