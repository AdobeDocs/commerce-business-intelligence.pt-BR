---
title: Análise de coorte de receita vitalícia
description: Explore o potencial da análise de coorte de inteligência do Commerce.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# [!DNL Lifetime Revenue Cohort] Análise

Há várias maneiras de examinar seus dados no [!DNL Adobe Commerce Intelligence], e você sabe que interpretação e compreensão são tão importantes quanto cálculo e visualização. Este tópico explora o poder do [!DNL Commerce Intelligence] `cohort` análise.

## O que faz `lifetime revenue cohort` meio de análise?

O gráfico abaixo mostra os gastos cumulativos por usuário por um período de tempo após a aquisição. `Cohorts` de usuários são divididos pelo mês de aquisição.

Por exemplo, a linha laranja acima mostra a média para usuários que foram adquiridos em novembro de 2011. O primeiro ponto de dados significa que, no primeiro mês, os usuários adquiridos em novembro gastaram uma média de cerca de `$200`. O segundo ponto de dados significa que, no final do segundo mês, esses usuários gastaram uma média de cerca de `$240`. A despesa média no segundo mês foi de aproximadamente `$40 (240 - 200)`. As diferentes linhas representam diferentes coortes de usuários. A linha verde representa os usuários que foram adquiridos em dezembro e a azul representa os usuários que foram adquiridos em outubro.

## Por que isso é importante?

Esse tipo de `cohort` a análise pode ser útil para várias finalidades diferentes, mas o benefício mais imediato geralmente é a adoção de melhores decisões de aquisição de clientes. Muitas empresas limitam seus gastos de marketing a canais que rendem lucratividade na primeira compra de um cliente. Essas empresas pagam para adquirir clientes por meio de um determinado canal, desde que sua primeira compra média gere mais `gross margin` que custa adquiri-los.

O problema com essa abordagem é que muitas vezes resulta em um subinvestimento em crescimento. Se seus concorrentes fazem marketing com base em uma compreensão mais profunda do comportamento de compra, eles superam você. A variável `lifetime revenue cohort` A análise ajuda a entender as consequências da expansão dos gastos com aquisição de clientes e fornece uma maneira fácil de transmitir isso ao restante da equipe. Se os clientes futuros se comportarem como clientes existentes, a aquisição de clientes por um CPA mais alto resultará em um período de retorno previsível. Dependendo da posição de caixa da empresa, você pode definir com qual período de retorno você se sente confortável, encontrar a vaga relevante no gráfico e gastar de acordo.

Além disso, você pode usar essa análise para ver se está melhorando na integração, no envolvimento e na geração de receita com os usuários que adquiriu. Por exemplo, isso `cohort` a análise é uma ótima maneira de ver se uma promoção de frete gratuito para novos usuários resultou em compradores recorrentes ou compradores únicos que nunca retornam.

## Como isso varia de acordo com os diferentes modelos de negócios?

Para a maioria das empresas, a `lifetime revenue cohort` o gráfico de análise mostrará uma grande quantidade de gastos no período inicial e aumentará mais lentamente ao longo do tempo. Esse pico inicial se deve ao fato de que os clientes têm mais probabilidade de fazer sua primeira compra logo após a aquisição do que em qualquer outro momento. Nos casos em que o evento de aquisição em si é uma compra, 100% dos clientes fazem uma compra em seu primeiro período. Nos casos em que o registro pode ocorrer antes das compras, esse efeito é menos drástico.

Como exemplo, [!DNL Groupon] provavelmente teria um salto inicial muito menor do que [!DNL Amazon], pois muitas das pessoas que se inscrevem no [!DNL Groupon] não faça uma compra imediatamente. A menos que haja um número alto de reembolsos, esse gráfico inclinará para cima e para a direita após o salto inicial. A taxa de crescimento tende a diminuir com o tempo, pois os clientes estão mais ativos quando se inscrevem pela primeira vez. Isso faz com que a média caia porque o número de pessoas no coorte permanece constante, independentemente de quantas voltam para comprar mais. Em empresas de assinatura, a inclinação decairá de forma menos agressiva do que em empresas onde as pessoas fazem compras únicas.

Ocasionalmente, uma empresa de assinatura terá uma inclinação que aumenta com o tempo. É raro ver isso, mas é um ótimo sinal para o negócio quando acontece. Isso não significa que não há clientes com churn, mas sim atualizações para clientes que permanecem mais do que compensam os clientes que saem.

## Como isso é calculado?

Há duas entradas simples para esse cálculo: quantos membros estão na variável `cohort` (que nunca muda) e quanta receita esses membros geraram no período determinado. Para determinar os membros na `cohort`, você conta o número de usuários que foram adquiridos no período em questão. Uma aquisição pode ser uma primeira compra, criação de conta, inscrição em boletim informativo ou algum outro evento. A variável `revenue` cálculo é um pouco mais complicado. Você deseja somar a receita dos pedidos feitos pelos membros desta `cohort` e ocorreu dentro de um período fixo a partir da data de aquisição (por exemplo, os primeiros três meses). Por fim, divida a receita pelo número de membros na `cohort` para cada período no gráfico e adicione esse valor cumulativamente ao longo do tempo.

## Quais são as variações desse gráfico?

Existem muitos tipos diferentes de `cohort` análises. A variação mais comum é [filtragem por origem de aquisição do usuário](../analysis/most-value-source-channel.md). Por exemplo, talvez você queira ver esse gráfico para clientes que vieram de `organic` pesquisa, `paid` ou um programa afiliado. Isso ajuda você a entender se os clientes de uma fonte de aquisição são mais fiéis ou valiosos do que os de outra. Também é possível filtrar por demografia ou outros atributos do usuário.

Outra maneira de observar os dados é com uma perspectiva de dados incremental, em vez de cumulativa. Mostra a quantidade incremental que um usuário médio gasta em cada mês após a aquisição. Isso é útil para prever o número de compras repetidas que você obtém de usuários existentes. Você pode ver isso com outras coisas além da receita também. Alguns exemplos incluem métricas de margem e não financeiras, como convites, votos ou mensagens.
