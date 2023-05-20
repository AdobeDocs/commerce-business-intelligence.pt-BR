---
title: Análise do uso do cupom
description: Saiba como analisar o uso de cupons na aquisição e retenção de clientes.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# Uso do cupom

Você já se perguntou como a oferta de cupons afeta seus negócios? Quer saber quais cupons estão ajudando ou prejudicando o desempenho? Este tópico explora análises que fornecem uma boa imagem do uso de cupom dos clientes respondendo a estas perguntas:

* Quantos clientes estão usando os cupons?
* Quantos cupons estão sendo usados?
* Qual é a receita antes e depois que os cupons são aplicados?
* Qual é a valor médio de pedido antes e depois que os cupons são aplicados?
* Que tipo de clientes você está atraindo com os cupons?

## Métricas recomendadas {#metrics}

Ao analisar o uso do cupom, considere usar ([ou construção](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Número de ordens

Essa métrica mostra o número de pedidos com e sem cupons ao longo do tempo. Isso mostra se e com que frequência os clientes estão usando seus cupons e como isso muda com o tempo.

### Receita bruta

Essa métrica revela a receita bruta obtida de pedidos que incluem um cupom específico. A receita bruta é um cálculo do preço total dos itens vendidos, antes da aplicação de descontos. Isso pode ajudar a determinar quais cupons estão associados à receita bruta mais alta e mais baixa.

### Descontos de cupons

Essa métrica pode mostrar o valor total do desconto aplicado dos cupons. É importante observar que esses pedidos podem não ter ocorrido sem os cupons.

### Receita líquida

Essa métrica mostra a receita líquida que você ganha com pedidos que incluem um cupom específico. A receita líquida é um cálculo do preço dos itens vendidos depois que todos os descontos são aplicados. Isso pode ajudar a determinar quais cupons estão associados à receita líquida mais alta e mais baixa.

### Porcentagem descontada

Isso mostra o compartilhamento de receita brutos que são compensados por descontos. Para cupons que oferta um desconto percentual, esse valor já é conhecido (por exemplo, 10% de desconto). Apesar disso, esse medir fornece insight e um método de comparação para os cupons que são um desconto fixo em dólar.

### Valor médio solicitar líquido

Esta medida mostra o valor médio de pedido quando um cupom é aplicado. Você pode analisar se os pedidos com cupons têm consistentemente um valor de pedido menor do que os pedidos sem cupons.

### Desconto médio de pedido

Ela mostra o valor médio em dólar descontado de cada pedido em que os cupons são aplicados. Isso exibe a diferença entre o valor líquido médio da ordem e o valor bruto médio da ordem.

### Compradores distintos

Este métrica exibe o número de compradores distintos que usam um determinado cupom.

### tempo de vida média receita

Esta métrica ajuda a avaliar a fidelidade e a média de receita geradas pelos clientes que usam um certo cupom. Ao avaliar se os clientes que usam cupons têm maior valor que outros, certifique-se de conta pelo número de compradores distintos em cada categoria para garantir que você tenha um tamanho de amostra significativo.

## Exemplo {#example}

Agora que você sabe quais métricas examinar, veja um exemplo envolvendo três cupons diferentes--10% desligado, $20 desligado $100 ou mais e $10 desativado.

| **Cupom** | **número de pedidos** | **receita bruta** | **Descontos brutos dos cupons** | **NET receita** | **Porcentagem descontada** |
|-----|-----|-----|-----|-----|-----|
| **10% de desconto** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **$20 desligado em $100 +** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **$10 desativado** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style="table-layout:auto"}


| **Cupom** | **Média valor líquido da ordem** | **Média desconto do pedido** | **Compradores distintos** | **Avg. tempo de vida receita** |
|-----|-----|-----|-----|-----|
| **10% de desconto** | $225.08 | $25.01 | 79 | $361.50 |
| **US$ 20 de desconto US$ 100+** | $117.91 | $20.00 | 95 | $218.76 |
| **$10 de desconto** | $62.35 | $10.00 | 199 | $84.27 |

{style="table-layout:auto"}

## O que você pode tirar disso?

Cerca de 80 pedidos foram colocados com a cupom &quot;10% off&quot;, 100 pedidos com o &quot;$20 desligado $100 ou mais&quot; cupom e 200 pedidos com o cupom &quot;$10 desativado&quot;. O número de pedidos **associados a** cada cupom pode variar com base em vários fatores, incluindo:

* o período de tempo durante o qual os cupons foram oferecidos.
* a hora em que o dia/semana/mês/ano os cupons foram oferecidos.
* a temporada em que os cupons foram oferecidos, dependendo do negócio. Por exemplo:
* O cupom de &quot;10% de desconto&quot; foi oferecido durante os meses de verão, mas a empresa vende roupas de inverno.

* as restrições aos cupões. Por exemplo:
* O cupom de desconto de &quot;$10&quot; só é oferecido a novos clientes.
* A cupom &quot;10% off&quot; é oferecida somente aos clientes que compram uma revestimento de inverno no mesmo solicitar.

* o comportamento de aquisição do cliente típico.

Embora os **descontos** brutos para todos os três cupons sejam semelhantes (ao redor de $2000), o número de pedidos de cada cupom é diferente. A análise de descontos por solicitar ajuda a explicar os motivos desses números de contraste. A cupom &quot;10% off&quot; tem o menor número de pedidos, mas uma **média solicitar desconto** de cerca de $25. Embora esse cupom tenha um número baixo de pedidos, seu valor médio de desconto alto causa seu valor bruto de desconto para a abordagem $2000.

**Os receita** brutos e líquidos fornecem uma idéia geral do valor total dos pedidos associados a cada cupom. No entanto, essa imagem geral não fornece uma compreensão dos diferentes comportamentos relacionados a cada cupom. Depois de observar uma base por solicitar, você pode ver que o cupom &quot;10% off&quot; tem um valor de solicitar **de rede média alta** , que, por sua vez, leva à sua receita **alta** de rede.

Por outro lado, o cupom com &quot;10% de desconto&quot; tem um valor médio de desconto alto ($25,01), mas o mais baixo **porcentagem descontada**. Isso faz sentido quando você contabiliza seu valor líquido médio de pedido de US$ 225,08. O cupom de &quot;10% de desconto&quot; tem um pequeno desconto por cento de um grande valor líquido médio de pedido, portanto, o desconto médio de pedido é uma grande quantia.

Olhe para o **compradores distintos** e **receita média vitalícia** para cada cupom. A cupom &quot;10% off&quot; tem o mesmo número de pedidos que os compradores distintos. Isso pode ser um resultado de cada cliente limitado a um cupom. Por outro lado, os cupons &quot;$20 desligado $100 ou mais&quot; e &quot;$10 desligado&quot; têm menos compradores distintos que o número de pedidos, o que implica que alguns clientes usaram esses cupons várias vezes.

Para receita de tempo de vida média, você pode ver que a média de tempo de vida receita para cada cupom é maior que o valor médio de solicitar **de rede correspondente** . Isso implica que os clientes efetuaram compras repetidas e/ou o valor de solicitar era muito maior do que o valor médio solicitar de rede.

## O que mais posso analisar? {#otheranalyses}

As análises mencionadas neste tópico podem fornecer informações valiosas sobre como seus clientes usam seus cupons, mas há uma variedade de outras análises que permitem obter informações um pouco mais detalhadas.

**Você poderia analisar as aquisições de clientes com base em cupons.**

Quais cupons estão incentivando os clientes a fazer pedidos? Esses cupons atraem compradores únicos ou incentivam a fidelidade do cliente (em outras palavras, o cliente que faz compras repetidas)?

**Você pode analisar o tempo necessário para que seus clientes usem seus cupons.**

Os cupons foram usados no dia em que são lançados ou há uma semana ou dois decorridos antes que a maioria dos seus clientes os utilize?

**Você pode descobrir o valor de desconto ideal que aumenta fidelização do cliente e valor geral.**

Qual valor de desconto incentiva os compradores repetidos, maior valor médio de pedido e maior tempo de vida receita?

Responder a essas perguntas fornece informações sobre seus clientes, seu comportamento e os cupons que fornecem mais valor para seus negócios.
