---
title: Painéis
description: Saiba como criar e trabalhar com um painel.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Painéis

[!DNL MBI] Os painéis fornecem uma visão rápida do desempenho e da atividade de vendas de sua loja. Painéis individuais podem ser compartilhados com outros usuários e organizados em grupos lógicos. Você também pode definir diferentes níveis de permissão para outros usuários.

É fácil criar um novo relatório, adicioná-lo a um painel e exportar os dados para o Excel. Os gráficos e relatórios podem ser redimensionados e arrastados para a posição no painel.

![Painel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Criação de painéis {#createdash}

Os painéis são essencialmente compartilháveis, têm temas para as análises criadas nos Report Builder. É assim que você pode incentivar sua equipe a colaborar e manter uma única fonte de verdade em toda a organização.

*Se você for um Administrador ou Usuário padrão*, é possível criar um painel clicando no botão `Dashboard Options` lista suspensa e escolha `Create New dashboard`.

A aparência dos painéis criados depende de você. Você pode organizar e redimensionar os elementos no painel da maneira que quiser que atenda às suas necessidades e workflow.

![organizar elemento do painel de redimensionamento](../../assets/arrange_resize_dashboard_element.gif)

### Criar um novo painel

1. No menu, clique em **[!UICONTROL Dashboards]**.

1. O nome do painel padrão é exibido no canto superior esquerdo do cabeçalho do painel. Clique na seta para baixo (![](../../assets/magento-bi-btn-down.png)) para mostrar as opções disponíveis.

   ![Criar painel](../../assets/magento-bi-dashboard-create.png)

1. Clique em **[!UICONTROL Create Dashboard]**. Em seguida, faça o seguinte:

   * Insira um `Name` para seu painel.

   * Para criar um novo `Group` no painel, insira o nome do grupo.

      Por exemplo, se sua instalação do Commerce tiver várias exibições de loja, você poderá criar um Grupo para cada exibição de loja.

   * Clique em **[!UICONTROL Create]**.

   ![nome do painel](../../assets/magento-bi-dashboard-create-name.png)

   * O nome do novo painel aparece no canto superior esquerdo. Clique na seta para baixo (![](../../assets/magento-bi-btn-down.png)) para mostrar as opções. Se você criou um grupo, o novo painel aparece abaixo do grupo na lista.


### Adicionar um relatório

1. Para adicionar um relatório, siga um destes procedimentos:

   * Clique no botão **[!UICONTROL Add a report]** na página.

   * No cabeçalho do painel, clique em **[!UICONTROL Add Report]**.

      ![Adicionar relatório](../../assets/magento-bi-dashboard-create-add-report.png)

1. Clique em **[!UICONTROL Create Report]** para mostrar a **[!UICONTROL Report Builder Options]**.

   ![Opções de Report Builder](../../assets/magento-bi-report-builder.png)

## Organizar itens em um painel

* Para redimensionar um gráfico ou relatório, arraste o canto inferior direito para o novo tamanho.

* Para mover um gráfico ou relatório, passe o mouse sobre o título ou cabeçalho até que o cursor mude para uma cruz. Em seguida, arraste-o para a posição.

## Gerenciamento de painéis {#managedash}

Em **[!DNL Manage Data** > **Dashboards]**, você pode gerenciar permissões do usuário para painéis de sua propriedade, excluir painéis de que não precisa mais e definir um painel padrão.

### Compartilhamento de painéis {#sharingdash}

Para dimensionar verdadeiramente [!DNL MBI] em toda a organização e forneça insights valiosos, recomendamos que você compartilhe painéis criados com outros membros da equipe. *Você pode compartilhar seus painéis* clicando no botão `Share Dashboard` na parte superior da página.

Ao compartilhar um painel, você pode atribuir permissões em sua organização OU individualmente, o que significa que decide quem pode exibir e editar seus relatórios.

>[!NOTE]
>
>`Read-Only` os usuários só têm acesso aos painéis que são compartilhados diretamente com eles; eles não podem pesquisar e adicionar painéis sozinhos. Não se esqueça de mantê-los em loop!

### Acesso aos painéis compartilhados {#accessshared}

*Se você for um usuário administrador ou padrão* e quiser adicionar um painel compartilhado à sua conta, clique em **[!UICONTROL Dashboard Options]** e, em seguida, clicando em **[!UICONTROL Find]** na lista suspensa.

![localizar painel](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Gerenciar configurações do painel

1. No menu, clique em **[!DNL Manage Data** > **Dashboards]**.

1. Se aplicável, insira um novo `Dashboard Name`.

1. Atribuição do painel a um `Dashboard Group`, escolha na lista de grupos.

   **`Permissions`**

   Para conceder a todos os usuários o mesmo nível de acesso ao painel, faça o seguinte:

   1. Em **`Shared with`**, escolha uma das seguintes opções:

      * `View`
      * `Edit`
      * `None`
   1. Quando solicitado a confirmar, clique em **[!UICONTROL OK]** para atualizar o nível de permissões para cada usuário.

   1. Para alterar o nível de permissão de um indivíduo, encontre o usuário na lista e altere o nível de permissão. A alteração é salva automaticamente.

   **`Default`**

   1. Para tornar esse painel o padrão para o seu [!DNL MBI] conta, clique em **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Para remover o painel, clique em **[!UICONTROL Delete Dashboard]**.
