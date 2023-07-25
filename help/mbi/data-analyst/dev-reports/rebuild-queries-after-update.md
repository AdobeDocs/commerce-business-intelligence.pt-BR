---
title: Recriar consultas após o ciclo de atualização?
description: Saiba o que acontece com as consultas após a execução do ciclo de atualização.
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Reconstrução de Consultas após o Ciclo de Atualização

Não é necessário recriar as consultas. Relatórios criados usando o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) são salvas como as criadas no `Report Builder`. O processo de atualização dos gráficos SQL é o mesmo: depois que os dados forem atualizados, os valores nos gráficos serão recalculados e exibidos novamente.
