---
title: Comparação sequencial coluna calculada
description: Saiba mais sobre a finalidade e os usos da coluna calculada Comparação sequencial.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# Comparação sequencial coluna calculada

Este tópico descreve a finalidade e os usos do `Sequential Comparison` coluna calculada disponível na **[!DNL Manage Data > Data Warehouse]** página. Abaixo está uma explicação do que ele faz, seguida de um exemplo, e os mecanismos de criação.

**Explicação**

O `Sequential Comparison` tipo de coluna: encontra a diferença entre eventos consecutivos. O tipo mais comum de `Sequential Comparison` é a `Seconds since previous order` coluna. Há três entradas necessárias para esta coluna:

1. `Event Owner`: Essa entrada determina a entidade para a qual as linhas são agrupadas. Por exemplo, no `Seconds since previous order` , o proprietário do evento é o cliente, pois queremos encontrar o número de segundos desde a ordem anterior do mesmo cliente.
1. `Event Date`: Essa entrada impõe a sequência de eventos. No caso de `Seconds since previous order`, a coluna que contém o carimbo de data e hora da ordem deve ser a `Event Date`. Essa entrada sempre é um carimbo de data e hora.
1. `Value to Compare`: Essa entrada é o valor real a ser comparado. Ele subtrai o valor da linha anterior do valor da linha atual. Assim, uma coluna que localiza a diferença de tempo entre ordens sucessivas de um cliente é chamada `Seconds since previous order`. Essa entrada não precisa ser um carimbo de data e hora. Um exemplo sem carimbo de data e hora é encontrar a diferença no valor da ordem entre pedidos sucessivos de um cliente.

**Exemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

No exemplo acima, `Seconds since owner's previous event` é `Sequential Comparison` coluna calculada. Para o `owner_id = A`, primeiro identifica uma sequência com base no `timestamp` e, em seguida, subtrai o evento anterior `timestamp` no carimbo de data e hora do evento atual. Na terceira linha do quadro - a segunda linha de `owner_id A` - o valor de `Seconds since owner's previous event` é o número de segundos entre &#39;2015-01-01 02:00&#39; e &#39;2015-01-01 00:00:00&#39;. Essa diferença é igual a 2 horas = 7200 segundos.

Para esse tipo de coluna calculada, a linha correspondente ao primeiro evento do proprietário tem um `NULL` valor.

**Mecânica**

Para criar um **Número do evento** coluna:

1. Navegue até o **[!DNL Manage Data** > **Data Warehouse]** página.
1. Navegue até a tabela na qual deseja criar essa coluna.
1. Clique em **[!UICONTROL Create New Column]** na parte superior direita da tela.
1. Selecionar `Same Table` como `Definition Type` (se as colunas que deseja comparar não estiverem na mesma tabela, talvez seja necessário relocá-las).
1. Selecionar `SEQUENTIAL_COMPARISON` como `Column Definition Equation`.
1. Escolha as entradas, conforme explicado acima:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`
1. Filtros também podem ser adicionados para excluir linhas da consideração. As linhas excluídas terão um valor NULL para essa coluna.
1. Forneça um nome para a coluna na parte superior da página e clique em **[!UICONTROL Save]**.
1. A coluna estará disponível para uso *imediatamente*.

![SEC](../../assets/SEC_new.png)
