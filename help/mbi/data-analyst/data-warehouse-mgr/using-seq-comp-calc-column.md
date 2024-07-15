---
title: Coluna Calculada de Comparação Sequencial
description: Saiba mais sobre a finalidade e os usos da coluna calculada Comparação sequencial.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Coluna Calculada de Comparação Sequencial

Este tópico descreve a finalidade e os usos da coluna calculada `Sequential Comparison` disponível na página **[!DNL Manage Data > Data Warehouse]**. Abaixo está uma explicação do que ele faz, seguido por um exemplo e os mecanismos para criá-lo.

**Explicação**

O tipo de coluna `Sequential Comparison`: encontra a diferença entre eventos consecutivos. O tipo mais comum de coluna `Sequential Comparison` é a coluna `Seconds since previous order`. Há três entradas necessárias para esta coluna:

1. `Event Owner`: esta entrada determina a entidade para a qual as linhas são agrupadas. Por exemplo, na coluna `Seconds since previous order`, o proprietário do evento é o cliente, porque você deseja encontrar o número de segundos desde a ordem anterior do mesmo cliente.
1. `Event Date`: esta entrada impõe a sequência de eventos. No caso de `Seconds since previous order`, a coluna contendo o carimbo de data e hora da ordem deve ser `Event Date`. Essa entrada é sempre um carimbo de data e hora.
1. `Value to Compare`: esta entrada é o valor real a ser comparado. Ele subtrai o valor da linha anterior do valor da linha atual. Assim, uma coluna que encontra a diferença de tempo entre pedidos sucessivos de um cliente é chamada `Seconds since previous order`. Essa entrada não precisa ser um carimbo de data e hora. Um exemplo sem carimbo de data e hora é encontrar a diferença no valor do pedido entre pedidos sucessivos de um cliente.

**Exemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 01-01-2015 00:00:00 | NULL |
| **`2`** | B | 01-01-2015 00:30:00 | NULL |
| **`3`** | A | 01-01-2015 02:00:00 | 7200 |
| **`4`** | A | 01-01-2015 13:00:00 | 126000 |
| **`5`** | B | 01-01-2015 13:00:00 | 217800 |

No exemplo acima, `Seconds since owner's previous event` é a coluna calculada `Sequential Comparison`. Para `owner_id = A`, primeiro identifica uma sequência com base na coluna `timestamp` e, em seguida, subtrai a `timestamp` do evento anterior do carimbo de data e hora do evento atual. Na terceira linha da tabela - a segunda linha para `owner_id A` - o valor de `Seconds since owner's previous event` é o número de segundos entre &#39;2015-01-01 02:00&#39; e &#39;2015-01-01 00:00:00&#39;. Essa diferença é igual a duas horas = 7200 segundos.

Para este tipo de coluna calculada, a linha correspondente ao primeiro evento do proprietário tem um valor `NULL`.

**Mecânica**

Para criar uma coluna **Número do Evento**:

1. Navegue até a página **[!DNL Manage Data > Data Warehouse]**.

1. Navegue até a tabela em que deseja criar essa coluna.

1. Clique em **[!UICONTROL Create New Column]** no canto superior direito.

1. Selecione `Same Table` como `Definition Type` (se as colunas que você deseja comparar não estiverem na mesma tabela, talvez seja necessário realocá-las).

1. Selecione `SEQUENTIAL_COMPARISON` como `Column Definition Equation`.

1. Escolha as entradas, conforme explicado acima:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. Também é possível adicionar filtros para excluir linhas de serem consideradas. As linhas excluídas têm um valor `NULL` para esta coluna.

1. Forneça um nome para a coluna na parte superior da página e clique em **[!UICONTROL Save]**.

1. A coluna está disponível para uso *imediatamente*.

![S](../../assets/SEC_new.png)
