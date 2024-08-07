---
title: Análise do uso do cupom
description: Saiba como analisar o uso de cupons na aquisição e retenção de clientes.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Uso do cupom

Você já se perguntou como a oferta de cupons afeta seus negócios? Quer saber quais cupons estão ajudando ou prejudicando o desempenho? Este tópico explora análises que fornecem uma boa imagem do uso de cupom dos clientes respondendo a estas perguntas:

* Quantos clientes estão usando cupons?
* Quantos cupons estão sendo usados?
* Qual é sua receita antes e depois da aplicação dos cupons?
* Qual é o valor médio de pedido antes e depois da aplicação dos cupons?
* Que tipo de clientes você está atraindo com cupons?

## Métricas recomendadas {#metrics}

Ao analisar o uso do cupom, considere usar ([ou criar](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Número de ordens

Essa métrica mostra o número de pedidos com e sem cupons ao longo do tempo. Isso mostra se e com que frequência os clientes estão usando seus cupons e como isso muda com o tempo.

### Receita bruta

Essa métrica revela a receita bruta obtida de pedidos que incluem um cupom específico. A receita bruta é um cálculo do preço total dos itens vendidos, antes da aplicação de descontos. Isso pode ajudar a determinar quais cupons estão associados à receita bruta mais alta e mais baixa.

### Descontos de cupons

Essa métrica pode mostrar o valor total do desconto aplicado dos cupons. É importante observar que esses pedidos podem não ter ocorrido sem os cupons.

### Receita líquida

Essa métrica mostra a receita líquida que você ganha com pedidos que incluem um cupom específico. A receita líquida é um cálculo do preço dos itens vendidos depois que todos os descontos são aplicados. Isso pode ajudar a determinar quais cupons estão associados à receita líquida mais alta e mais baixa.

### Porcentagem descontada

Mostra a parte da receita bruta que é compensada por descontos. Para cupons que oferecem um desconto percentual, esse valor já é conhecido (por exemplo, 10% de desconto). Apesar disso, essa medida fornece insight e um método de comparação para cupons que são um desconto em dólar fixo.

### Valor líquido médio da ordem

Esta medida mostra o valor médio de pedido quando um cupom é aplicado. Você pode analisar se os pedidos com cupons têm consistentemente um valor de pedido menor do que os pedidos sem cupons.

### Desconto médio de pedido

Ela mostra o valor médio em dólar descontado de cada pedido em que os cupons são aplicados. Isso exibe a diferença entre o valor líquido médio da ordem e o valor bruto médio da ordem.

### Compradores distintos

Essa métrica exibe o número de compradores distintos que usam um determinado cupom.

### Receita média vitalícia

Essa métrica ajuda a avaliar a fidelidade e a receita média geradas pelos clientes que usam um determinado cupom. Ao avaliar se os clientes que usam cupons têm valor maior do que outros, considere o número de compradores distintos em cada categoria para garantir que você tenha um tamanho de amostra significativo.

## Exemplo {#example}

Agora que você sabe quais métricas examinar, veja um exemplo envolvendo três cupons diferentes: 10% de desconto, $20 de desconto em $100 ou mais e $10 de desconto.

| **Cupom** | **# de pedidos** | **Receita bruta** | **Descontos brutos de cupons** | **Receita líquida** | **Percentual com desconto** |
|-----|-----|-----|-----|-----|-----|
| **10% de desconto** | 79 | $ 19.757,02 | $ 1.975,70 | $ 17.781,32 | 10,00% |
| **$20 de desconto $100+** | 101 | $ 13.928,91 | $ 2.020,00 | $ 11.908,91 | 14,50% |
| **$10 de desconto** | 201 | $ 14.542,35 | $ 2.010,00 | $ 12.532,35 | 13,82% |

{style="table-layout:auto"}


| **Cupom** | **Média valor líquido da ordem** | **Média desconto do pedido** | **Compradores distintos** | **Média receita vitalícia** |
|-----|-----|-----|-----|-----|
| **10% de desconto** | $ 225,08 | $ 25,01 | 79 | $ 361,50 |
| **$20 de desconto $100+** | $ 117,91 | $ 20,00 | 95 | $ 218,76 |
| **$10 de desconto** | $ 62,35 | $ 10,00 | 199 | $ 84,27 |

{style="table-layout:auto"}

## O que você pode tirar disso?

Cerca de 80 pedidos foram feitos com o cupom de &quot;10% de desconto&quot;, 100 pedidos com o cupom de &quot;$20 de $100 ou mais&quot; e 200 pedidos com o cupom de &quot;$10 de desconto&quot;. O **número de pedidos** associados a cada cupom pode variar com base em vários fatores, incluindo:

* o período pelo qual os cupons foram oferecidos.
* a hora do dia/semana/mês/ano em que os cupons foram oferecidos.
* a temporada em que os cupons foram oferecidos, dependendo do negócio. Por exemplo:
* O cupom de &quot;10% de desconto&quot; foi oferecido durante os meses de verão, mas a empresa vende roupas de inverno.

* as restrições aos cupões. Por exemplo:
* O cupom de desconto de &quot;$10&quot; só é oferecido a novos clientes.
* O cupom de &quot;10% de desconto&quot; é oferecido apenas aos clientes que compram um casaco de inverno na mesma ordem.

* o comportamento de compra típico do cliente.

Embora os **descontos brutos** para todos os três cupons sejam semelhantes (cerca de US$ 2.000), o número de pedidos para cada cupom é diferente. A análise de descontos por ordem ajuda a explicar os motivos desses números contrastantes. O cupom com &quot;10% de desconto&quot; tem o menor número de pedidos, mas um **desconto médio de pedido** de cerca de US$ 25. Embora esse cupom tenha um número baixo de pedidos, seu alto valor médio de desconto faz com que sua quantia bruta de desconto se aproxime de US$ 2.000.

**Receita bruta e líquida** fornece uma ideia geral do valor total dos pedidos associados a cada cupom. No entanto, esse quadro geral não fornece uma compreensão dos diferentes comportamentos relacionados a cada cupom. Uma vez analisado o valor por ordem, você pode ver que o cupom com 10% de desconto tem um valor alto de **ordem líquida média**, o que, por sua vez, resulta em sua alta **receita líquida**.

Por outro lado, o cupom com &quot;10% de desconto&quot; tem um valor de desconto médio alto ($25,01), mas o menor **percentual com desconto**. Isso faz sentido quando você contabiliza seu valor líquido médio de pedido de US$ 225,08. O cupom de &quot;10% de desconto&quot; tem um pequeno desconto por cento de um grande valor líquido médio de pedido, portanto, o desconto médio de pedido é uma grande quantia.

Examine os **compradores distintos** e a **receita média ao longo da vida** para cada cupom. O cupom com &quot;10% de desconto&quot; tem o mesmo número de pedidos que os compradores distintos. Isso pode ser resultado de cada cliente estar limitado a um cupom. Por outro lado, os cupons &quot;$20 de $100 ou mais&quot; e &quot;$10 de desconto&quot; têm menos compradores distintos do que o número de pedidos, o que implica que alguns clientes usaram esses cupons várias vezes.

Para a receita média por vida, você pode ver que a receita média por vida para cada cupom é maior que o respectivo valor de **ordem líquida média**. Isso implica que os clientes fizeram compras repetidas e/ou o valor de seus pedidos foi muito maior do que o valor líquido médio de pedido.

## O que mais posso analisar? {#otheranalyses}

As análises mencionadas neste tópico podem fornecer informações valiosas sobre como seus clientes usam seus cupons, mas há uma variedade de outras análises que permitem obter informações um pouco mais detalhadas.

**Você pode analisar as aquisições de clientes com cupons.**

Quais cupons estão incentivando os clientes a fazer pedidos? Esses cupons atraem compradores únicos ou incentivam a fidelidade do cliente (em outras palavras, o cliente que faz compras repetidas)?

**Você pode analisar o tempo que leva para seus clientes usarem seus cupons.**

Seus cupons são usados no dia em que são liberados ou uma ou duas semanas antes da maioria de seus clientes os usarem?

**Você pode descobrir o valor do desconto ideal que aumenta a fidelidade do cliente e o valor geral.**

Que quantia de desconto incentiva compradores recorrentes, maior valor médio de pedido e maior receita vitalícia?

Responder a essas perguntas fornece informações sobre os clientes, o comportamento deles e os cupons que agregam mais valor à sua empresa.
