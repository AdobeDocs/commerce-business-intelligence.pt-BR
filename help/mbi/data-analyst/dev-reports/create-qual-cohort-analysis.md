---
title: Criar uma análise qualitativa de coorte
description: Saiba o que é uma coorte qualitativa, por que você pode estar interessado em criar essa análise e como criá-la no Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Criar um `Qualitative Cohort Analysis`

Você sabe como seus [!DNL Google Adwords]-os segmentos de clientes adquiridos aumentam seu LTV em comparação aos clientes adquiridos da pesquisa orgânica? Você já pensou em executar um `cohort` análise de diferentes segmentos de clientes lado a lado no mesmo relatório? Em caso afirmativo, `qualitative cohort analysis` O ajuda a responder a essas perguntas.

Este tópico aborda o que é uma coorte qualitativa, por que você pode estar interessado em criar essa análise e como criá-la no [!DNL Commerce Intelligence].

## O que são `qualitative cohorts`De qualquer forma? {#whatare}

`Cohort` a análise, em geral, pode ser definida como a análise de grupos de usuários que compartilham características semelhantes ao longo de seus ciclos de vida. Ele permite identificar tendências comportamentais em diferentes grupos de usuários.

Consulte [análise de coorte](https://www.cohortanalysis.com/).

Mais `cohort` análises em [!DNL Commerce Intelligence] agrupe usuários em uma data comum (por exemplo, o conjunto de todos os clientes que fizeram sua primeira compra em um determinado mês). A `qualitative cohort` é um pouco diferente: é um grupo de usuários definido por uma característica que não é baseada no tempo. Os exemplos incluem:

* O conjunto de todos os usuários adquiridos de uma campanha publicitária
* O conjunto de todos os usuários cuja primeira compra incluiu um cupom (ou não)
* O conjunto de todos os usuários com determinada idade

## Como isso difere do normal? `cohort` construtor? {#different}

A variável [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) é otimizado para agrupar coortes usando uma característica baseada em tempo. Isso é ótimo para análises com foco em um segmento específico de usuário (por exemplo, todos os usuários que foram adquiridos por meio de uma campanha de pesquisa paga). No `Cohort Analysis Builder`, você pode (1) se concentrar nesse grupo de usuários específico e (2) `cohort` em uma data (como a data de seu primeiro pedido).

No entanto, se você deseja analisar o comportamento da coorte de vários segmentos de usuários no mesmo relatório de coorte (`paid` pesquisa versus `organic` pesquisa versus tráfego direto, talvez?), essa análise mais avançada pode ser construída no `Report Builder`.

## Quais informações devo enviar para o suporte para configurar minha análise? {#support}

Criação de um `qualitative cohort` relatório no `Report Builder` envolve a equipe de analistas do Adobe criando algumas [colunas calculadas avançadas](../data-warehouse-mgr/creating-calculated-columns.md) nas tabelas necessárias.

Para criá-los, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (e consulte este artigo!). Veja o que você precisa saber:

* A variável `metric` você deseja executar a análise de coorte com o e qual tabela ele usa (exemplo: `Revenue`, criado com base no `orders` tabela).

* A variável `user segments` que deseja definir e onde essas informações residem no banco de dados (exemplo: valores diferentes de `User's referral source`, nativo para o `users` e realocada para o estado `orders`).

* A variável `cohort date` que deseja que sua análise use (exemplo: a variável `User's first order date` timestamp). Esse exemplo permitiria analisar cada segmento e perguntar `How does a user's revenue grow in the months following their first order date?`.

* A variável `time interval` sobre o qual você deseja ver a análise (exemplo: `weeks`, `months`ou `quarters` depois que a variável `User's first order date`).

Assim que a equipe de analistas do Adobe responder à pergunta acima, você terá algumas novas colunas calculadas avançadas para criar seu relatório. Em seguida, siga as instruções abaixo para fazer isso.

## Criação da análise qualitativa de coorte {#create}

Primeiro, adicione a métrica em que está interessado na coorte, uma vez para cada `cohort` você está analisando. Neste exemplo, você deseja ver as `Revenue` feito nos meses seguintes ao primeiro pedido de um cliente, segmentado pelo `User's referral source`. Isso significa que, para cada segmento, você adiciona um `Revenue` métrica e filtro para o segmento específico:

![](../../assets/qualcohort1.gif)

Em segundo lugar, você deve fazer duas alterações nas opções de tempo do relatório:

1. Defina o `time interval` para `None`. Isso ocorre porque você eventualmente agrupa pelo intervalo de tempo como uma dimensão em vez de usar as opções de tempo normais.

1. Defina o `time range` à janela de tempo que você deseja que o relatório cubra.

Neste exemplo, você vê uma variável `all time` exibição de `Revenue`. Depois disso, você deve terminar com uma série de pontos:

![](../../assets/qualcohort2.gif)

Terceiro, você ajusta para configurar o `cohorts`. Com base no `cohort date` e `time interval` especificado para a equipe de analistas do Adobe, você tem uma dimensão em sua conta que executa a `cohort` namoro. Neste exemplo, essa dimensão personalizada é chamada de `Months between this order and customer's first order date`. Usando essa dimensão, você deve:

* `Group by` a dimensão com a variável `group by` opção

* Selecione todos os valores de `dimension` em que você está interessado

* Com o `Show top/bottom option`, selecione os X meses principais em que você está interessado e classifique por `Months between this order and customer's first order date` dimension

Agora é possível ver uma linha para cada `cohort` especificado. Dê uma olhada no exemplo agora - você vê o `Revenue` contribuído por usuários de cada fonte de referência, `grouped by` o número de meses entre seu primeiro pedido e qualquer pedido subsequente. O exemplo também adicionou um `Cumulative perspective` para ver o `cohorts'` crescimento agregado - observe a tabela de resultados para obter mais granularidade.

O que isso nos diz? Aqui, a fonte de referência específica `Paid search` O é valioso no primeiro mês de vida útil de compra de um cliente, mas o não mantém sua base de clientes com receita repetida. Enquanto `Direct Traffic` começa com uma quantia menor, a receita nos meses subsequentes na verdade se acumula em um ritmo semelhante.

Não importa o quanto você faça isso, `cohort` a análise é uma ferramenta eficiente na sua caixa de ferramentas de análise. Esse tipo de análise pode fornecer alguns insights interessantes sobre sua empresa, `time-based cohorts` não, permitindo que você tome melhores decisões orientadas por dados.
