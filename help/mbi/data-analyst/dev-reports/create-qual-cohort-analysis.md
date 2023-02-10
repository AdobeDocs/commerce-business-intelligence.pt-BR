---
title: Criar uma análise de coorte qualitativa
description: Saiba o que é um coorte qualitativo, por que você pode estar interessado em criar essa análise e como criá-la em [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Crie um `Qualitative Cohort Analysis`

Você sabe como seu [!DNL Adwords]Segmentos de clientes adquiridos aumentam o LTV em comparação aos clientes adquiridos a partir de pesquisa orgânica? Você já pensou em executar uma `cohort` análise em diferentes segmentos de clientes lado a lado no mesmo relatório? Em caso afirmativo, `qualitative cohort analysis` O ajudará você a responder a essas perguntas.

Neste artigo, investigamos o que é um coorte qualitativo, por que você pode estar interessado em criar essa análise e como criá-la em [!DNL MBI].

## O que são `qualitative cohorts`E mesmo assim? {#whatare}

`Cohort` Em geral, a análise pode ser definida como a análise de grupos de utilizadores que partilham características semelhantes ao longo dos seus ciclos de vida. Ela permite identificar tendências comportamentais em diferentes grupos de usuários.

Consulte [análise de coorte](https://www.cohortanalysis.com/) - escrevemos o site nele!

Mais `cohort` análises em [!DNL MBI] agrupe os usuários por uma data comum (por exemplo, o conjunto de todos os clientes que fizeram sua primeira compra em um determinado mês). A `qualitative cohort` é um pouco diferente: é um grupo de usuários definido por uma característica que não se baseia no tempo. Alguns exemplos incluem:

* O conjunto de todos os usuários que foram adquiridos de uma campanha publicitária
* O conjunto de todos os usuários cuja primeira compra incluiu um cupom (ou não)
* O conjunto de todos os usuários de uma determinada idade

## Como isso difere do normal? `cohort` construtor? {#different}

O [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) O é otimizado para agrupar coortes usando uma característica com base em tempo. Isso é ótimo para análises focadas em um segmento específico de usuário (por exemplo, todos os usuários que foram adquiridos por meio de uma campanha de pesquisa paga). No `Cohort Analysis Builder`, você pode (1) focar nesse grupo de usuários específico e (2) `cohort` em uma data (como a data do primeiro pedido).

No entanto, se você quiser analisar o comportamento de coorte de vários segmentos de usuários no mesmo relatório de coorte (`paid` pesquisa versus `organic` tráfego de pesquisa versus tráfego direto, talvez?), essa análise mais avançada pode ser construída no `Report Builder`.

## Quais informações devo enviar para oferecer suporte para configurar minha análise? {#support}

Criação de um `qualitative cohort` no relatório `Report Builder` envolve nossa equipe de analistas criando alguns [colunas calculadas avançadas](../data-warehouse-mgr/creating-calculated-columns.md) nas tabelas necessárias.

Para criá-los, envie uma [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (e consulte este artigo!). Veja o que precisamos saber:

* O `metric` você deseja executar a análise de coorte com e qual tabela ela usa (exemplo: `Revenue`, criado na `orders` tabela).

* O `user segments` você deseja definir e onde essas informações estão no seu banco de dados (por exemplo: diferentes valores de `User's referral source`nativo para o `users` e relocalizada para o `orders`).

* O `cohort date` você deseja que sua análise use (exemplo: o `User's first order date` timestamp). Este exemplo nos permitiria analisar cada segmento e perguntar `How does a user's revenue grow in the months following their first order date?`.

* O `time interval` que você deseja visualizar a análise (exemplo: `weeks`, `months`ou `quarters` após a `User's first order date`).

Assim que a equipe de analistas responder ao acima, você terá algumas novas colunas calculadas avançadas para criar seu relatório! Então você poderá seguir as instruções abaixo para fazer isso.

## Criação da análise de coorte qualitativa {#create}

Primeiro, você deseja adicionar a métrica em que está interessado na coorte, uma vez para cada `cohort` você está analisando. Neste exemplo, queremos ver cumulativo `Revenue` feito nos meses seguintes ao primeiro pedido de um cliente, segmentado pela variável `User's referral source`. Isso significa que, para cada segmento, adicionaremos um `Revenue` métrica e filtro para o segmento específico:

![](../../assets/qualcohort1.gif)

Segundo, você deve fazer duas alterações nas opções de tempo do relatório:

1. Defina as `time interval` para `None`. Isso ocorre porque eventualmente nos agrupamos pelo intervalo de tempo como uma dimensão, em vez de usar as opções de horário normais.

1. Defina as `time range` na janela de tempo que deseja que o relatório cubra.

Em nosso exemplo, observamos uma `all time` visão de `Revenue`. Depois disso, você deve acabar com uma série de pontos:

![](../../assets/qualcohort2.gif)

Em terceiro lugar, você fará um ajuste para realmente configurar o `cohorts`. Com base na `cohort date` e `time interval` você especificou para nossa equipe de analistas, você terá uma dimensão em sua conta que executará a variável `cohort` de datas. Neste exemplo, essa dimensão personalizada é chamada de `Months between this order and customer's first order date`. Com essa dimensão, você deve:

* `Group by` a dimensão com a `group by` opção

* Selecione todos os valores da variável `dimension` em que está interessado

* Com o `Show top/bottom option`, selecione os X meses principais de seu interesse e classifique pelo `Months between this order and customer's first order date` dimension

Agora, você pode ver uma linha para cada `cohort` que você especificou. Vejam o nosso exemplo agora — vemos o `Revenue` contribuído por usuários de cada fonte de referência, `grouped by` o número de meses entre o primeiro pedido e qualquer pedido subsequente. Adicionamos também um `Cumulative perspective` para ver o `cohorts'` crescimento agregado - consulte a tabela de resultados para obter mais granularidade.

O que isso nos diz? Aqui, a fonte de referência específica `Paid search` O é muito valioso no primeiro mês do ciclo de vida de compra de um cliente, mas não mantém sua base de clientes com receita repetida. Ao `Direct Traffic` começa com um valor inferior, a receita nos meses seguintes acumula-se efetivamente a um ritmo semelhante.

Não importa o que você diga. `cohort` a análise é uma ferramenta poderosa na sua caixa de ferramentas de análise. Esse tipo de análise pode fornecer insights muito interessantes sobre seus negócios que o `time-based cohorts` O pode não, permitindo que você tome decisões melhores orientadas por dados.
