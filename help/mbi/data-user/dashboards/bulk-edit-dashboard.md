---
title: Gráficos de edição em massa nos painéis
description: Saiba como usar o recurso de edição em massa no [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Gráficos de edição em massa nos painéis

O recurso de edição em massa facilita a alteração de nomes e datas de gráficos em seus painéis. Por exemplo, você deseja que todos os gráficos em um painel específico se refiram a um único armazenamento e relatório mensalmente em vez de trimestralmente. Em vez de alterar tudo manualmente, deixe a `bulk-editing` recurso do trabalho. Neste tópico, você aprenderá a usar:

* [A variável [!DNL Find/Replace] Recurso](#findreplace)

* [A variável [!DNL Prepend Name] Recurso](#prepend)

* [A variável [!DNL Change Dates] Recurso](#dates)

Dito isto, considerem isto - *Essas mudanças precisam ser permanentes?* Caso contrário, considere clonar o painel e alterar as datas no novo painel. Isso permite preservar o painel original e, ao mesmo tempo, fazer as alterações necessárias.

>[!NOTE]
>
>Se você estiver alterando vários relatórios, o processo de atualização pode demorar um pouco.

## Usar [!DNL Find/Replace] {#findreplace}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ao lado do nome do painel e, em seguida, o ícone [!UICONTROL Bulk Edit Reports] janela.

1. Clique em **[!UICONTROL Chart Title Find and Replace]** no pop-up.

1. No `Chart Title Find` digite as palavras ou os caracteres que deseja localizar.

1. No `Replace With` digite as palavras ou caracteres que devem substituir o que está na caixa `Find` campo.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![editar em massa](../../assets/bulk_edit.gif)

## Pendente `Chart Names` {#prepend}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ao lado do nome do painel e, em seguida, o ícone [!UICONTROL Bulk Edit Reports] janela.

1. Clique em **[!UICONTROL Prepend Report Names]** no pop-up.

1. Digite as palavras ou os caracteres que você deseja anexar aos seus gráficos.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![anexar](../../assets/prepend.gif)

## Alteração `Dates` {#dates}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ao lado do nome do painel e selecione o ícone [!UICONTROL Bulk Edit Reports] janela.

1. Clique em **[!UICONTROL Change Dates]** na janela pop-up.

1. Defina o novo `Start/End Date` e `Time Interval`. Você também pode deixar esses campos inalterados.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![alteração de datas](../../assets/dates.gif)
