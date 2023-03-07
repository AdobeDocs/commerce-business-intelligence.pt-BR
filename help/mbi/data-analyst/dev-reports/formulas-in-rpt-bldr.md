---
title: Fórmulas no Report Builder
description: Saiba como as fórmulas podem ser usadas no Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Fórmulas na `Report Builder`

No [`Report Builder`](../../tutorials/using-visual-report-builder.md), você pode criar visualizações poderosas usando o [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) em sua conta. Combinar essas métricas em uma fórmula permite obter mais insights dos seus dados. Este artigo aborda como as fórmulas podem ser usadas na `Report Builder` - Vamos entrar!

## O que é uma `formula`? {#what}

No `Report Builder`, um `formula` é apenas uma combinação de uma ou mais métricas baseadas em alguma lógica matemática. Um exemplo típico tem esta aparência:

![](../../assets/formula-example.png)

Neste exemplo, você usa um `Number of orders metric (A)` e uma `Distinct buyers metric (B)`, e o objetivo é responder à pergunta: qual é o número médio de pedidos que meus compradores estão fazendo a cada mês? Os parâmetros da fórmula são:

* `Definition`: aqui, você aplica matemática às métricas de entrada. Neste exemplo, dividir o número de pedidos pelo número de compradores distintos nos diz o número médio de pedidos. Portanto, a definição é (A/B).

* `Format`: sua fórmula está retornando um número, um período ou um valor de moeda? Ao lado da definição da fórmula há uma lista suspensa, que pode ser usada para especificar o formato do retorno. Nesse caso, é um número.

* `Miscellaneous`: o carimbo de data e hora, os agrupamentos, as perspectivas e os filtros da fórmula são herdados por suas métricas de entrada. Não há nada para fazer aqui!

## Como posso usar `formulas` nos meus relatórios? {#how}

Agora que já abordou as noções básicas, veja alguns exemplos.

### Exemplo: quero descobrir qual porcentagem da minha receita pode ser atribuída a pedidos iniciais.

![Uso de fórmulas para localizar o percentual de receita atribuído a pedidos pela primeira vez](../../assets/first_time_orders.gif)

Neste exemplo, você usou o `Revenue` e `Revenue (first time orders)` métricas. Ao dividir as `Revenue (first time orders)(B)` métrica por `Revenue metric (A)` e definição do formato de retorno para `Percent`, você pode encontrar a porcentagem de receita que pode ser atribuída aos pedidos iniciais.

### Exemplo: quero saber qual é a receita média por pedido quando faço e não ofereço um `promo code`.

![Utilização de fórmulas para localizar a receita média por pedido com e sem códigos promocionais](../../assets/promo_code.gif)

Neste exemplo, você usou o `Revenue` e `Number of orders` métricas. A resposta a esta questão envolve duas etapas - dividir `Revenue (A)` pela `Number of orders (B)` e definição do formato de retorno para `Currency`. Em seguida, você só permitiu o resultado da fórmula (`Avg. Revenue per order`) para mostrar e agrupar os resultados por `Promo code`.

### Exemplo: quero saber a distribuição das fontes de UTM dos novos clientes.

![Utilização de fórmulas para encontrar a distribuição de fontes de UTM de novos clientes](../../assets/distro.gif)

A resposta para essa pergunta envolve algumas etapas:

1. Primeiro, você adicionou o `New Customers` e, em seguida, agrupada por `utm_source - all`. Esta é a métrica `A`ou `New Customers (grouped)`.

1. Em seguida, você duplicou o `New Customers (grouped)` e defina-a para usar uma dimensão independente. Métrica `B` - `New customers (ungrouped)` - mostra o número total de novos clientes.

1. Depois de ocultar as duas métricas, defina a definição da fórmula como `A/B`. Isso divide a `New customers (grouped)` pela `New Customers (ungrouped)`.

1. Em seguida, defina o formato dos resultados como `Percent`.

Neste exemplo, você usou o `Stacked Columns` perspectiva para exibir os resultados por mês. Isso nos permite comparar a distribuição de novos clientes a cada mês.

## Encapsulamento {#wrapup}

Você notou nos exemplos acima que o valor da fórmula `timestamp`, `groupings`, `perspectives`, e `filters` são herdados de suas métricas de entrada? Lembre-se de que as fórmulas podem ser usadas para `perspectives` e [opções de tempo independentes](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, da mesma forma que as métricas podem.

Se você tiver dúvidas adicionais sobre o uso de fórmulas no `Report Builder`, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
