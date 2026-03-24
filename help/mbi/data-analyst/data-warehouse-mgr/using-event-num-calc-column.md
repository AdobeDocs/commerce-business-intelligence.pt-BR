---
title: Coluna Calculada do Número do Evento
description: Saiba mais sobre a finalidade e os usos da coluna calculada Número do evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/vLN8AubwPn0Cq0CmmVq4nHbWNjWrCZNBvfhSDsE6lBw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 399
ht-degree: 1%

---

# Coluna Calculada do Número do Evento

Este tópico descreve a finalidade e os usos da coluna calculada `Event Number` disponível na página **[!DNL Manage Data > Data Warehouse]**. Abaixo está uma explicação do que ele faz, seguido por um exemplo, e os mecanismos para criá-lo.

**Explicação**

O tipo de coluna `Event Number` identifica a sequência na qual os eventos ocorreram para um **proprietário do evento** específico, como um `customer` ou `user`. Se você estiver familiarizado com SQL, esse tipo de coluna será idêntico à função `RANK`. Ela pode ser usada para observar diferenças de comportamento entre eventos pela primeira vez, eventos repetidos ou enésimos eventos nos dados.

No caso de um vínculo, esta coluna contém a mesma **classificação** para os eventos vinculados e ignora os números subsequentes. Por exemplo, se estivesse classificando os números 5,8,10,10,12, as posições seriam 1,2,3,3,5.

O caso de uso mais comum desta coluna é analisar compradores pela primeira vez e compradores recorrentes. Os compradores pela primeira vez são identificados ao adicionar um filtro (a uma métrica ou relatório) em `Customer's order number` = 1. `Customer's order number` é uma coluna do tipo `Event Number`.

**Exemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 01-01-2015 00:00:00 | 1 |
| **2 | B | 01-01-2015 00:30:00 | 1 |
| **3 | A | 01-01-2015 02:00:00 | 2 |
| **4 | A | 01-01-2015 13:00:00 | 3 |
| **5 | B | 01-01-2015 13:00:00 | 2 |

No exemplo acima, a coluna `Owner's event number` é uma coluna `Event Number`. Classifica os eventos do proprietário na ordem em que ocorreram (com base na coluna `timestamp`).

Por exemplo, considere todas as linhas em que `owner_id = A`. A primeira linha da tabela é o carimbo de data e hora mais antigo desse proprietário, seguida pela terceira linha da tabela e pela quarta linha da tabela.

**Mecânica**

Estas são algumas instruções sobre como criar uma coluna `Event Number`:

1. Navegue até a página **[!UICONTROL Manage Data > Data Warehouse]**.

1. Navegue até a tabela em que deseja criar essa coluna.

1. Clique em **[!UICONTROL Create a Column]** e escolha o tipo de coluna `EVENT_NUMBER (…)`: na seção `Same Table`.

1. A primeira lista suspensa `Event Owner` especifica a entidade para a qual a classificação deve ser determinada. No caso em que um `Customer's order number`, um identificador de cliente como `customer_id` ou `customer_email` seria o `Event Owner`.

1. A segunda lista suspensa `Event Rank` especifica a coluna que impõe a sequência que determina a classificação da linha. No caso em que um `Customer's order number`, o carimbo de data/hora `created_at` seria `Event Rank`.

1. Na lista suspensa `Options`, é possível adicionar filtros para excluir linhas de serem consideradas. As linhas excluídas têm um valor `NULL` para esta coluna.

1. Forneça um nome para a coluna e clique em **[!UICONTROL Save]**.

1. A coluna está disponível para usar _imediatamente._
