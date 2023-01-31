---
title: Análise de coorte de receita vitalícia
description: Explore o poder da [!DNL MBI] análise de coorte.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# `Lifetime Revenue Cohort` Análise

Há muitas maneiras diferentes de analisar seus dados no [!DNL MBI]e sabemos que a interpretação e a compreensão são tão importantes quanto o cálculo e a visualização. Este artigo explorará o potencial da [!DNL MBI] `cohort` análise.

## O que `lifetime revenue cohort` análise?

O gráfico abaixo mostra o gasto cumulativo por usuário por um período de tempo após a aquisição. `Cohorts` de usuários são divididos por seu mês de aquisição.

Por exemplo, a linha laranja acima mostra a média de usuários que foram adquiridos em novembro de 2011. O primeiro ponto de dados significa que, em seu primeiro mês, os usuários adquiridos em novembro passaram uma média de cerca de `$200`. O segundo ponto de dados significa que, no final do segundo mês, esses usuários gastaram uma média de cerca de `$240`. A sua despesa média no segundo mês foi aproximadamente `$40 (240 - 200)`. As diferentes linhas representam coortes diferentes de usuários. A linha verde representa os usuários que foram adquiridos em dezembro, e a azul são os usuários que foram adquiridos em outubro.

## Por que isso é importante?

Esse tipo de `cohort` a análise pode ser útil para vários propósitos diferentes, mas o benefício mais imediato é geralmente melhores decisões de aquisição de clientes. Muitas empresas limitam seus gastos com marketing a canais que geram lucratividade na primeira compra de um cliente. Estas empresas pagarão para adquirir clientes através de um determinado canal, desde que a média da sua primeira compra produza mais `gross margin` do que custa adquirir.

O problema desta abordagem é que resulta frequentemente num subinvestimento no crescimento. Se seus concorrentes estiverem fazendo marketing com base em uma compreensão mais profunda do comportamento de compra, eles vão superar você. O `lifetime revenue cohort` A análise ajuda você a entender as consequências da expansão dos gastos com aquisição de clientes e fornece uma maneira fácil de transmitir isso ao resto da equipe. Se os clientes futuros se comportarem como clientes existentes, a aquisição de clientes para um CPA mais alto resultará em um período de retorno previsível. Dependendo da posição de caixa da empresa, você pode definir com qual período de retorno você está confortável, encontrar o ponto relevante no gráfico e gastar de acordo.

Além disso, você pode usar essa análise para ver se está melhorando na integração, envolvimento e geração de receita dos usuários que adquire.  Por exemplo, este `cohort` a análise é uma ótima maneira de ver se uma promoção de frete grátis para novos usuários resultou em compradores repetidos ou em compradores ocasionais que nunca voltaram.

## Como isso irá variar para diferentes modelos de negócios?

Para a maioria das empresas, a variável `lifetime revenue cohort` o gráfico de análise mostrará uma grande quantidade de gastos no período inicial e, em seguida, aumentará mais lentamente ao longo do tempo. Esse pico inicial deve-se ao fato de os clientes terem maior probabilidade de realizar a sua primeira compra logo após a aquisição do que em qualquer outro momento. Nos casos em que o evento de aquisição é uma compra, 100% dos clientes fazem uma compra no seu primeiro período. Nos casos em que o registro pode ocorrer antes das compras, este efeito é menos drástico.

Como exemplo, [!DNL Groupon] provavelmente teria um salto inicial muito mais baixo do que [!DNL Amazon], porque muitas das pessoas que se inscreveram [!DNL Groupon] não faça uma compra imediatamente. A menos que haja um número alto de reembolsos, esse gráfico será inclinado para cima e para a direita após o salto inicial. A taxa de crescimento tende a diminuir com o tempo, pois os clientes geralmente são mais ativos quando se inscrevem pela primeira vez. Isso faz com que a média diminua porque o número de pessoas na coorte permanece constante, independentemente de quantas retornam para comprar mais. Em empresas de assinatura, a inclinação diminuirá menos agressivamente do que em empresas onde as pessoas fazem compras únicas.

Ocasionalmente, um negócio de assinatura terá, na verdade, uma inclinação que aumenta com o tempo. É raro ver isso, mas é um grande sinal para a empresa quando acontece. Isso não significa que não haja nenhum cliente em andamento, mas sim atualizações para clientes que permanecem mais do que compensam os clientes que saem.

## Como isso é calculado?

Existem duas entradas simples para este cálculo: quantos membros estão na `cohort` (que nunca muda) e a receita que esses membros geraram no período em questão. Para determinar os membros na `cohort`, contamos o número de usuários que foram adquiridos no período em questão. Uma aquisição pode ser uma primeira compra, criação de conta, assinatura de boletim informativo ou algum outro evento. O `revenue` cálculo é um pouco mais complicado. Queremos somar a receita de pedidos que foram colocados por membros deste grupo `cohort` e ter ocorrido num período de tempo fixo a partir da data de aquisição (por exemplo, os três primeiros meses). Por último, dividimos as receitas pelo número de membros no `cohort` para cada período no gráfico e adicione esse valor cumulativamente ao longo do tempo.

## Quais são as variações deste gráfico?

Existem vários tipos diferentes de úteis `cohort` análises.  A variação mais comum é [filtrar por fonte de aquisição de usuário](../analysis/most-value-source-channel.md). Por exemplo, você pode querer ver este gráfico para clientes que vieram de `organic` pesquisar, `paid` pesquisa ou um programa afiliado. Isso ajudará você a entender se os clientes de uma fonte de aquisição são mais leais ou valiosos do que outra. É claro que você também pode filtrar por demografia ou outros atributos do usuário.

Outra maneira de observar os dados é com uma perspectiva de dados incremental, em vez de cumulativa.  Isso mostra o valor incremental que um usuário médio gasta em cada mês após a aquisição.  Isso é útil para prever a quantidade de compras repetidas que você obterá dos usuários existentes. Podemos olhar para isso com outras coisas além de receita também. Alguns exemplos incluem margem e métricas não financeiras como convites, votos ou mensagens.
