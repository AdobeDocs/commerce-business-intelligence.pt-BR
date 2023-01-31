---
title: Análise do comportamento de recompra do cliente
description: Saiba como analisar o comportamento de recompra do cliente.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Comportamento de recompra do cliente

Se você oferecer mais de um produto, provavelmente se perguntará como os clientes que compram um produto específico se comportam de forma diferente ao longo do tempo em comparação com outros clientes. Neste artigo, exploramos análises que podem ajudar você a responder as seguintes perguntas:

Entre clientes que compram um *item específico*,

* Qual é a probabilidade de realizar outra compra?
* Quanto tempo levará para que eles façam outra compra?
* Qual é o número médio de pedidos que os clientes fazem a curto/longo prazo?
* Qual é a receita média que os clientes geram a curto/longo prazo?

## Métricas recomendadas

Ao criar análises de atividade de recompra do cliente, recomendamos usar as seguintes métricas:

### Probabilidade de ordem repetida

Essa medida é definida como o número total de pedidos repetidos, como uma porcentagem do total de pedidos. Em outras palavras, essa é a probabilidade de um pedido ser seguido por outro pedido. Essa medida identifica itens que provavelmente induzirão os clientes a retornar à sua loja.

### Número médio de pedidos colocados

Isso expõe o comportamento de compra de seus clientes, especificamente quantos pedidos seus clientes fizeram em um determinado período. É possível optar por limitar essa medida para ver o comportamento dos clientes a curto, médio ou longo prazo. Alguns produtos podem incentivar os clientes a fazer compras frequentes a curto prazo, enquanto outros podem influenciar a fidelidade de um cliente a longo prazo. Se esse número for maior para um item em comparação a outros itens, isso sugeriria que as pessoas que compram esse item são aquelas que voltam à sua loja.

### Receita média do tempo de vida do cliente

Essa métrica permite entender se os clientes que compram itens específicos são mais valiosos ao longo da vida. Se esse número for maior para um item em comparação a outros itens com preços semelhantes, isso sugeriria que seus clientes de maior valor tendem a comprar esse item.

### Hora da próxima ordem

Essa medida mostra a frequência de pedido do cliente ou o tempo que leva para o cliente fazer o pedido novamente. Se o tempo até o próximo pedido for menor para um item em comparação a outros itens, isso sugeriria que as pessoas que compraram este item tendem a voltar mais cedo.

## Exemplo de hoje: produtos de café

Lembrando as métricas acima, vamos observar um exemplo envolvendo produtos de café.

| **Nome do produto** | **Probabilidade de ordem repetida** | **Número médio de ordens por vida** | **Receita vitalícia média** | **Tempo médio para a ordem seguinte** |
|-----|-----|-----|-----|-----|
| Derramador de café de xícara única | 94,98% | 7,92 | US$ 549,82 | 57,01 dias |
| Cápsulas de café | 93,82% | 8,68 | US$ 479,98 | 63,48 dias |
| Feijão | 41,92% | 6,07 | 99,82 $ | 27,31 dias |

{style=&quot;table-layout:auto&quot;}

Agora que temos nossos dados, vamos dar uma olhada no que isso pode significar para cada uma de nossas métricas.

### Probabilidade de ordem repetida

Neste exemplo, a probabilidade de repetição de pedidos - ou a probabilidade de um pedido ser seguido por outro pedido - é muito maior para os cafeeiros e cápsulas de café de uma xícara do que para os cafés.

Como os clientes que compram o cervejeiro estão &quot;comprometidos&quot; com a compra das cápsulas associadas no futuro, isso faz sentido. Da mesma forma, os clientes que compraram cápsulas têm um copo compatível com as cápsulas. No entanto, os grãos de café não são específicos de nenhum produtor específico.

### Número médio de ordens por vida

Com base nos dados acima, podemos ver que as pessoas que compram o produtor ou cápsulas fizeram mais compras em sua vida, em média, em comparação com os clientes que compraram grãos de café.

### Receita média do tempo de vida do cliente

Os clientes que compram o produtor têm a maior receita média vitalícia; que faz sentido, dado que o custo do produtor está incluído nesta medida. Por outro lado, os clientes que compram cafés normalmente só compram itens de baixo custo.

### Hora da próxima ordem

Entre os clientes que compraram cápsulas de café, metade faz um pedido repetido em cerca de 2 meses. No entanto, entre os clientes que compraram grãos de café, metade faz um pedido repetido em cerca de 1 mês. Isso pode ocorrer porque as pessoas que pedem cápsulas (1) não tomam tanto café ou (2) fazem pedidos em massa (por exemplo, comprando 2 meses de café em uma ordem).

## Quais outras análises posso criar?

Usando as métricas descritas neste artigo, também é possível criar outras análises úteis de recompra. Por exemplo, também podemos ver como os clientes fazem recompras **o mesmo item** - por exemplo, se comprarem recargas regularmente. As cápsulas e os grãos de café podem ser recomprados regularmente, mas seria inesperado que os clientes fizessem compras repetidas do cafeeiro. Se sua empresa estiver focada em recargas ou repovoamento, essa análise será extremamente útil.

Além de analisar o comportamento de recompra dos clientes, você também pode criar análises que analisem a fidelidade dos clientes. Considere analisar os padrões na rotatividade do cliente - onde os clientes estão saindo do site e não voltando? A que ritmo isto ocorre?

Depois de identificar por que o churn está acontecendo, você pode usar a análise para criar um `reactivation` campanha. Com esses dados, você pode identificar os usuários que ficaram inativos, quanto tempo passou desde a última visita, qual foi a última compra e assim por diante. Isso permitirá que você tome decisões acionáveis que levarão seus clientes a retornarem.

Para obter ajuda com a análise, [entrar em contato com o suporte](../../guide-overview.md).
