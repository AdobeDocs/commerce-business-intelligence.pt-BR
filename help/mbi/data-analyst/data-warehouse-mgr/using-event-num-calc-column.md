---
title: Coluna Calculada do Número do Evento
description: Saiba mais sobre a finalidade e os usos da coluna calculada Número do evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# Coluna Calculada do Número do Evento

Este tópico descreve o objetivo e os usos da `Event Number` coluna calculada disponível no **[!DNL Manage Data > Data Warehouse]** página. Abaixo está uma explicação do que ele faz, seguido por um exemplo, e os mecanismos para criá-lo.

**Explicação**

A variável `Event Number` tipo de coluna: identifica a sequência na qual os eventos ocorreram para uma determinada **proprietário do evento**, como um `customer` ou `user`. Se você estiver familiarizado com SQL, esse tipo de coluna será idêntico ao `RANK` função. Ela pode ser usada para observar diferenças de comportamento entre eventos pela primeira vez, eventos repetidos ou enésimos eventos nos dados.

No caso de um vínculo, essa coluna contém o mesmo **classificação** para os eventos vinculados e ignora os números subsequentes. Por exemplo, se estivesse classificando os números 5,8,10,10,12, as posições seriam 1,2,3,3,5.

O caso de uso mais comum desta coluna é analisar compradores pela primeira vez e compradores recorrentes. Os compradores pela primeira vez são identificados adicionando um filtro (a uma métrica ou relatório) em `Customer's order number` = 1. `Customer's order number` é uma coluna do tipo `Event Number`.

**Exemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

No exemplo acima, a coluna `Owner's event number` é um `Event Number` coluna. Classifica os eventos do proprietário na ordem em que ocorreram (com base na `timestamp` coluna).

Por exemplo, considere todas as linhas em que `owner_id = A`. A primeira linha da tabela é o carimbo de data e hora mais antigo desse proprietário, seguida pela terceira linha da tabela e pela quarta linha da tabela.

**Mecânica**

Estas são algumas instruções sobre como criar uma `Event Number` coluna:

1. Navegue até a **[!UICONTROL Manage Data > Data Warehouse]** página.
1. Navegue até a tabela em que deseja criar essa coluna.
1. Clique em **[!UICONTROL Create a Column]** e escolha o `EVENT_NUMBER (…)` tipo de coluna: no campo `Same Table` seção.
1. A primeira lista suspensa `Event Owner` especifica a entidade para a qual a classificação deve ser determinada. No caso de uma `Customer's order number`, um identificador do cliente, como `customer_id` ou `customer_email` seria o `Event Owner`.
1. A segunda lista suspensa `Event Rank` especifica a coluna que impõe a sequência que determina a classificação da linha. No caso de uma `Customer's order number`, o `created_at` o carimbo de data e hora seria o `Event Rank`.
1. No `Options` , é possível adicionar filtros para excluir linhas de serem consideradas. As linhas excluídas têm um `NULL` para esta coluna.
1. Forneça um nome para a coluna e clique em **[!UICONTROL Save]**.
1. A coluna está disponível para uso _imediatamente._
