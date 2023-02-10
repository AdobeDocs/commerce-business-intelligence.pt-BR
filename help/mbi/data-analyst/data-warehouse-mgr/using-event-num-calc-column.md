---
title: Coluna Calculada do Número do Evento
description: Saiba o propósito e os usos da coluna calculada Número de evento .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Coluna Calculada do Número do Evento

Este tópico descreve a finalidade e os usos do `Event Number` coluna calculada disponível na **[!DNL Manage Data > Data Warehouse]** página. Abaixo está uma explicação do que ele faz, seguida de um exemplo, e os mecanismos de criação.

**Explicação**

O `Event Number` tipo de coluna: identifica a sequência em que os eventos ocorreram para um determinado **proprietário do evento** como um `customer` ou `user`. Se você estiver familiarizado com o SQL, esse tipo de coluna será idêntico ao `RANK` . Ela pode ser usada para observar diferenças de comportamento entre eventos de primeira hora, eventos de repetição ou eventos de enésima nos dados.

No caso de vínculos, essa coluna contém o mesmo **classificação** para os eventos vinculados e ignora os números subsequentes. Por exemplo, se estivesse classificando os números 5,8,10,10,12, as fileiras seriam 1,2,3,3,5.

O caso de uso mais comum dessa coluna é analisar compradores pela primeira vez e compradores repetidos. A primeira vez que compradores são identificados adicionando um filtro (para uma métrica ou relatório) em `Customer's order number` = 1. `Customer's order number` é uma coluna do tipo `Event Number`.

**Exemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

No exemplo acima, a coluna `Owner's event number` é um `Event Number` coluna. Ele classifica os eventos do proprietário na ordem em que ocorreram (com base no `timestamp` coluna).

Por exemplo, considere todas as linhas em que `owner_id = A`. A primeira linha da tabela é o primeiro carimbo de data e hora desse proprietário, seguido pela terceira linha da tabela, seguida pela quarta linha da tabela.

**Mecânica**

Estas são algumas instruções para criar uma `Event Number` coluna:

1. Navegue até o **[!UICONTROL Manage Data > Data Warehouse]** página.
1. Navegue até a tabela na qual deseja criar essa coluna.
1. Clique em **[!UICONTROL Create a Column]** e escolha a `EVENT_NUMBER (…)` tipo de coluna: nos termos do `Same Table` seção.
1. A primeira lista suspensa `Event Owner` especifica a entidade para a qual a classificação deve ser determinada. No caso de `Customer's order number`, um identificador do cliente como `customer_id` ou `customer_email` seria o `Event Owner`.
1. A segunda lista suspensa `Event Rank` especifica a coluna que aplica a sequência que determina a classificação da linha. No caso de `Customer's order number`, o `created_at` o carimbo de data e hora seria o `Event Rank`.
1. Em `Options` na lista suspensa, é possível adicionar filtros para excluir linhas da consideração. As linhas excluídas terão um `NULL` para essa coluna.
1. Forneça um nome para a coluna e clique em **[!UICONTROL Save]**.
1. A coluna estará disponível para uso _imediatamente._
