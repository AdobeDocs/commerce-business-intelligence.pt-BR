---
title: Criar gráficos de Google Analytics
description: Saiba como criar gráficos a partir dos dados do Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Criar [!DNL Google Analytics] gráficos

(com a ajuda da sintaxe regex)

Depois de conectar seu [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), é possível criar gráficos a partir de [!DNL Google Analytics] dados.

## Criar [!DNL Google Analytics] Gráficos

1. Clique em **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Ao selecionar uma métrica na variável `Chart Builder`, role até a parte inferior da lista para encontrar uma seção incluindo [!DNL Google Analytics] Perfis. Uma segunda lista suspensa de métricas será exibida. Aqui você pode escolher a métrica que deseja analisar.

1. Após escolher a métrica, você pode prosseguir com esse gráfico como se fosse qualquer outro, selecionando o `time period`, `interval`e dados `perspectives` que você gostaria de ver.

1. A grande diferença aqui é que `√` O usa expressões regulares para filtros. Uma expressão regular (regex para short) é uma string especial de texto para descrever um padrão de pesquisa. Consulte exemplos de sintaxe regex na seção [[!DNL Google] guia sobre expressões regulares do Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Os únicos caracteres especiais que precisam ser evitados por meio do caractere \ são os Metacárteres abaixo:

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
