---
title: Coluna Calculada de Comparação Sequencial
description: Saiba mais sobre a finalidade e os usos da coluna calculada Comparação sequencial.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/7fCAFSOningY5B-aM8A1w9icX47qjUBsIO47KoRDTDk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 413
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
