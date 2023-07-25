---
title: Compartilhar painéis com outros usuários
description: Saiba como compartilhar painéis com outros usuários.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Compartilhar painéis com outros usuários

O compartilhamento de painéis é uma ótima maneira de manter sua equipe informada e incentivar discussões colaborativas. Ao criar e compartilhar um painel central, você pode fornecer à sua equipe as informações necessárias, mantendo o controle. [[!DNL Adobe] recomenda](../../best-practices/share-dashboard-best-practice.md){: target=&quot;_blank&quot;} que você concedeu `Edit` direitos para selecionar alguns para minimizar as alterações acidentais.

>[!NOTE]
>
>Se o painel que você está compartilhando contiver relatórios criados com métricas às quais um usuário específico não tem acesso, os relatórios exibirão uma `Error Loading Data` mensagem. Se quiser que os dados sejam exibidos para o usuário específico, uma variável [usuário administrador](../../administrator/user-management/user-management.md) O deve conceder acesso a todas as métricas usadas nesses relatórios.

## Compartilhar um painel

1. Clique em **[!UICONTROL Share Dashboard]** na parte superior da tela.

   Uma lista de todos os usuários em seu [!DNL Commerce Intelligence] a conta será exibida.

1. Para selecionar um usuário com o qual compartilhar o painel, marque a caixa à esquerda do nome.

   Para selecionar/desmarcar todos os usuários, clique em **[!UICONTROL Select]** e selecione `Everyone` ou `None`, respectivamente.

1. As permissões podem ser definidas para cada usuário ou em massa.

   *Para definir permissões individuais*, clique em **[!UICONTROL None]** à direita do nome do usuário. Nesta lista suspensa, selecione o tipo de permissões que o usuário deve ter.

   *Para definir permissões em massa*, clique em **[!UICONTROL Set Permissions]**. Nesta lista suspensa, selecione o tipo de permissões que os usuários selecionados devem ter.

   >[!NOTE]
   >
   >Você também pode usar esse recurso para atualizar permissões definidas anteriormente. Por exemplo, se você deseja interromper o compartilhamento do painel com alguém, defina as permissões para `None`.

1. Para compartilhar o painel, clique em **[!UICONTROL Save Changes]**. Os usuários selecionados receberão um email convidando-os a visualizar o painel.

Exemplo:

![compartilhar painel](../../assets/Share_Dashboards.gif)
