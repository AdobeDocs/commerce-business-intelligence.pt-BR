---
title: Clonar painéis
description: Saiba como clonar painéis.
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Clonar um painel

A clonagem de um painel permite copiar todos os relatórios em um painel para um novo painel.

Isso é útil se você quiser recriar um conjunto existente de gráficos, mas alterar a perspectiva (por exemplo, visualização de dados diferente, mercado diferente, site ou loja diferente). Após duplicar o painel, você pode editar cada um dos novos gráficos para alterar sua métrica, visualização de dados, filtro ou agrupar por.

1. Para clonar um painel, clique em **[!UICONTROL Options]** na parte superior da tela.

1. Na lista suspensa, clique em **[!UICONTROL Save As]**.

1. Quando solicitado, insira o `New Dashboard Name`. A Adobe recomenda nomes que informam rapidamente quais informações estão contidas no painel.

   Por exemplo, você está clonando um painel chamado `Customer Activity`. Esse painel continha informações de atividade do cliente para o local da Filadélfia, mas agora você deseja criar um painel para o novo local da cidade de Nova York. Este painel pode ser nomeado como `New York City - Customer Activity`.

1. Use os campos `Chart Title Find` e `Chart Title Replace` para localizar todos os gráficos com `Philadelphia` no título e substituí-los por `New York City`.

   Se você não inserir nenhum valor nesses campos, uma `(2)` será anexada automaticamente ao final de todos os títulos de gráfico no novo painel.

1. Clique em **[!UICONTROL Save]** para clonar o painel.

Exemplo:

![painel do clone](../../assets/datgif.gif)
