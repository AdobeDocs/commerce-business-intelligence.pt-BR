---
title: Usar grupos de painéis
description: Saiba como permitir uma melhor organização dos painéis.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Usar grupos de painéis

Os grupos de painéis permitem uma melhor organização dos painéis. O caso de uso mais comum é agrupar painéis semelhantes no mesmo &quot;grupo&quot;. Por exemplo, todos os painéis relacionados ao marketing podem ser agrupados em um grupo de painéis &quot;Marketing&quot;.

Na lista suspensa de seleção do painel, os grupos de painéis são mostrados em ordem alfabética, com todos os painéis em &quot;Nenhum grupo&quot; mostrados por último. Painéis no mesmo grupo são mostrados juntos e em ordem alfabética dentro de cada grupo.

## Compartilhamento de grupo do painel

Grupos de painéis não podem ser compartilhados diretamente entre usuários. Quando um painel é compartilhado com usuários, o grupo de painéis em que está é criado automaticamente para esses usuários se não existir. Se o grupo de painéis existir, o painel será anexado à lista.

Quando um grupo de um painel é alterado pelo proprietário, a alteração é refletida automaticamente para todos os usuários com os quais o painel foi compartilhado. Os usuários não podem alterar o grupo de painéis para painéis que não são seus.

## Criar grupos de painéis

Os grupos de painéis podem ser criados de uma das duas formas a seguir:

1. Ao criar um painel:

   ![criar grupo de painéis](../../assets/create-dashboard-groups-new-dashboard.png)

1. Ao alterar o grupo de um painel existente, na página `Manage Data > Dashboards`:

   1. Clique no painel para o qual deseja criar o grupo.

   1. Em `Dashboard Group (optional)`, o grupo de painéis atual aparece.

   1. Para criar um grupo, digite o nome do novo grupo e clique em fora da caixa.

      ![criar grupo de painéis](../../assets/create-dashboard-groups-existing-dashboard.png)

## Adicionar painéis existentes a grupos existentes

1. Na página `Manage Data > Dashboards`, escolha o painel para o qual alterar o grupo.

1. O texto em `Dashboard Group (optional)` mostra o grupo de painéis atual do painel.

1. Para alterar o grupo do painel, escolha outro grupo na lista - neste caso, `PS`, `Campaigns`.

   ![alterar painel do grupo](../../assets/add-existing-dashboard-existing-group.png)

## Excluir grupos de painéis

Quando um grupo de painéis não tem painéis, ele é automaticamente excluído.
