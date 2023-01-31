---
title: Gráficos de edição em massa em painéis
description: Saiba como usar o recurso de edição em massa no [!DNL MBI].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Gráficos de edição em massa em painéis

O recurso de edição em massa facilita a alteração de nomes e datas de gráficos em seus painéis. Por exemplo, você deseja que todos os gráficos em um painel específico se refiram a uma única loja e reportem mensalmente em vez de trimestralmente. Em vez de alterar tudo manualmente, deixe a variável `bulk-editing` O recurso faz o trabalho. Neste artigo, você aprenderá a usar:

* [O ](#findreplace)

* [O ](#prepend)

* [O ](#dates)

Dito isto, considere isto - *Estas alterações têm de ser permanentes?* Caso contrário, considere clonar o painel e alterar as datas no novo painel. Isso permitirá que você preserve seu painel original enquanto ainda faz as alterações necessárias.

>[!NOTE]
>
>Se você estiver fazendo alterações em muitos relatórios, o processo de atualização pode demorar um pouco.

## Usando `Find/Replace` {#findreplace}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ícone ao lado do nome do painel e, em seguida, do [!UICONTROL Bulk Edit Reports] janela.

1. Clique em **[!UICONTROL Chart Title Find and Replace]** na janela pop-up.

1. No `Chart Title Find` digite as palavras ou os caracteres que deseja localizar.

1. No `Replace With` digite as palavras ou os caracteres que devem substituir o que está no campo `Find` campo.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![edição em massa](../../assets/bulk_edit.gif)

## Preenchimento `Chart Names` {#prepend}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ícone ao lado do nome do painel e, em seguida, do [!UICONTROL Bulk Edit Reports] janela.

1. Clique em **[!UICONTROL Prepend Report Names]** na janela pop-up.

1. Digite as palavras ou os caracteres com os quais você deseja incluir os gráficos.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![prefixo](../../assets/prepend.gif)

## Alterar `Dates` {#dates}

1. Clique na engrenagem (![](../../assets/gear-icon.png)) ícone ao lado do nome do painel e selecione o `!UICONTROL Bulk Edit Reports` janela.

1. Clique em **[!UICONTROL Change Dates]** na janela pop-up.

1. Defina o novo `Start/End Date` e `Time Interval`. Também é possível deixar esses campos inalterados.

1. Clique em **[!UICONTROL Update Reports]**.

Exemplo:

![alteração de datas](../../assets/dates.gif)
