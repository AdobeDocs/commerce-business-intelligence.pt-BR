---
title: Painéis
description: Saiba como criar e trabalhar com um painel.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Painéis

Os painéis do [!DNL Adobe Commerce Intelligence] fornecem uma visão rápida do desempenho da sua loja e das atividades de vendas. Painéis individuais podem ser compartilhados com outros usuários e organizados em grupos lógicos. Você também pode definir diferentes níveis de permissão para outros usuários.

É fácil criar um relatório, adicioná-lo a um painel e exportar os dados para o Excel. Os gráficos e relatórios podem ser redimensionados e arrastados para a posição no painel.

![Painel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Criação de painéis {#createdash}

Os painéis são compartimentáveis, com temas para as análises criadas nos Construtores de relatórios. É assim que você pode incentivar sua equipe a colaborar e manter uma única fonte de verdade em toda a organização.

*Se você for um usuário Administrador ou Padrão*, poderá criar um painel clicando na lista suspensa `Dashboard Options` e escolhendo `Create New dashboard`.

A aparência dos painéis que você cria depende totalmente de você. Você pode organizar e redimensionar os elementos no painel de qualquer maneira que desejar, para atender às suas necessidades e fluxo de trabalho.

![organizar elemento do painel de redimensionamento](../../assets/arrange_resize_dashboard_element.gif)

### Criar um painel

1. No menu, clique em **[!UICONTROL Dashboards]**.

1. O nome do painel padrão aparece no canto superior esquerdo do cabeçalho do painel. Clique na seta para baixo (![ícone de seta para baixo](../../assets/magento-bi-btn-down.png)) para mostrar as opções disponíveis.

   ![Criar Painel](../../assets/magento-bi-dashboard-create.png)

1. Clique em **[!UICONTROL Create Dashboard]**. Em seguida, faça o seguinte:

   * Digite um `Name` para o seu painel.

   * Para criar um `Group` para o painel, insira o nome do grupo.

     Por exemplo, se a sua instalação do Commerce tiver várias exibições de loja, você pode criar um Grupo para cada exibição de loja.

   * Clique em **[!UICONTROL Create]**.

   ![nome do painel](../../assets/magento-bi-dashboard-create-name.png)

   * O nome do novo painel é exibido no canto superior esquerdo. Clique na seta para baixo (![ícone de seta para baixo](../../assets/magento-bi-btn-down.png)) para mostrar as opções. Se você criou um grupo, o novo painel aparece abaixo do grupo na lista.

### Adicionar um relatório

1. Para adicionar um relatório, siga um destes procedimentos:

   * Clique no prompt **[!UICONTROL Add a report]** na página.

   * No cabeçalho do painel, clique em **[!UICONTROL Add Report]**.

     ![Adicionar relatório](../../assets/magento-bi-dashboard-create-add-report.png)

1. Clique em **[!UICONTROL Create Report]** para mostrar **[!UICONTROL Report Builder Options]**.

   ![Opções do Report Builder](../../assets/magento-bi-report-builder.png)

## Organizar itens em um painel

* Para redimensionar um gráfico ou relatório, arraste o canto inferior direito para o novo tamanho.

* Para mover um gráfico ou relatório, passe o mouse sobre o título ou cabeçalho até que o cursor mude para uma cruz. Em seguida, arraste-o para a posição.

## Gerenciamento de painéis {#managedash}

No **[!DNL Manage Data** > **Dashboards]**, você pode gerenciar permissões de usuário para seus painéis, excluir painéis que não são mais necessários e definir um painel padrão.

### Compartilhamento de seus painéis {#sharingdash}

Para realmente dimensionar o [!DNL Commerce Intelligence] em toda a sua organização e fornecer insights valiosos, a Adobe incentiva você a compartilhar painéis que criar com outros membros da equipe. *Você pode compartilhar seus painéis* clicando na opção `Share Dashboard` na parte superior da página.

Ao compartilhar um painel, você pode atribuir permissões em sua organização OU individualmente, o que significa que decide quem pode visualizar e editar seus relatórios.

>[!NOTE]
>
>`Read-Only` usuários têm acesso somente a painéis que são compartilhados diretamente com eles - eles não podem pesquisar e adicionar painéis por conta própria. Não se esqueça de mantê-los no loop!

### Acesso aos painéis compartilhados {#accessshared}

*Se você for um usuário Administrador ou Padrão* e quiser adicionar um painel compartilhado à sua conta, clique em **[!UICONTROL Dashboard Options]** e em **[!UICONTROL Find]** na lista suspensa.

![localizar painel](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Gerenciar configurações do painel

1. No menu, clique em **[!DNL Manage Data** > **Dashboards]**.

1. Se aplicável, insira um novo `Dashboard Name`.

1. Para atribuir o painel a um `Dashboard Group` específico, escolha na lista de grupos.

   **`Permissions`**

   Para conceder a todos os usuários o mesmo nível de acesso ao painel, faça o seguinte:

   1. Em **`Shared with`**, escolha uma das seguintes opções:

      * `View`
      * `Edit`
      * `None`

   1. Quando a confirmação for solicitada, clique em **[!UICONTROL OK]** para atualizar o nível de permissões para cada usuário.

   1. Para alterar o nível de permissão de um indivíduo, encontre o usuário na lista e altere o nível de permissão. A alteração é salva automaticamente.

   **`Default`**

   1. Para tornar esse painel o padrão para sua conta do [!DNL Commerce Intelligence], clique em **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Para remover o painel, clique em **[!UICONTROL Delete Dashboard]**.
