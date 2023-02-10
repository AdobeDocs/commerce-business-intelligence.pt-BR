---
title: Usando a coluna calculada Diferença de data
description: Saiba mais sobre a finalidade e os usos da coluna calculada Diferença de data .
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# Diferença de data da coluna calculada

Este tópico descreve a finalidade e os usos do `Date Difference` coluna calculada disponível na **[!DNL Manage Data > Data Warehouse]** página. Abaixo está uma explicação do que ele faz, seguida de um exemplo, e os mecanismos de criação.

**Explicação**

O `Date Difference` tipo de coluna: encontra o tempo entre dois eventos pertencentes a um único registro, com base nos carimbos de data e hora do evento. O valor bruto calculado nessa coluna é em segundos, mas será convertido automaticamente em minutos, horas, dias e assim por diante para exibição nos relatórios. No entanto, quando usado como filtro/grupo pelo , você desejará usar o valor em segundos.

A `date difference` coluna calculada poderia ser usada para criar uma métrica que calcula o tempo médio ou mediano entre dois eventos, como o tempo médio entre o registro do cliente e seus primeiros pedidos.

**Exemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


No exemplo acima, a variável `Date Difference` é a `Seconds between timestamp_2 and timestamp_1` coluna. Ele executa o cálculo `timestamp_2 minus timestamp_1`.

**Mecânica**

As etapas a seguir descrevem como criar um `Date Difference` coluna.

1. Navegue até o **[!DNL Manage Data > Data Warehouse]** página.
1. Navegue até a tabela na qual deseja criar essa coluna.
1. Clique em **[!UICONTROL Create a Column]** e configure sua coluna da seguinte maneira:
   * Selecionar `Column Definition Type` > `Same Table`
   * Selecionar `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Selecionar `Ending DATETIME` coluna > Escolha o campo datetime final, que normalmente é o evento que ocorre mais tarde
   * Selecionar `Starting DATETIME` column** > Escolha o campo datetime inicial, que normalmente é o evento que ocorre anteriormente

1. Forneça um nome para a coluna e clique em **[!UICONTROL Save]**.
1. A coluna estará disponível para uso *imediatamente*.

Como exemplo, o exemplo a seguir é configurado para calcular a variável `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
