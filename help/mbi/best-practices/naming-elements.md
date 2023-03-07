---
title: Nomear relatórios e elementos no MBI
description: Saiba mais sobre as práticas recomendadas para nomear relatórios e elementos no [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Nomear relatórios e elementos

Antes de começar a criar em[!DNL MBI], Adobe quer compartilhar alguns segredos para o sucesso. Saber como criar métricas, filtros e assim por diante é importante, mas todo o seu trabalho pode ser em vão se você não conseguir encontrar o que precisa ou se houver ambiguidade.

## Por que a nomenclatura é importante? {#why}

A forma como você nomeia colunas calculadas, métricas e relatórios determina a facilidade com que diferentes usuários podem navegar pelos seus [!DNL MBI] conta. Ao nomear esses recursos, lembre-se dos três Cs:

* **CLAREZA** - Para que você possa ter uma ideia geral do que um relatório está mostrando, o que uma métrica faz e assim por diante.
* **CONSISTÊNCIA** - Para que você (e a equipe de suporte do Adobe) possam encontrar e entender facilmente elementos e relatórios em sua conta.
* **CREDIBILIDADE** - A fim de inspirar e capacitar outras organizações [!DNL MBI] usuários, você precisa incutir confiança em como eles entendem e usam os dados!

Leia para dicas de nomenclatura testadas e verdadeiras!

## Práticas recomendadas gerais {#general}

### Seja significativo {#meaningful}

Seja específico sempre que possível! Por exemplo, se for o país, você sabe se é o país de envio ou de faturamento? É a cidade do usuário ou é a cidade do negócio?

**Exemplo incorreto:**
Receita

Isso é vago e não nos diz muito.

**Bons exemplos:**
Receita (total geral base + taxa) País de remessa do usuário

Esses exemplos são específicos, o que diminui o potencial de confusão.

### Ser consistente com maiúsculas {#capitalize}

Adobe recomenda que a primeira letra seja maiúscula com o restante dos caracteres em minúsculas, a menos que o estilo substantivo adequado seja capitalizado. Por exemplo, **Número do pedido do usuário** em vez de **Número do pedido do usuário.**

Isso é realmente uma questão de preferência, mas o que deve ser lembrado é ser consistente com o que você escolher.

### Consistência da entidade {#entity}

Você provavelmente já tem uma nomenclatura em vigor em sua empresa. Mantenha as métricas e dimensões que você implementou consistentes com o que é usado em outros bancos de dados e ferramentas. Por exemplo:

* Usuário vs. Cliente vs. Membro vs. Conta
* Empresa versus Conta versus Organização
* Registro vs. criação

### Ortografia e gramática {#spelling}

Certifique-se de verificar novamente a sua ortografia e não se esqueça desses possessivos chatos!

## Gráficos {#charts}

Ao nomear [gráficos](../tutorials/using-visual-report-builder.md), é mais útil seguir esta fórmula: **(Perspectiva De Dados) + (Métrica) + (Período) + (Intervalo)**

**Exemplo incorreto:**
Receita

Isso não nos diz nada sobre o relatório, que é ruim.

**Exemplo correto:**
Receita cumulativa nos últimos 30 dias por mês

Isso nos diz **exatamente** o que está no relatório, que é fantástico.

## Painéis {#dashboards}

Os painéis devem ser nomeados de forma a representar tematicamente os relatórios contidos neles. Por exemplo, se o painel contiver apenas informações relacionadas a receita e pedidos, considere nomeá-lo como **Nome da loja — Receita e pedidos.**

Por outro lado, se o painel for um local em que você está experimentando com relatórios diferentes, considere nomeá-lo **Sandbox do seu nome** portanto, você sabe que os relatórios contidos aqui são rascunhos.

## Dimension (colunas calculadas) {#dimensions}

Ao nomear novo [dimensões](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), é mais útil seguir esta fórmula: **(Entidade) + (Enésimo) + (intervalo de tempo) + (cálculo) + (comentários)**. Por exemplo:

Receita dos primeiros 30 dias do usuário
* Número do pedido do usuário
* Número do pedido do usuário (aguardando auditoria)

## Conjuntos de filtros {#filterset}

[Conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) normalmente são nomeados de maneiras que explicam as informações que incluem ou excluem. Por exemplo, nomear um conjunto de filtros **Pedir itens que contamos** O permite que qualquer usuário entre no, visualize a lógica do conjunto de filtros e entenda quais informações de ordem determinam o que é contado na empresa. Lembre-se de que os conjuntos de filtros podem ser aplicados a métricas e colunas calculadas e devem ser fáceis de entender.

## Métricas {#metrics}

[Métricas](../data-user/reports/ess-manage-data-metrics.md) são perguntas para as quais você deseja obter respostas regularmente. Qual foi o número de pedidos no mês passado? Qual é o valor médio por vida útil de seus clientes? É uma prática recomendada nomear métricas para refletir a resposta que estão dando aos usuários. Além disso, se você tiver a mesma métrica filtrada para uma loja ou departamento específico, ela deverá ser rotulada como tal. Por exemplo:

LTV de cliente médio (primeiros 30 dias) Nome da loja - Receita

Por fim, a mesma métrica pode ser organizada por carimbos de data e hora diferentes, dependendo de como os usuários individuais a calculam. Em caso positivo, inclua o carimbo de data e hora no nome:

Receita (remetida\_em) Receita (criada\_em)

## Encapsulamento {#wrapup}

Estabelecer o estilo e as convenções de nomenclatura antecipadamente ajuda a configurar o para o sucesso no seu [!DNL MBI] conta. Lembre-se dos três códigos: clareza, consistência e credibilidade.
