---
title: Nomear relatórios e elementos no Commerce Intelligence
description: Conheça as práticas recomendadas para nomear relatórios e elementos no [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Nomear relatórios e elementos

Antes de começar a criar no [!DNL Adobe Commerce Intelligence], a Adobe deseja compartilhar alguns segredos com sucesso. Saber como criar métricas, filtros e assim por diante é importante, mas todo o seu trabalho pode ser em vão se você não conseguir encontrar o que precisa ou se houver ambiguidade.

## Por que a nomenclatura é importante? {#why}

A forma como você nomeia colunas calculadas, métricas e relatórios facilita a navegação de diferentes usuários pela sua conta do [!DNL Commerce Intelligence]. Ao nomear esses recursos, lembre-se dos três Cs:

* **CLAREZA** - para que você possa saber rapidamente o que um relatório está mostrando, o que uma métrica faz e assim por diante.
* **CONSISTÊNCIA** - Para que você (e a equipe de suporte da Adobe) possam encontrar e entender facilmente elementos e relatórios em sua conta.
* **CREDIBILIDADE** - Para inspirar e capacitar outros usuários do [!DNL Commerce Intelligence] orientados por dados, é necessário incutir confiança em como eles entendem e usam os dados!

Leia para dicas de nomenclatura testadas e verdadeiras!

## Práticas recomendadas gerais {#general}

### Seja significativo {#meaningful}

Seja específico sempre que possível! Por exemplo, se for o país, você sabe se é o país de envio ou de faturamento? É a cidade do usuário ou é a cidade do negócio?

**Exemplo incorreto:**
Receita

Isso é vago e não nos diz muito.

**Bons exemplos:**
Receita (total geral base + taxa)
País de remessa do usuário

Esses exemplos são específicos, o que diminui o potencial de confusão.

### Ser consistente com maiúsculas {#capitalize}

[!DNL Adobe] recomenda que a primeira letra seja maiúscula com o restante dos caracteres em minúsculas, a menos que o estilo substantivo apropriado seja capitalizado. Por exemplo, **Número de pedido do usuário** em vez de **Número de pedido do usuário.**

Isso é realmente uma questão de preferência, mas o que deve ser lembrado é ser consistente com o que você escolher.

### Consistência da entidade {#entity}

Você provavelmente já tem uma nomenclatura em vigor em sua empresa. Mantenha as métricas e dimensões que você implementou consistentes com o que é usado em outros bancos de dados e ferramentas. Por exemplo:

* Usuário vs. Cliente vs. Membro vs. Conta
* Empresa versus Conta versus Organização
* Registro vs. criação

### Ortografia e gramática {#spelling}

Certifique-se de verificar novamente a sua ortografia e não se esqueça desses possessivos chatos!

## Gráficos {#charts}

Ao nomear [gráficos](../tutorials/using-visual-report-builder.md), é mais útil seguir esta fórmula: **(Perspectiva de Dados) + (Métrica) + (Período) + (Intervalo)**

**Exemplo incorreto:**
Receita

Isso não nos diz nada sobre o relatório, que é ruim.

**Bom exemplo:**
Receita cumulativa nos últimos 30 dias por mês

Isso nos informa **exatamente** o que está no relatório, o que é fantástico.

## Painéis {#dashboards}

Os painéis devem ser nomeados de forma a representar tematicamente os relatórios contidos neles. Por exemplo, se o seu painel contiver apenas informações relacionadas a receita e pedidos, considere nomeá-lo como **Nome da loja - Receita e pedidos.**

Por outro lado, se o seu painel for um local onde você está experimentando com relatórios diferentes, considere nomeá-lo como **Sandbox do seu nome** para que você saiba que os relatórios contidos nele são rascunhos.

## Dimensões (colunas calculadas) {#dimensions}

Ao nomear novas [dimensões](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), é mais útil seguir esta fórmula: **(Entidade) + (Enésimo) + (intervalo de tempo) + (cálculo) + (comentários)**. Por exemplo:

Receita dos primeiros 30 dias do usuário
* Número do pedido do usuário
* Número do pedido do usuário (aguardando auditoria)

## Conjuntos de filtros {#filterset}

[Os conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) normalmente são nomeados de maneiras que explicam as informações que estão incluindo ou excluindo. Por exemplo, nomear um conjunto de filtros **Pedir itens que contamos** permite que qualquer usuário entre, visualize a lógica do conjunto de filtros e entenda quais informações de pedido determinam o que é contado na empresa. Lembre-se de que os conjuntos de filtros podem ser aplicados a métricas e colunas calculadas e devem ser fáceis de entender.

## Métricas {#metrics}

[Métricas](../data-user/reports/ess-manage-data-metrics.md) são essencialmente perguntas para as quais você deseja obter respostas regularmente. Qual foi o número de pedidos no mês passado? Qual é o valor médio por vida útil de seus clientes? É uma prática recomendada nomear métricas para refletir a resposta que estão dando aos usuários. Além disso, se você tiver a mesma métrica filtrada para uma loja ou departamento específico, ela deverá ser rotulada como tal. Por exemplo:

LTV de cliente médio (primeiros 30 dias)
Nome da Loja - Receita

Por fim, a mesma métrica pode ser organizada por carimbos de data e hora diferentes, dependendo de como os usuários individuais a calculam. Em caso positivo, inclua o carimbo de data e hora no nome:

Receita (remetida\_em)
Receita (criada\_em)

## Encapsulamento {#wrapup}

O estabelecimento antecipado de convenções de estilo e nomenclatura ajuda a configurar com sucesso sua conta do [!DNL Commerce Intelligence]. Lembre-se dos três códigos: clareza, consistência e credibilidade.
