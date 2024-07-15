---
title: Criar gráficos de Google Analytics
description: Saiba como criar gráficos a partir dos dados do Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Criar [!DNL Google Analytics] gráficos

(com ajuda da sintaxe de regex)

Após conectar sua [[!DNL Google Analytics] conta](../../data-analyst/importing-data/integrations/google-analytics.md), você pode criar gráficos com seus dados do [!DNL Google Analytics].

## Criar Gráficos de [!DNL Google Analytics]

1. Clique em **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Ao selecionar uma métrica no `Chart Builder`, role até a parte inferior da lista para localizar uma seção que inclua seus Perfis do [!DNL Google Analytics]. Uma segunda lista suspensa de métricas é exibida. Aqui é possível escolher a métrica que deseja analisar.

1. Após escolher a métrica, você pode continuar com este gráfico como se fosse qualquer outro gráfico, selecionando o `time period`, `interval` e os dados `perspectives` que você gostaria de ver.

1. A principal diferença aqui é que `√` usa expressões regulares para filtros. Uma expressão regular (regex para abreviar) é uma sequência especial de texto para descrever um padrão de pesquisa. Consulte exemplos de sintaxe regex no [[!DNL Google] guia sobre expressões regulares do Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Os únicos caracteres especiais que precisam ser evitados usando o caractere \ são os Metacaracters abaixo:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
