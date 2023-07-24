---
title: Análise do impacto do cupom
description: Saiba como analisar o impacto do cupom na aquisição e retenção de clientes.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 2%

---

# Impacto do cupom

Analisar como os clientes usam seus cupons pode fornecer informações significativas sobre sua empresa. Especificamente, analisar como adquirir e reter clientes por meio de cupons. Este tópico explora análises que podem ajudá-lo a responder aos seguintes tipos de perguntas:

* Quantos clientes você está adquirindo através de cupons?
* Os clientes adquiridos com cupons têm mais probabilidade de fazer compras repetidas do que os clientes não adquiridos por meio de cupons?
* Como a receita média vitalícia difere entre clientes adquiridos de cupom e clientes não adquiridos por meio de cupons?
* Os clientes adquiridos de cupons fazem compras repetidas com cupons?

Responda a essas perguntas se concentrando em [comparação de clientes adquiridos com cupom com clientes não adquiridos com cupom](#compare), [análise de detalhes da primeira ordem de aquisições de cupom](#firstorder), e [analisar os atributos de clientes que usam cupons em sua primeira ordem.](#attributes)

Comece já!

## Comparação de clientes adquiridos com cupom com clientes não adquiridos com cupom {#compare}

Ao criar análises que explorem a aquisição e a retenção de cupom, considere usar as seguintes métricas:

### Número de novos clientes

Essa métrica mostra o número de clientes adquiridos e não adquiridos com cupom ao longo de todo o tempo. Isso pode ajudá-lo a determinar a proporção de aquisições de clientes por meio de cupons.

### Receita média vitalícia

Essa métrica mostra a receita média vitalícia de clientes adquiridos com e sem cupom. Isso pode ajudar a determinar se o valor vitalício de um cliente varia dependendo do tipo de aquisição.

### Número de ordens repetidas

Essa métrica mostra o número de ordens repetidas feitas por ambos os tipos de aquisições de clientes. Isso pode ajudar a determinar se mais pedidos de acompanhamento são feitos por clientes adquiridos ou não com cupom.

### Número e porcentagem de ordens repetidas com cupom

Mostra o número de pedidos repetidos feitos com um cupom aplicado e a porcentagem de pedidos repetidos feitos com um cupom. Isso pode ajudar você a determinar se os clientes adquiridos com cupom tendem a fazer mais pedidos repetidos com um cupom do que os clientes adquiridos sem cupom e se os clientes adquiridos com cupom estão usando cupons de forma desproporcional em suas ordens de acompanhamento.

Analise alguns dados de exemplo para métricas de aquisição de cupom versus aquisição de não cupom:

| **Aquisição de clientes** | **Número de novos clientes** | **Receita média vitalícia** | **Número de ordens repetidas** | **Número de ordens repetidas c/ cupom** | **% de ordens repetidas c/ cupom** |
|-----|-----|-----|-----|-----|-----|
| Cupom | 1,206 | $356.91 | 2,570 | 1,248 | 48.56% |
| Sem cupom | 11,561 | $498.30 | 20,145 | 3,251 | 16.14% |

{style="table-layout:auto"}

Veja o que você pode tirar disso:

### Número de novos clientes

No exemplo acima, há um número muito maior de aquisições sem cupom do que de aquisições com cupom. No entanto, ainda existem 1.206 clientes adquiridos por meio de um cupom que, de outra forma, poderiam não se tornar clientes.

### Receita média vitalícia

Neste exemplo, as aquisições que não são de cupom têm uma receita média por vida maior do que as aquisições de cupom. Isto implica que as aquisições sem cupons estão fazendo compras mais repetidas e/ou estão fazendo compras de maior valor.

### Número de ordens repetidas

O número de ordens repetidas para aquisições que não são de cupom é muito maior do que as aquisições de cupom. Isso é esperado porque há muito mais clientes adquiridos sem cupom.

### Número de ordens repetidas com cupom

Da mesma forma, o número de ordens repetidas feitas com um cupom é maior para aquisições que não são de cupom.

## Porcentagem de ordens repetidas com cupom

Os clientes não adquiridos com cupom têm uma porcentagem muito menor de pedidos repetidos com um cupom aplicado do que os clientes adquiridos com cupom. Assim, para os clientes adquiridos com cupão, quase metade das ordens repetidas tem um cupão aplicado. Neste exemplo, os clientes de cupom adquiridos tendem a fazer compras repetidas com cupons.

## Análise de detalhes da primeira ordem das aquisições de cupom {#firstorder}

Esta seção foca apenas em **primeiras ordens de aquisições de cupom, segmentadas por cupom.** Use estas métricas em sua análise:

### Número de pedidos/clientes

Essa métrica mostra o número de pedidos pela primeira vez para cada cupom ou o número de clientes que usaram esse cupom na primeira ordem. Isso pode ajudar a determinar se um determinado cupom incentiva mais compras pela primeira vez do que outros cupons.

### Receita bruta

Essa métrica revela a receita obtida com um cupom específico que foi usado no primeiro pedido de um cliente. Esta receita é um cálculo de itens vendidos antes da aplicação de descontos.

### Descontos de cupons

Essa métrica mostra o valor total do desconto aplicado dos cupons.

### Receita líquida

Essa métrica revela a receita obtida com um cupom específico que foi usado no primeiro pedido de um cliente. Essa receita é um cálculo de itens vendidos depois que todos os descontos são aplicados. É importante observar que a receita líquida pode não ter ocorrido sem os cupons.

### Valor médio de pedido

Essa métrica revela o valor médio de pedido de um cupom específico.

### Número médio de ordens vitalícias

Essa métrica ajuda a avaliar a fidelidade e o número médio de pedidos gerados por clientes que usam um determinado cupom.

### Receita média vitalícia

Essa métrica ajuda a avaliar a fidelidade e a receita média geradas pelos clientes que usam um determinado cupom. Ao avaliar se os clientes que usam cupons têm valor maior do que outros, considere o número de pedidos em que cada cupom foi usado para garantir que você tenha um tamanho de amostra significativo.

Agora, veja um exemplo envolvendo três cupons diferentes usados para o pedido de clientes pela primeira vez:

| **Cupom** | **Ordens pela primeira vez (FTO)** | **Receita bruta de FTO** | **Descontos aplicados a FTO** | **Receita líquida de FTO** | **Valor médio de pedido para FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% de desconto em US$ 100 ou mais** | 56 | $8,531.04 | $2,132.76 | $6,398.28 | $152.34 |
| **$10 de desconto** | 87 | $3,707.07 | $426.10 | $3,280.97 | $42.61 |
| **20% de desconto** | 145 | $10,975.05 | $2,195.01 | $8,780.04 | $75.69 |

{style="table-layout:auto"}

O que podemos tirar disso? Primeiro, o cupom com &quot;20% de desconto&quot; teve o maior número de pedidos pela primeira vez. No entanto, o número de pedidos associados a cada cupom pode variar com base em vários fatores, incluindo:

* a quantidade de anúncio para cada cupom.
* o período pelo qual os cupons foram oferecidos.
* a hora do dia/semana/mês/ano em que os cupons foram oferecidos.
* a temporada em que os cupons foram oferecidos, dependendo do negócio.

  **Exemplo:** o cupom de &quot;20% de desconto&quot; foi oferecido durante os meses de verão, mas a empresa vende roupas de inverno.
* as restrições aos cupões.

  **Exemplo:** o cupom de &quot;10% de desconto&quot; é oferecido apenas aos clientes que compram um casaco de inverno na mesma ordem.

A variável **receita bruta** para o cupom &quot;25% de desconto de US$ 100 ou mais&quot;, é muito maior do que a receita bruta do cupom &quot;US$ 10 de desconto&quot;. No entanto, o cupom de &quot;$10 off&quot; tem um muito maior **número de ordens**. Análise da **valor médio de pedido** O fornece informações sobre essas diferenças. Embora o cupom com &quot;25% de desconto de US$ 100 ou mais&quot; tenha menos pedidos, o valor médio do pedido é superior ao triplo do cupom com &quot;US$ 10 de desconto&quot;. Assim, uma receita bruta maior é atribuída ao cupom &quot;25% de desconto de US$ 100 ou mais&quot;.

A variável **descontos** e **receita líquida** para os cupons &quot;25% de desconto de US$ 100 ou mais&quot; e &quot;20% de desconto&quot;, os cupons têm valor próximo. Mesmo que o valor médio de pedido para &quot;25% de desconto de US$ 100 ou mais&quot; esteja próximo do dobro do valor médio de pedido para &quot;20% de desconto&quot;, o último cupom tem um pouco menos do que o triplo do número de pedidos.

## Atributos de clientes que usam cupons em sua primeira ordem {#attributes}

Agora que você analisou os próprios pedidos, analise os clientes que usam cupons em seus primeiros pedidos:

| **Cupom de primeira ordem do cliente** | **Número de clientes** | **Número médio de ordens vitalícias** | **Receita média vitalícia** |
|-----|-----|-----|-----|
| **25% de desconto em US$ 100 ou mais** | 56 | 2.8 | $554.54 |
| **$10 de desconto** | 87 | 1.9 | $115.50 |
| **20% de desconto** | 145 | 1.3 | $103.75 |

{style="table-layout:auto"}

Você percebe que o número de pedidos pela primeira vez é o mesmo que o número de clientes para cada cupom. Isso faz sentido porque cada cliente só pode ter uma primeira ordem.

O maior número de clientes foi adquirido por meio do cupom com &quot;20% de desconto&quot;. No entanto, esses clientes têm a menor **número médio de ordens vitalícias** e **receita média vitalícia**; geralmente, a maioria dos clientes adquiridos com cupons não faz pedidos repetidos. Além disso, os clientes adquiridos através do drive de cupom &quot;25% de desconto de US$ 100 ou mais&quot; mais alto **número médio de ordens vitalícias** e, por sua vez, **receita média vitalícia**. Geralmente, os usuários que foram adquiridos através deste cupom geralmente voltam e fazem mais compras repetidas.

## Encapsulamento {#wrapup}

Há uma variedade de análises que você pode criar para entender melhor como seus clientes usam cupons. Já pensou em analisar como seus clientes usam seus cupons ou o tempo que leva para que os cupons sejam usados? E quanto a encontrar a quantia ideal de desconto - que quantia incentiva compradores recorrentes, maior valor médio de pedido e maior receita vitalícia? Para obter ajuda com esses tipos de perguntas, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
