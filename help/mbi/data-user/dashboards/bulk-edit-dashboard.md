---
title: Gráficos de edição em massa nos painéis
description: Saiba como usar o recurso de edição em massa no [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 260
ht-degree: 0%

---

# Gráficos de edição em massa nos painéis

O recurso de edição em massa facilita a alteração de nomes e datas de gráficos em seus painéis. Por exemplo, você deseja que todos os gráficos em um painel específico se refiram a um único armazenamento e relatório mensalmente em vez de trimestralmente. Em vez de alterar tudo manualmente, deixe o recurso `bulk-editing` funcionar. Neste tópico, você aprenderá a usar:

* [O Recurso  [!DNL Find/Replace] &#x200B;](#findreplace)

* [O Recurso  [!DNL Prepend Name] &#x200B;](#prepend)

* [O Recurso  [!DNL Change Dates] &#x200B;](#dates)

Dito isto, considere isto: *Estas alterações precisam ser permanentes?* Caso contrário, considere clonar o painel e alterar as datas no novo painel. Isso permite preservar o painel original e, ao mesmo tempo, fazer as alterações necessárias.

>[!NOTE]
>
>Se você estiver alterando vários relatórios, o processo de atualização pode demorar um pouco.

## Usando o [!DNL Find/Replace] {#findreplace}

1. Clique no ícone de engrenagem (![ícone de engrenagem](../../assets/gear-icon.png)) ao lado do nome do painel e, em seguida, na janela [!UICONTROL Bulk Edit Reports].

1. Clique em **[!UICONTROL Chart Title Find and Replace]** na janela pop-up.

1. No campo `Chart Title Find`, digite as palavras ou os caracteres que deseja localizar.

1. No campo `Replace With`, digite as palavras ou os caracteres que devem substituir o que está no campo `Find`.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![edição em massa](../../assets/bulk_edit.gif)

## Precedendo `Chart Names` {#prepend}

1. Clique no ícone de engrenagem (![ícone de engrenagem](../../assets/gear-icon.png)) ao lado do nome do painel e, em seguida, na janela [!UICONTROL Bulk Edit Reports].

1. Clique em **[!UICONTROL Prepend Report Names]** na janela pop-up.

1. Digite as palavras ou os caracteres que você deseja anexar aos seus gráficos.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![anexar](../../assets/prepend.gif)

## Alterando `Dates` {#dates}

1. Clique no ícone de engrenagem (![ícone de engrenagem](../../assets/gear-icon.png)) ao lado do nome do painel e selecione a janela [!UICONTROL Bulk Edit Reports].

1. Clique em **[!UICONTROL Change Dates]** na janela pop-up.

1. Defina os novos `Start/End Date` e `Time Interval`. Você também pode deixar esses campos inalterados.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![alterando datas](../../assets/dates.gif)
