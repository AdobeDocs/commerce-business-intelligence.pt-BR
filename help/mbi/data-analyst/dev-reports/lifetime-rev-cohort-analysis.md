---
title: Análise de coorte de receita vitalícia
description: Explore o potencial da análise de coorte do Commerce Intelligence.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Análise de [!DNL Lifetime Revenue Cohort]

Há várias maneiras de examinar seus dados no [!DNL Adobe Commerce Intelligence], e você sabe que interpretação e compreensão são tão importantes quanto cálculo e visualização. Este tópico explora o poder da análise de [!DNL Commerce Intelligence] `cohort`.

## O que significa a análise de `lifetime revenue cohort`?

O gráfico abaixo mostra os gastos cumulativos por usuário por um período de tempo após a aquisição. `Cohorts` de usuários são divididos por seu mês de aquisição.

Por exemplo, a linha laranja acima mostra a média para usuários que foram adquiridos em novembro de 2011. O primeiro ponto de dados significa que, no primeiro mês, os usuários adquiridos em novembro gastaram uma média de aproximadamente `$200`. O segundo ponto de dados significa que no final do segundo mês, esses usuários tinham gasto uma média de aproximadamente `$240`. A média de gastos no segundo mês foi de aproximadamente `$40 (240 - 200)`. As diferentes linhas representam diferentes coortes de usuários. A linha verde representa os usuários que foram adquiridos em dezembro e a azul representa os usuários que foram adquiridos em outubro.

## Por que isso é importante?

Esse tipo de análise do `cohort` pode ser útil para várias finalidades diferentes, mas o benefício mais imediato geralmente são melhores decisões de aquisição de clientes. Muitas empresas limitam seus gastos de marketing a canais que rendem lucratividade na primeira compra de um cliente. Essas empresas pagam para adquirir clientes por meio de um determinado canal, desde que sua primeira compra média produza mais `gross margin` do que custa adquiri-los.

O problema com essa abordagem é que muitas vezes resulta em um subinvestimento em crescimento. Se seus concorrentes fazem marketing com base em uma compreensão mais profunda do comportamento de compra, eles superam você. A análise do `lifetime revenue cohort` ajuda você a entender as consequências do aumento dos gastos com aquisição de clientes, além de fornecer uma maneira fácil de transmitir isso para o restante da equipe. Se os clientes futuros se comportarem como clientes existentes, a aquisição de clientes por um CPA mais alto resultará em um período de retorno previsível. Dependendo da posição de caixa da empresa, você pode definir com qual período de retorno você se sente confortável, encontrar a vaga relevante no gráfico e gastar de acordo.

Além disso, você pode usar essa análise para ver se está melhorando na integração, no envolvimento e na geração de receita com os usuários que adquiriu. Por exemplo, essa análise `cohort` é uma ótima maneira de ver se uma promoção de frete gratuito para novos usuários resultou em compradores recorrentes ou compradores únicos que nunca retornam.

## Como isso varia de acordo com os diferentes modelos de negócios?

Para a maioria das empresas, o gráfico de análise `lifetime revenue cohort` mostrará uma grande quantidade de gastos no período inicial e aumentará mais lentamente ao longo do tempo. Esse pico inicial se deve ao fato de que os clientes têm mais probabilidade de fazer sua primeira compra logo após a aquisição do que em qualquer outro momento. Nos casos em que o evento de aquisição em si é uma compra, 100% dos clientes fazem uma compra em seu primeiro período. Nos casos em que o registro pode ocorrer antes das compras, esse efeito é menos drástico.

Por exemplo, [!DNL Groupon] provavelmente terá um salto inicial muito menor que [!DNL Amazon], pois muitas das pessoas que se inscrevem no [!DNL Groupon] não fazem uma compra imediatamente. A menos que haja um número alto de reembolsos, esse gráfico inclinará para cima e para a direita após o salto inicial. A taxa de crescimento tende a diminuir com o tempo, pois os clientes estão mais ativos quando se inscrevem pela primeira vez. Isso faz com que a média caia porque o número de pessoas no coorte permanece constante, independentemente de quantas voltam para comprar mais. Em empresas de assinatura, a inclinação decairá de forma menos agressiva do que em empresas onde as pessoas fazem compras únicas.

Ocasionalmente, uma empresa de assinatura terá uma inclinação que aumenta com o tempo. É raro ver isso, mas é um ótimo sinal para o negócio quando acontece. Isso não significa que não há clientes com churn, mas sim atualizações para clientes que permanecem mais do que compensam os clientes que saem.

## Como isso é calculado?

Há duas entradas simples para este cálculo: quantos membros estão em `cohort` (o que nunca muda) e quanta receita esses membros geraram em determinado período. Para determinar os membros no `cohort`, você conta o número de usuários que foram adquiridos no período em questão. Uma aquisição pode ser uma primeira compra, criação de conta, inscrição em boletim informativo ou algum outro evento. O cálculo de `revenue` é um pouco mais complicado. Você deseja somar a receita de pedidos feitos por membros deste `cohort` e que ocorreram em um período fixo a partir da data de aquisição (por exemplo, os primeiros três meses). Finalmente, você divide a receita pelo número de membros no `cohort` para cada período no gráfico e adiciona esse valor cumulativamente ao longo do tempo.

## Quais são as variações desse gráfico?

Há vários tipos diferentes de análises `cohort` úteis. A variação mais comum é a [filtragem por origem de aquisição de usuário](../analysis/most-value-source-channel.md). Por exemplo, talvez você queira ver este gráfico para clientes que vieram da pesquisa de `organic`, da pesquisa de `paid` ou de um programa afiliado. Isso ajuda você a entender se os clientes de uma fonte de aquisição são mais fiéis ou valiosos do que os de outra. Também é possível filtrar por demografia ou outros atributos do usuário.

Outra maneira de observar os dados é com uma perspectiva de dados incremental, em vez de cumulativa. Mostra a quantidade incremental que um usuário médio gasta em cada mês após a aquisição. Isso é útil para prever o número de compras repetidas que você obtém de usuários existentes. Você pode ver isso com outras coisas além da receita também. Alguns exemplos incluem métricas de margem e não financeiras, como convites, votos ou mensagens.
