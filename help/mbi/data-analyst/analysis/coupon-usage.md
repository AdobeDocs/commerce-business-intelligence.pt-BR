---
title: Análise do uso de cupom
description: Saiba como analisar o uso do cupom em adquirir e reter clientes.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Uso de cupom

Você já se perguntou como os cupons de oferta afetam seu negócio? Quer saber quais cupons estão ajudando ou prejudicando o desempenho? Neste artigo, exploramos análises que fornecem uma boa imagem do uso do cupom de seus clientes respondendo a estas perguntas:

* Quantos clientes estão usando cupons?
* Quantos cupons estão sendo usados?
* Qual é a receita antes e depois da aplicação dos cupons?
* Qual é o valor médio de pedido antes e depois da aplicação dos cupons?
* Que tipo de cliente você está atraindo com cupons?

Vamos começar!

## Métricas recomendadas {#metrics}

Ao analisar o uso do cupom, considere usar ([ou edifício](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Número de pedidos

Essa métrica mostra o número de pedidos com e sem cupons ao longo do tempo. Isso mostra se e com que frequência os clientes estão usando seus cupons e como isso muda ao longo do tempo.

### Receitas brutas

Essa métrica revela a receita bruta obtida com pedidos que incluem um cupom específico. O rendimento bruto é o cálculo do preço total dos itens vendidos, antes de serem aplicados quaisquer descontos. Isso pode ajudar a determinar quais cupons estão associados à receita bruta mais alta e mais baixa.

### Descontos de cupons

Essa métrica pode mostrar a quantia total de desconto aplicada dos cupons. é importante observar que essas ordens podem não ter ocorrido sem os cupons.

### Receitas líquidas

Essa métrica mostra a receita líquida obtida com pedidos que incluem um cupom específico. A receita líquida é um cálculo do preço dos itens vendidos após a aplicação de todos os descontos. Isso pode ajudar a determinar quais cupons estão associados à receita líquida mais alta e mais baixa.

### Porcentagem com desconto

Mostra a parte da receita bruta que é compensada por descontos. Para cupons que oferecem um desconto em porcentagem, esse valor já é conhecido (por exemplo, 10% de desconto). Apesar disso, esta medida fornece informações e um método de comparação para cupons que são um desconto fixo em dólares.

### Valor líquido médio de pedido

Essa medida mostra o valor médio de pedido quando um cupom é aplicado. Você pode analisar se os pedidos com cupons têm consistentemente um valor de pedido menor que os pedidos sem cupons.

### Desconto médio de pedido

Mostra o valor médio em dólar descontado de cada ordem em que são aplicados cupons. Isso exibe a diferença entre o valor líquido médio da ordem e o valor bruto médio da ordem.

### Compradores distintos

Essa métrica exibe o número de compradores distintos que usam um determinado cupom.

### Receita média da vida útil

Essa métrica ajuda a avaliar a fidelidade e a receita média geradas pelos clientes que usam um determinado cupom. Ao avaliar se os clientes que usam cupons têm valor maior que os outros, considere o número de compradores distintos em cada categoria para garantir que você tenha um tamanho de amostra significativo.

## Exemplo {#example}

Agora que sabemos quais métricas observar, vamos dar uma olhada em um exemplo envolvendo três cupons diferentes — 10% de desconto, 20 dólares de US$ 100 ou mais e US$ 10 de desconto.

| **Cupom** | **Número de pedidos** | **Receitas brutas** | **Descontos brutos de cupons** | **Receitas líquidas** | **Porcentagem com desconto** |
|-----|-----|-----|-----|-----|-----|
| **10% de desconto** | 79º | US$ 19.757,02 | US$ 1.975,70 | US$ 17.781,32 | 10,00% |
| **US$ 20 de US$ 100+** | 101º | 13.928,91 $ | US$ 2.020,00 | US$ 11.908,91 | 14,50% |
| **US$ 10 de desconto** | 201º | US$ 14.542,35 | US$ 2.010,00 | US$ 12.532,35 | 13,82% |

{style=&quot;table-layout:auto&quot;}


| **Cupom** | **Média valor líquido da ordem** | **Média desconto de pedido** | **Compradores distintos** | **Média receita vitalícia** |
|-----|-----|-----|-----|-----|
| **10% de desconto** | US$ 225,08 | US$ 25,01 | 79º | US$ 361,50 |
| **US$ 20 de US$ 100+** | US$ 117,91 | US$ 20,00 | 95 | 218,76 $ |
| **US$ 10 de desconto** | US$ 62,35 | US$ 10,00 | 199 | US$ 84,27 |

{style=&quot;table-layout:auto&quot;}

## O que podemos tirar disso?

Cerca de 80 pedidos foram feitos com o cupom de &quot;10% de desconto&quot;, 100 pedidos com o cupom de &quot;$20 de $100 ou mais&quot; e 200 pedidos com o cupom de &quot;$10 de desconto&quot;. O **número de ordens** associado a cada cupom pode variar com base em vários fatores, incluindo:

* a duração da oferta dos cupões.
* a hora do dia/semana/mês/ano em que os cupons foram oferecidos.
* a temporada dos cupons foi oferecida, dependendo do negócio. Por exemplo:
* O cupom de &quot;10% de folga&quot; foi oferecido durante os meses de verão, mas a empresa vende roupas de inverno.

* as restrições aos cupons. Por exemplo:
* O cupom &quot;$10 off&quot; é oferecido apenas para novos clientes.
* O cupom de &quot;10% de desconto&quot; é oferecido apenas para clientes que compram um casaco de inverno no mesmo pedido.

* o comportamento típico de compra do cliente.

Enquanto a variável **descontos brutos** para todos os três cupons são muito semelhantes (cerca de US$ 2.000), o número de pedidos para cada cupom é significativamente diferente. A análise de descontos por pedido ajuda a explicar os motivos para esses números contrastantes. O cupom de &quot;10% de desconto&quot; tem o menor número de pedidos, mas um **desconto médio de pedido** cerca de US$ 25. Mesmo que esse cupom tenha um número baixo de pedidos, seu valor médio de desconto alto faz com que sua quantia bruta de desconto se aproxime de US$ 2.000.

**Receitas brutas e líquidas** fornecer uma ideia geral do valor total das ordens associadas a cada cupom. No entanto, esse quadro geral não oferece uma compreensão dos diferentes comportamentos relacionados a cada cupom. Quando você observa uma base por pedido, pode ver que o cupom de &quot;10% de desconto&quot; tem um valor muito alto **ordem líquida média** , o que, por sua vez, leva ao seu alto **receita líquida**.

Por outro lado, o cupom de &quot;10% de desconto&quot; tem um valor médio de desconto muito alto (US$ 25,01), mas o mais baixo **porcentagem de desconto**. Isso faz sentido quando você considera o valor líquido médio de pedidos de US$ 225,08. O cupom de &quot;10% de desconto&quot; tem um desconto percentual pequeno de um valor líquido médio de pedido grande, então o desconto médio de pedido é uma quantia grande.

Vejamos a **compradores distintos** e **receita média da vida útil** para cada cupom. O cupom de &quot;10% de desconto&quot; tem o mesmo número de pedidos que compradores distintos. Isso pode ser resultado de cada cliente ser limitado a um cupom. Por outro lado, os cupons &quot;$20 de $100 ou mais&quot; e &quot;$10 off&quot; têm menos compradores distintos do que o número de pedidos, o que implica que alguns clientes usaram esses cupons várias vezes.

Para a receita média do tempo de vida, você pode ver que a receita média do tempo de vida de cada cupom é maior que o respectivo **ordem líquida média** valor. Isso implica que os clientes fizeram compras repetidas e/ou seu valor de pedido era muito superior ao valor médio líquido de pedido.

## O que mais posso analisar? {#otheranalyses}

As análises que abordamos neste artigo podem fornecer informações valiosas sobre como seus clientes usam seus cupons, mas há uma infinidade de outras análises que permitem pesquisar um pouco mais fundo.

**Você pode analisar suas aquisições de clientes a partir de cupons.**

Quais cupons estão incentivando os clientes a fazer pedidos? Esses cupons estão atraindo compradores únicos ou incentivam a fidelidade do cliente (em outras palavras, clientes que fazem compras repetidas)?

**Você pode analisar o tempo que leva para seus clientes usarem seus cupons.**

Seus cupons são usados no dia em que são lançados ou decorre uma semana ou duas antes de a maioria dos clientes usá-los?

**Você pode descobrir o valor ideal do desconto que aumenta a fidelidade do cliente e o valor geral.**

Que valor de desconto incentivará compradores repetidos, maior valor médio de pedido e maior receita vitalícia?

Responder essas perguntas fornecerá insights sobre seus clientes, seu comportamento e os cupons que agregam mais valor à sua empresa.
