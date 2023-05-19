---
title: Análise do comportamento de recompra do cliente
description: Saiba como analisar o comportamento de recompra do cliente.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 1%

---

# Comportamento de recompra do cliente

Se você oferecer mais de um produto, provavelmente se perguntará como os clientes que compram um produto específico se comportam de forma diferente ao longo do tempo em comparação a outros clientes. Este tópico explora análises que podem ajudá-lo a responder às seguintes perguntas.

Entre os clientes que compram um *item específico*,

* Qual é a probabilidade de eles fazerem outra compra?
* Quanto tempo leva para eles fazerem outra compra?
* Qual é o número médio de pedidos que os clientes fazem a curto/longo prazo?
* Qual é a receita média que os clientes geram no curto/longo prazo?

## Métricas recomendadas

Ao criar análises de atividade de recompra de clientes, o Adobe recomenda usar as seguintes métricas:

### Probabilidade de ordem de repetição

Essa medida é definida como o número total de ordens repetidas, como uma porcentagem do total de ordens. Em outras palavras, essa é a probabilidade de uma ordem ser seguida por outra ordem. Essa medida identifica itens que provavelmente induzirão os clientes a voltar para a loja.

### Número médio de pedidos feitos

Isso expõe o comportamento de compra dos clientes, especificamente quantos pedidos eles fizeram em um determinado período. É possível optar por limitar essa medida para ver o comportamento dos clientes a curto, médio ou longo prazo. Alguns produtos podem incentivar os clientes a fazer compras frequentes a curto prazo, enquanto outros podem influenciar a fidelidade de longo prazo de um cliente. Se esse número for maior para um item em comparação a outros itens, isso sugere que as pessoas que compram esse item são as que retornam à sua loja.

### Receita média vitalícia do cliente

Essa métrica permite entender se os clientes que compram itens específicos são mais valiosos ao longo da vida útil. Se esse número for maior para um item em comparação a outros itens com preços semelhantes, isso sugere que seus clientes de valor mais alto tendem a comprar esse item.

### Tempo até a próxima ordem

Essa medida mostra a frequência de pedidos do cliente ou o tempo necessário para que o cliente faça o pedido novamente. Se o tempo para o próximo pedido for menor para um item em comparação a outros itens, isso sugere que as pessoas que compram esse item tendem a voltar mais cedo.

## Exemplo de hoje: produtos de café

Considerando as métricas acima, veja um exemplo que envolve produtos para café.

| **Nome do produto** | **Probabilidade de ordem de repetição** | **Número médio de ordens vitalícias** | **Receita vitalícia média** | **Tempo médio para a próxima ordem** |
|-----|-----|-----|-----|-----|
| Cervejeira de café de xícara única | 94.98% | 7.92 | $549.82 | 57,01 dias |
| Cápsulas de café | 93.82% | 8.68 | $479.98 | 63,48 dias |
| Grãos de café | 41.92% | 6.07 | $99.82 | 27,31 dias |

{style="table-layout:auto"}

Agora que você tem seus dados, o que isso significa para cada uma de suas métricas?

### Probabilidade de ordem de repetição

Neste exemplo, a probabilidade de ordem repetida - ou a probabilidade de que uma ordem seja seguida por outra ordem - é muito maior para as cervejeiras de café de xícara única e cápsulas de café do que para os grãos de café.

Uma vez que os clientes que compram o cervejeiro estão &quot;comprometidos&quot; em comprar as cápsulas associadas a partir de agora, isso faz sentido. Da mesma forma, os clientes que compraram cápsulas têm uma cervejaria compatível com as cápsulas. No entanto, os grãos de café não são específicos de qualquer cervejeira em particular.

### Número médio de ordens vitalícias

Com base nos dados acima, você pode ver que as pessoas que compram a cervejaria ou cápsulas fizeram mais compras em sua vida, em média, em comparação com os clientes que compraram grãos de café.

### Receita média vitalícia do cliente

Os clientes que compram a cervejeira têm a maior receita média ao longo da vida útil, o que faz sentido, dado que o custo da cervejeira está incluído nesta medida. Por outro lado, os clientes que compram grãos de café normalmente só compram itens de baixo custo.

### Tempo até a próxima ordem

Entre os clientes que compraram cápsulas de café, metade faz um pedido repetido em cerca de dois meses. No entanto, entre os clientes que compraram grãos de café, metade faz um pedido repetido em cerca de um mês. Isso pode ocorrer porque as pessoas que pedem cápsulas (1) não bebem tanto café ou (2) fazem pedidos a granel (por exemplo, compram café equivalente a dois meses em uma única encomenda).

## Que outras análises posso fazer?

Usando as métricas descritas neste tópico, você também pode criar outras análises úteis de recompra. Por exemplo, você também pode ver como os clientes compram novamente **o mesmo item** - por exemplo, se compram recheios regularmente. Cápsulas e grãos de café podem ser recomprados regularmente, mas seria inesperado ver clientes fazendo compras repetidas da cervejaria de café. Se sua empresa se concentrar em recarregamentos ou reabastecimento, essa análise será útil.

Além de analisar o comportamento de recompra dos clientes, você também pode criar análises que analisam a fidelidade do cliente. Considere analisar os padrões de churn do cliente - de onde seus clientes estão saindo do site e não voltando? Em que ritmo isso ocorre?

Depois de identificar por que o abandono está acontecendo, você pode usar sua análise para criar um `reactivation` campanha. Usando esses dados, você pode identificar os usuários que se tornaram inativos, quanto tempo passou desde a última visita, qual foi a última compra e assim por diante. Isso permite tomar decisões acionáveis que motivam seus clientes a voltar.

Para obter ajuda com a análise, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
