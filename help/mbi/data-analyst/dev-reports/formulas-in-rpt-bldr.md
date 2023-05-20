---
title: Fórmulas no Report Builder
description: Saiba como as fórmulas podem ser usadas no Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Fórmulas na `Report Builder`

No [`Report Builder`](../../tutorials/using-visual-report-builder.md), você pode criar visualizações poderosas usando o [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) em sua conta. A combinação dessas métricas em uma fórmula permite que você lance informações adicionais a partir dos seus dados. Este tópico se aprofunda em como as `Report Builder` fórmulas podem ser usadas no salto-permitir!

## O que é um `formula` ? {#what}

`Report Builder`No, a `formula` é apenas uma combinação de uma ou mais métricas com base em alguma lógica matemática. Um exemplo típico parece curtir isso:

![](../../assets/formula-example.png)

Neste exemplo, você usa um `Number of orders metric (A)` e um `Distinct buyers metric (B)` , e o objetivo é responder a pergunta: Qual é o número médio de pedidos que meus compradores estão fazendo por mês? Os parâmetros da fórmula são:

* `Definition`: Aqui, você aplica matemática nas métricas de entrada. Nesse exemplo, a divisão do número de pedidos pelo número de compradores distintos nos informa o número médio de pedidos. Portanto, a definição é (A/B).

* `Format`: sua fórmula está retornando um número, um período ou um valor de moeda? Ao lado da definição da fórmula há uma lista suspensa, que pode ser usada para especificar o formato do retorno. Nesse caso, é um número.

* `Miscellaneous`: o carimbo de data e hora, os agrupamentos, as perspectivas e os filtros da fórmula são herdados por suas métricas de entrada. Não há nada para fazer aqui!

## Como posso usar `formulas` em meus relatórios? {#how}

Agora que você abordou os fundamentos, veja alguns exemplos.

### Exemplo: desejo descobrir qual porcentagem de minhas receita pode ser atribuída a pedidos de primeira vez.

![Uso de fórmulas para encontrar a porcentagem de receita atribuída a pedidos em primeiro prazo](../../assets/first_time_orders.gif)

Neste exemplo, você usou as `Revenue` métricas e `Revenue (first time orders)` . Ao dividir a `Revenue (first time orders)(B)` métrica pelo `Revenue metric (A)` e definir o formato `Percent` de devolução, você pode encontrar a porcentagem de receita que podem ser atribuídas aos pedidos do primeiro período.

### Exemplo: desejo saber qual é a receita média por solicitar quando faço e não oferta a `promo code` .

![Utilização de fórmulas para localizar a receita média por pedido com e sem códigos promocionais](../../assets/promo_code.gif)

Neste exemplo, você usou o `Revenue` e `Number of orders` métricas. A resposta a esta questão envolve duas etapas - dividir `Revenue (A)` pela `Number of orders (B)` e definição do formato de retorno para `Currency`. Em seguida, você só permitiu o resultado da fórmula (`Avg. Revenue per order`) para mostrar e agrupar os resultados por `Promo code`.

### Exemplo: quero saber a distribuição das fontes de UTM dos novos clientes.

![Utilização de fórmulas para encontrar a distribuição de fontes de UTM de novos clientes](../../assets/distro.gif)

Encontrar a resposta a essa pergunta envolve algumas etapas:

1. Primeiro, você adicionou a `New Customers` métrica e, em seguida, agrupado por `utm_source - all` . Isso é métrica `A` ou `New Customers (grouped)` .

1. Próximo, você duplicau o métrica e o `New Customers (grouped)` define para usar um dimensão independente. Métrica `B` - `New customers (ungrouped)` -mostra o número total de novos clientes.

1. Depois de ocultar ambas as métricas, defina a definição de fórmula como `A/B` . Isso divide o `New customers (grouped)` pelo `New Customers (ungrouped)` .

1. Próximo, você define o formato de resultados como `Percent` .

Neste exemplo, você usou o `Stacked Columns` perspectiva para exibir os resultados por mês. Isso nos permite comparar a distribuição de novos clientes a cada mês.

## Encapsulamento {#wrapup}

Você notou nos exemplos acima que o valor da fórmula `timestamp`, `groupings`, `perspectives`, e `filters` são herdados de suas métricas de entrada? Lembre-se de que as fórmulas podem ser usadas para `perspectives` e [opções de tempo independentes](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, da mesma forma que as métricas podem.

Se você tiver dúvidas adicionais sobre como usar fórmulas no, [ entre em contato com o `Report Builder` suporte ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) .
