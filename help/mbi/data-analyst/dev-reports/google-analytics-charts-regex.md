---
title: Criar gráficos de Google Analytics
description: Saiba como criar gráficos a partir dos dados do Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Criar [!DNL Google Analytics] gráficos

(com ajuda da sintaxe de regex)

Depois de conectar seu [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), você pode criar gráficos com o seu [!DNL Google Analytics] dados.

## Criar [!DNL Google Analytics] Gráficos

1. Clique em **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Ao selecionar uma métrica na variável `Chart Builder`, role até a parte inferior da lista para encontrar uma seção que inclua [!DNL Google Analytics] Perfis. Uma segunda lista suspensa de métricas é exibida. Aqui é possível escolher a métrica que deseja analisar.

1. Após escolher a métrica, você pode continuar com esse gráfico como se ele fosse qualquer outro gráfico selecionando o `time period`, `interval`, e dados `perspectives` que você gostaria de ver.

1. A grande diferença aqui é que `√` O usa expressões regulares para filtros. Uma expressão regular (regex para abreviar) é uma sequência especial de texto para descrever um padrão de pesquisa. Veja exemplos de sintaxe regex no [[!DNL Google] guia sobre expressões regulares do Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Os únicos caracteres especiais que precisam ser evitados usando o caractere \ são os Metacaracters abaixo:

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
