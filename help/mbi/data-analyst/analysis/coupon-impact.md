---
title: Análise do impacto do cupom
description: Saiba como analisar o impacto do cupom na aquisição e retenção de clientes.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Impacto do cupom

A análise de como os clientes usam seus cupons pode fornecer insights significativos para sua empresa. Especificamente, analisando como você adquire e retém clientes por meio de cupons. Neste artigo, exploramos análises que podem ajudar você a responder os seguintes tipos de perguntas:

* Quantos clientes você está adquirindo por meio de cupons?
* Os clientes adquiridos por cupons têm maior probabilidade de realizar compras repetidas do que os clientes não adquiridos por meio de cupons?
* Como a receita média vitalícia difere entre clientes adquiridos por cupons e clientes não adquiridos por meio de cupons?
* Os clientes adquiridos a partir de cupons fazem compras repetidas com cupons?

Para responder a essas perguntas, nos concentramos em [comparação de clientes adquiridos por cupom com clientes adquiridos sem cupom](#compare), [análise de detalhes do primeiro pedido de aquisições de cupom](#firstorder)e [análise dos atributos dos clientes que usam cupons em sua primeira ordem.](#attributes)

Vamos começar!

## Comparação de clientes adquiridos por cupom com clientes adquiridos por não cupom {#compare}

Ao criar análises que exploram sua aquisição e retenção de cupom, considere usar as seguintes métricas:

### Número de novos clientes

Essa métrica mostra o número de clientes adquiridos com cupom e clientes adquiridos sem cupom durante todo o tempo. Isso pode ajudar você a determinar a proporção de aquisições de clientes por meio de cupons.

### Receita média da vida útil

Essa métrica mostra a receita média da vida útil de clientes adquiridos com cupom e sem cupom. Isso pode ajudar a determinar se o valor vitalício de um cliente varia dependendo do tipo de aquisição.

### Número de pedidos repetidos

Essa métrica mostra o número de ordens repetidas feitas por ambos os tipos de aquisições de clientes. Isso pode ajudar a determinar se mais pedidos de acompanhamento são feitos por clientes adquiridos ou não por cupom.

### Número e porcentagem de pedidos repetidos com cupom

Isso mostra o número de pedidos repetidos feitos com um cupom aplicado e a porcentagem de pedidos repetidos feitos com um cupom. Isso pode ajudar você a determinar se os clientes adquiridos por cupom tendem a fazer mais pedidos repetidos com um cupom do que clientes adquiridos por não cupom e se os clientes adquiridos por cupom usam desproporcionadamente cupons em suas ordens de acompanhamento.

Vamos analisar alguns dados de amostra para a aquisição de cupom versus métricas de aquisição sem cupom:

| **Aquisição de clientes** | **Número de novos clientes** | **Receita média da vida útil** | **Número de pedidos repetidos** | **Número de pedidos repetidos com cupom** | **% de ordens repetidas com cupão** |
|-----|-----|-----|-----|-----|-----|
| Cupom | 1 206 | US$ 356,91 | 2 570 | 1 248 | 48,56% |
| Sem cupom | 11 561 | US$ 498,30 | 20 145 | 3 251 | 16,14% |

{style=&quot;table-layout:auto&quot;}

O que podemos tirar disso? Vejamos:

### Número de novos clientes

No exemplo acima, há um número muito maior de aquisições sem cupons do que de aquisições com cupons. No entanto, ainda há 1.206 clientes adquiridos por meio de um cupom que, de outra forma, pode não ter se tornado clientes.

### Receita média da vida útil

Neste exemplo, as aquisições sem cupons têm uma receita média de tempo de vida mais alta do que as aquisições de cupom. Isto implica que as aquisições sem cupão estão a efetuar mais compras repetidas e/ou a efetuar compras de valor mais elevado.

### Número de pedidos repetidos

O número de ordens repetidas para aquisições sem cupons é muito maior do que as aquisições de cupons. Isso é esperado porque há muito mais clientes adquiridos que não são de cupom.

### Número de pedidos repetidos com cupom

Da mesma forma, o número de ordens repetidas feitas com um cupom é maior para aquisições sem cupons.

## #Porcentagem de pedidos repetidos com cupom

Clientes adquiridos sem cupom têm uma porcentagem muito menor de pedidos repetidos com um cupom aplicado do que clientes adquiridos por cupom. Assim, para clientes adquiridos por cupons, quase um em cada dois pedidos repetidos tem um cupom aplicado. Neste exemplo, clientes adquiridos por cupom tendem a fazer compras repetidas com cupons.

## Analisando detalhes do primeiro pedido a partir de aquisições de cupom {#firstorder}

Nesta seção, nos concentramos apenas em **primeiras ordens de aquisições de cupão, segmentadas por cupão.** usamos essas métricas em nossa análise:

### Número de ordens/clientes

Essa métrica mostra o número de pedidos pela primeira vez para cada cupom, ou o número de clientes que usaram esse cupom em seu primeiro pedido. Isso pode ajudar a determinar se um determinado cupom incentiva compras pela primeira vez mais do que outros cupons.

### Receitas brutas

Essa métrica revela a receita obtida com um cupom específico que foi usado no primeiro pedido de um cliente. Esta receita é um cálculo de itens vendidos antes da aplicação de quaisquer descontos.

### Descontos de cupons

Essa métrica mostra o valor total do desconto aplicado aos cupons.

### Receitas líquidas

Essa métrica revela a receita obtida com um cupom específico que foi usado no primeiro pedido de um cliente. Esta receita é um cálculo de itens vendidos após a aplicação de todos os descontos. é importante notar que o rendimento líquido pode não ter ocorrido sem os cupões.

### Valor médio de pedido

Essa métrica revela o valor médio de pedido de um cupom específico.

### Número médio de ordens por vida

Essa métrica ajuda a avaliar a fidelidade e o número médio de pedidos gerados por clientes que usam um determinado cupom.

### Receita média da vida útil

Essa métrica ajuda a avaliar a fidelidade e a receita média geradas pelos clientes que usam um determinado cupom. Ao avaliar se os clientes que usam cupons têm valor maior que outros, considere o número de pedidos que cada cupom foi usado para garantir que você tenha um tamanho de amostra significativo.

Agora, vamos ver um exemplo envolvendo três cupons diferentes usados para a primeira ordem dos clientes:

| **Cupom** | **Pedidos pela primeira vez (FTO)** | **Receitas brutas provenientes da FTO** | **Descontos aplicados à FTO** | **Receitas líquidas provenientes da FTO** | **Valor médio de pedido para FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% de desconto em US$ 100 ou mais** | 56º | 8.531,04 $ | US$ 2.132,76 | US$ 6.398,28 | US$152,34 |
| **US$ 10 de desconto** | 87 | US$ 3.707,07 | US$ 426,10 | US$ 3.280,97 | US$ 42,61 |
| **20% de desconto** | 145 | US$ 10.975,05 | US$ 2.195,01 | 8.780,04 $ | 75,69 $ |

{style=&quot;table-layout:auto&quot;}

O que podemos tirar disso? Primeiro, o cupom de &quot;20% de desconto&quot; tinha o maior número de pedidos pela primeira vez. No entanto, o número de ordens associadas a cada cupom pode variar com base em vários fatores, incluindo:

* a quantidade de anúncios para cada cupom.
* a duração da oferta dos cupões.
* a hora do dia/semana/mês/ano em que os cupons foram oferecidos.
* a temporada dos cupons foi oferecida, dependendo do negócio.

   **Exemplo:** o cupom de &quot;20% de desconto&quot; foi oferecido durante os meses de verão, mas a empresa vende roupas de inverno.
* as restrições aos cupons.

   **Exemplo:** o cupom de &quot;10% de desconto&quot; é oferecido apenas para clientes que compram um casaco de inverno no mesmo pedido.

O **receita bruta** para o cupom &quot;25% de desconto de US$ 100 ou mais&quot; é muito superior à receita bruta do cupom &quot;$10 de desconto&quot;. No entanto, o cupom &quot;$10 off&quot; tem um valor muito maior **número de ordens**. Análise do **valor médio de pedido** fornece informações sobre essas diferenças: mesmo que o cupom &quot;25% de desconto de US$ 100 ou mais&quot; tivesse menos número de pedidos, o valor médio de pedido é mais do triplo do cupom &quot;$10 de desconto&quot;. Assim, uma receita bruta maior é atribuída ao cupom &quot;25% de US$ 100 ou mais&quot;.

O **descontos** e **receita líquida** para os cupons &quot;25% de desconto de US$ 100 ou mais&quot; e &quot;20% de desconto&quot; têm valor próximo. Embora o valor médio de pedido de &quot;25% de desconto de US$ 100 ou mais&quot; seja próximo do dobro do valor médio de pedido de &quot;20% de desconto&quot;, o último cupom tem pouco menos do triplo do número de pedidos.

## Atributos de clientes que usam cupons em sua primeira ordem {#attributes}

Agora que olhamos para as próprias ordens, vamos dar uma olhada nos clientes que usam cupons em suas primeiras ordens:

| **Cupom do primeiro pedido do cliente** | **Número de clientes** | **Número médio de ordens por vida** | **Receita média da vida útil** |
|-----|-----|-----|-----|
| **25% de desconto em US$ 100 ou mais** | 56º | 2,8 | US$ 554,54 |
| **US$ 10 de desconto** | 87 | 1,9 | US$ 115,50 |
| **20% de desconto** | 145 | 1,3 | US$ 103,75 |

{style=&quot;table-layout:auto&quot;}

você observará que o número de pedidos pela primeira vez é o mesmo que o número de clientes para cada cupom. Isso faz sentido, pois cada cliente só pode ter um primeiro pedido.

O maior número de clientes foi adquirido através do cupom de &quot;20% de desconto&quot;. No entanto, esses clientes têm o menor **número médio de ordens** e **receita média da vida útil**; geralmente, a maioria dos clientes adquiridos por cupom não faz pedidos repetidos. Além disso, os clientes adquiridos por meio do drive de cupom de &quot;25% de US$ 100 ou mais&quot; são maiores **número médio de ordens** e, por sua vez, maior **receita média da vida útil**. Geralmente, os usuários que foram adquiridos por meio desse cupom geralmente retornam e fazem compras mais repetidas.

## Quebra de linha {#wrapup}

Há uma variedade de análises que você pode criar para entender melhor como seus clientes usam cupons. Já pensou em analisar como seus clientes usam seus cupons ou o tempo que leva para os cupons serem usados? E quanto a encontrar o valor ideal de desconto - que valor estimula compradores repetidos, valor médio de pedido mais alto e receita vitalícia mais alta? Para obter ajuda com esses tipos de perguntas, [entrar em contato com o suporte](../../guide-overview.md).
