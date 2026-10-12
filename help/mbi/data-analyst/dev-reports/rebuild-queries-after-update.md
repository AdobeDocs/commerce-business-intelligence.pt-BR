---
title: Recriar consultas após o ciclo de atualização?
description: Saiba o que acontece com as consultas após a execução do ciclo de atualização.
role: Admin, User
feature: Commerce Tables, Data Warehouse Manager, Reports
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
source-git-commit: e394c83041fa764ad81bd0b6b74240eb5c2f567d
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%
---
# Reconstrução de Consultas após o Ciclo de Atualização

Não é necessário recriar as consultas. Os relatórios criados usando o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) são salvos como os criados no `Report Builder` tradicional. O processo de atualização dos gráficos SQL é o mesmo: depois que os dados forem atualizados, os valores nos gráficos serão recalculados e exibidos novamente.
