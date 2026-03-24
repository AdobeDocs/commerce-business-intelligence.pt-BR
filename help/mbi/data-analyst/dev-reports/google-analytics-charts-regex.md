---
title: Criar gráficos do Google Analytics
description: Saiba como criar gráficos a partir dos dados do Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
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
source-wordcount: 160
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
