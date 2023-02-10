---
title: Nomear relatórios e elementos no MBI
description: Conheça as práticas recomendadas para nomear relatórios e elementos no [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Nomear relatórios e elementos

Antes de começar a criar[!DNL MBI], queremos compartilhar alguns de nossos segredos para o sucesso. Saber como criar métricas, filtros e assim por diante é importante, mas tudo isso funcionará completamente se não for possível encontrar o que precisa ou se houver alguma ambiguidade.

## Por que a nomenclatura é importante? {#why}

A maneira como você nomeia colunas, métricas e relatórios calculados determina a facilidade com que usuários diferentes podem navegar pelo seu [!DNL MBI] conta. Ao nomear esses recursos, lembre-se dos três Cs:

* **CLARIDADE** - Assim, você pode ver rapidamente o que um relatório está mostrando, o que uma métrica faz, e assim por diante.
* **CONSISTÊNCIA** - Para que você (e nossa equipe de suporte) possa encontrar e entender facilmente elementos e relatórios em sua conta.
* **CREDIBILIDADE** - Para inspirar e capacitar outros [!DNL MBI] usuários, você precisa confiar em como eles compreendem e usam os dados!

Leia as dicas de nomenclatura testadas e verdadeiras!

## Práticas recomendadas gerais {#general}

### Seja significativo {#meaningful}

Seja específico sempre que possível! Por exemplo, se é o país, você sabe se é o país de envio ou de cobrança? É a cidade do usuário, ou é a cidade do negócio?

**Exemplo incorreto:**
Receita

Isto é vago e não nos diz muito.

**Exemplos bons:**
Receita (total geral base + taxa) País de entrega do usuário

Estes exemplos são específicos, o que diminui o potencial de confusão.

### Seja consistente com a capitalização {#capitalize}

Somos fãs de letras maiúsculas e minúsculas, e o resto dos caracteres fica em minúsculas, a menos que o estilo substantivo adequado de maiúsculas. Por exemplo: **Número do pedido do usuário** em vez de **Número do pedido do usuário.**

Isto é realmente uma questão de preferência, mas a coisa a lembrar é ser consistente com o que você escolher.

### Consistência da entidade {#entity}

Você provavelmente já tem uma nomenclatura em vigor em sua empresa. Mantenha as métricas e dimensões colocadas em prática consistentes com o que é usado em outros bancos de dados e ferramentas. Por exemplo:

* Usuário versus Cliente vs. Membro vs. Conta
* Empresa versus Conta versus Organização
* Registro e criação

### Ortografia e gramática {#spelling}

Certifique-se de verificar a ortografia duas vezes e não se esqueça desses possíveis possessivos!

## Gráficos {#charts}

Ao nomear [gráficos](../tutorials/using-visual-report-builder.md), consideramos mais útil seguir esta fórmula: **(Perspectiva De Dados) + (Métrica) + (Período De Tempo) + (Intervalo De Tempo)**

**Exemplo incorreto:**
Receita

Isto não nos diz nada sobre o relatório, que é mau.

**Exemplo correto:**
Receita cumulativa após 30 dias por mês

Isso nos diz **exatamente** o que está no relatório, o que é fantástico.

## Painéis {#dashboards}

Os painéis devem ser nomeados de formas que representem automaticamente os relatórios contidos neles. Por exemplo, se o painel contiver apenas informações relacionadas a receita e pedidos, considere nomeá-lo como **Nome da Loja - Receita e pedidos.**

Por outro lado, se o painel for um local em que você está fazendo testes com relatórios diferentes, considere nomeá-lo **Sandbox do seu nome** para que você saiba que os relatórios contidos são rascunhos.

## Dimension (colunas calculadas) {#dimensions}

Ao nomear novos [dimensões](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), consideramos mais útil seguir esta fórmula: **(Entidade) + (Nth) + (intervalo de tempo) + (cálculo) + (comentários)**. Por exemplo:

Receita dos primeiros 30 dias do usuário
* Número do pedido do usuário
* Número do pedido do usuário (aguardando auditoria)

## Conjuntos de filtros {#filterset}

[Conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) normalmente são nomeadas de forma a explicar as informações que estão incluindo ou excluindo. Por exemplo, nomear um conjunto de filtros **Ordenar itens contados** O permitirá que qualquer usuário entre, visualize a lógica do conjunto de filtros e entenda quais informações de ordem determinam o que é contado na empresa. Lembre-se de que os conjuntos de filtros podem ser aplicados a colunas calculadas e métricas, e devem ser fáceis de entender.

## Métricas {#metrics}

[Métricas](../data-user/reports/ess-manage-data-metrics.md) são essencialmente perguntas para as quais você deseja obter respostas regularmente. Qual foi o número de pedidos no mês passado? Qual é o valor médio da vida útil de nossos clientes? Geralmente, é uma prática recomendada nomear métricas para refletir a resposta que estão dando aos usuários. Além disso, se você tiver a mesma métrica filtrada para uma loja ou departamento específico, ela deve ser rotulada como tal. Por exemplo:

LTV de cliente médio (primeiros 30 dias) Nome do armazenamento - Receita

Por fim, a mesma métrica pode, às vezes, ser organizada por diferentes carimbos de data e hora, dependendo de como os usuários individuais a calculam. Se esse for o caso, inclua o carimbo de data e hora no nome:

Receita (enviado\_at) Receita (criada\_at)

## Quebra de linha {#wrapup}

Estabelecer estilo e convenções de nomenclatura antecipadamente ajudará a configurar o sucesso em [!DNL MBI] conta. Lembre-se dos três C&#39;s: clareza, coerência e credibilidade.
