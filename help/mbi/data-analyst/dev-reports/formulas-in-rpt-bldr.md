---
title: Fórmulas na Report Builder
description: Saiba como as fórmulas podem ser usadas no Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Fórmulas na `Report Builder`

No [`Report Builder`](../../tutorials/using-visual-report-builder.md), você pode criar visualizações avançadas usando o [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) na sua conta. Combinar essas métricas em uma fórmula permite obter insights adicionais dos seus dados. Neste artigo, aprofundamos em como as fórmulas podem ser usadas na variável `Report Builder` - vamos entrar!

## O que é um `formula`? {#what}

No `Report Builder`, a `formula` é apenas uma combinação de uma ou mais métricas com base em alguma lógica matemática. Um exemplo típico tem esta aparência:

![](../../assets/formula-example.png)

Neste exemplo, estamos usando um `Number of orders metric (A)` e `Distinct buyers metric (B)`e nosso objetivo é responder a pergunta: qual é o número médio de pedidos que meus compradores fazem por mês? Os parâmetros da fórmula são:

* `Definition`: Aqui, você aplica a matemática nas métricas de entrada. Neste exemplo, dividir o número de ordens pelo número de compradores distintos indicar-nos-á o número médio de ordens. Portanto, a definição é (A/B).

* `Format`: Sua fórmula retorna um número, um período ou um valor monetário? Ao lado da definição da fórmula, há uma lista suspensa que pode ser usada para especificar o formato do retorno. Nesse caso, é um número.

* `Miscellaneous`: O carimbo de data e hora, os agrupamentos, as perspectivas e os filtros da fórmula são herdados pelas métricas de entrada. Não há nada a fazer aqui!

## Como posso usar `formulas` nos meus relatórios? {#how}

Agora que cobrimos as noções básicas, vamos dar uma olhada em alguns exemplos.

### Exemplo: Quero descobrir qual porcentagem da minha receita pode ser atribuída aos pedidos pela primeira vez.

![Uso de fórmulas para encontrar a porcentagem da receita atribuída aos pedidos pela primeira vez](../../assets/first_time_orders.gif)

Neste exemplo, usamos a variável `Revenue` e `Revenue (first time orders)` métricas. Dividindo o `Revenue (first time orders)(B)` por `Revenue metric (A)` e definir o formato de retorno como `Percent`, podemos encontrar a porcentagem da receita que pode ser atribuída aos primeiros pedidos.

### Exemplo: Quero saber qual é a receita média por pedido quando eu faço e não ofereço uma `promo code`.

![Uso de fórmulas para encontrar a receita média por pedido com e sem códigos promocionais](../../assets/promo_code.gif)

Neste exemplo, usamos a variável `Revenue` e `Number of orders` métricas. A resposta a essa pergunta envolve duas etapas - divisão `Revenue (A)` pela `Number of orders (B)` e definir o formato de retorno como `Currency`. Em seguida, permitimos apenas o resultado da fórmula (`Avg. Revenue per order`) para mostrar e agrupar os resultados por `Promo code`.

### Exemplo: Quero saber a distribuição das fontes de UTM dos meus novos clientes.

![Usar fórmulas para encontrar a distribuição das fontes de UTM de novos clientes](../../assets/distro.gif)

Encontrar a resposta para essa pergunta envolve algumas etapas:

1. Primeiro adicionamos o `New Customers` e, em seguida, agrupadas por `utm_source - all`. Esta é a métrica `A`ou `New Customers (grouped)`.

1. Em seguida, duplicamos a variável `New Customers (grouped)` e defina-a para usar uma dimensão independente. Métrica `B` - `New customers (ungrouped)` - mostra o número total de novos clientes.

1. Depois de ocultar ambas as métricas, definimos a definição da fórmula como `A/B`. Isso divide o `New customers (grouped)` pela `New Customers (ungrouped)`.

1. Em seguida, definimos o formato dos resultados como `Percent`.

Em nosso exemplo, usamos o `Stacked Columns` para exibir os resultados por mês. Isso nos permite comparar a distribuição de novos clientes mensalmente.

## Quebra de linha {#wrapup}

Você notou nos exemplos acima que a fórmula `timestamp`, `groupings`, `perspectives`e `filters` são herdadas de suas métricas de entrada? Lembre-se de que as fórmulas podem ser aproveitadas para usar `perspectives` e [opções de hora independente](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, assim como as métricas podem.

Se tiver dúvidas adicionais sobre o uso de fórmulas na `Report Builder`, [entrar em contato com o suporte](../../guide-overview.md).
