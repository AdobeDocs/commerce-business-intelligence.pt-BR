---
title: Usando a Coluna Calculada de Diferença de Data
description: Saiba mais sobre a finalidade e os usos da coluna calculada Diferença de datas.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# Coluna Calculada de Diferença de Data

Este tópico descreve o objetivo e os usos da `Date Difference` coluna calculada disponível no **[!DNL Manage Data > Data Warehouse]** página. Abaixo está uma explicação do que ele faz, seguido por um exemplo, e os mecanismos para criá-lo.

**Explicação**

A variável `Date Difference` o tipo de coluna calcula o tempo entre dois eventos pertencentes a um único registro, com base nos carimbos de data e hora do evento. O valor bruto calculado nessa coluna está em segundos, mas é convertido automaticamente em minutos, horas, dias e assim por diante, para exibição em relatórios. No entanto, quando usado como um filtro/grupo por, você deseja usar o valor em segundos.

A `date difference` a coluna calculada pode ser usada para criar uma métrica que calcula o tempo médio ou mediano entre dois eventos, como o tempo médio entre o registro do cliente e seus primeiros pedidos.

**Exemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


No exemplo acima, a variável `Date Difference` coluna é a `Seconds between timestamp_2 and timestamp_1` coluna. Ele executa o cálculo `timestamp_2 minus timestamp_1`.

**Mecânica**

As etapas a seguir descrevem como criar uma `Date Difference` coluna.

1. Navegue até a **[!DNL Manage Data > Data Warehouse]** página.
1. Navegue até a tabela em que deseja criar essa coluna.
1. Clique em **[!UICONTROL Create a Column]** e configure sua coluna da seguinte maneira:
   * Selecionar `Column Definition Type` > `Same Table`
   * Selecionar `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Selecionar `Ending DATETIME` coluna > Escolha o campo de data e hora de término, que normalmente é o evento que ocorre mais tarde
   * Selecionar `Starting DATETIME` coluna** > Escolha o campo de data e hora inicial, que normalmente é o evento que ocorre mais cedo

1. Forneça um nome para a coluna e clique em **[!UICONTROL Save]**.
1. A coluna está disponível para uso *imediatamente*.

Como exemplo, o exemplo a seguir é configurado para calcular o `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
