---
title: Depuração da [!DNL MBI] Conta
description: Saiba como limpar seu [!DNL MBI] conta.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# Limpe seu [!DNL MBI] Conta

Se você esteve com [!DNL MBI] por 6 meses ou 6 anos, manter uma conta arrumada é fundamental para que sua organização obtenha o máximo da plataforma. Com o tempo, é natural que haja usuários, painéis, relatórios, métricas e colunas que não são mais necessárias. Talvez você tenha criado um relatório para uso único e esquecido disso, ou um usuário que deixou a empresa nunca teve sua conta desativada.

Em conjunto com [nomenclatura padronizada e clara para todos os elementos](../best-practices/naming-elements.md)) da sua [!DNL MBI] , as etapas de auditoria de conta abaixo ajudarão você a reduzir a confusão e as análises desnecessárias para seus usuários. Um benefício adicional inclui [ciclos de atualização potencialmente mais rápidos](../best-practices/reduce-update-cycle-time.md).

## Etapa 1: Identifique seus usuários não ativos

A primeira etapa para limpar sua conta é desativar as contas de seus usuários não ativos, como pessoas que deixaram a empresa ou não usam mais [!DNL MBI] nas funções atuais.

Você pode fazer isso clicando no nome da empresa no canto superior direito da barra de navegação superior e selecionando **[!UICONTROL Manage Users]**. Em seguida, selecione o usuário que deseja desativar e clique em **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Você precisa [Permissões de administrador](../administrator/user-management/user-management.md) para fazer isso.

>[!WARNING]
>
>A desativação de um usuário também removerá os gráficos, painéis e outros ativos criados por esse usuário. Se quiser preservar esses ativos, entre em contato com o [!DNL MBI] [suporte](../guide-overview.md) antes de desativar o usuário. O suporte pode ajudar você a transferir esses ativos para outro usuário.

### Reativar um usuário

Para reativar um usuário, reconvide-o recriando sua conta com o mesmo endereço de email desativado, e seu acesso e os dados de sua propriedade serão restaurados no logon.

## Etapa 2: Excluir painéis e relatórios não utilizados

A próxima etapa na auditoria de sua conta é excluir todos os painéis e relatórios não utilizados.

>[!NOTE]
>
>Você precisa `Admin` ou `Standard` [permissões do usuário](../administrator/user-management/user-management.md) para fazer isso.

Cada usuário com `Admin` ou `Standard` O acesso do pode criar relatórios e painéis. Por esse motivo, todos com essas permissões devem seguir as etapas abaixo para identificar e remover relatórios não utilizados.

### Revisar seus painéis e relatórios

Antes de excluir qualquer item, você deve revisar seus relatórios e painéis para avaliar o que está em uso no momento. Embora você possa usar a variável **[!UICONTROL find unused reports]** recurso descrito abaixo, qualquer revisão inicial tornará seus esforços de limpeza muito mais produtivos.

### Exclusão de painéis e relatórios

Depois de acessar seus painéis e relatórios, você pode começar a limpar sua conta.

**Para remover um relatório de um painel**

1. Localize o relatório que deseja remover no painel.
1. Selecionar **[!UICONTROL Options]** no canto superior direito do relatório.
1. Clique em **[!UICONTROL Remove From Dashboard]**.

**Para excluir um painel inteiro**

1. Selecionar **[!UICONTROL Manage Data]** e depois **[!UICONTROL Dashboards**].
1. Clique no painel que deseja excluir.
1. Clique em **[!UICONTROL Delete Dashboard]**.

Você também pode selecionar **[!UICONTROL Dashboard Options]**, em seguida **[!UICONTROL Delete]** no próprio painel.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>A exclusão de um painel não exclui os relatórios nele, portanto, é necessário tomar mais uma etapa para excluir os relatórios.

**Para Excluir Relatórios Não Utilizados**

1. Selecionar **[!UICONTROL Manage Data]**, em seguida **[!UICONTROL Reports]**.
1. Verifique a **Mostrar somente relatórios não usados** localizada abaixo da lista de métricas. Isso criará uma lista de relatórios que não são usados em um painel ou resumo do email.
1. Selecione os relatórios que deseja excluir. Você pode selecionar tudo clicando na caixa de seleção acima da lista de relatórios.
1. Clique em **[!UICONTROL Delete Selected]**.

Veja a seguir o processo de exclusão de relatório não utilizado:

![](../../mbi/assets/unused_reports.png)

## Etapa 3: Excluir métricas não usadas

Após limpar a lista de usuários, os painéis e os relatórios, você pode passar para a auditoria da lista de métricas. Isso ajudará a identificar qualquer coisa que possa estar desatualizada, por exemplo, uma nova métrica foi criada com uma definição diferente ou não está em uso.

1. Para gerar uma lista de relatórios dependentes para uma métrica, acesse **[!DNL Manage Data]** e, em seguida, selecione Click **[!UICONTROL Metrics]**.
1. Clique em **[!UICONTROL Edit]** ao lado de uma métrica.
1. Na parte inferior da página, você verá uma seção chamada **[!UICONTROL Dependent Charts]**. Clique no link para gerar uma lista de relatórios dependentes para essa métrica.
1. Depois que o sistema concluir a verificação, [!DNL MBI] exibe uma lista de painéis, relatórios e usuários que utilizam essa métrica.

![](../../mbi/assets/report_dependecies.png)

Se você decidir que a métrica não é mais necessária, navegue de volta para a **[!UICONTROL Metrics]** clicando em **[!UICONTROL Back to Metric List]** na parte superior da página e localize a métrica que deseja excluir. Clique em **[!UICONTROL Delete]**.

## Etapa 4: Avaliar suas colunas sincronizadas

A última etapa é avaliar as colunas que estão sendo sincronizadas no data warehouse. Não apenas a não sincronização de colunas pode decolar sua conta, como também pode reduzir o tempo de atualização.

Caso deseje continuar com isso, entre em contato com o [!DNL MBI] [Suporte](../guide-overview.md). A equipe de suporte pode criar um relatório que inclua todas as colunas que não estão sendo usadas em nenhum painel para nenhum usuário e que não sejam usadas em resumos de email, excluindo Relatórios SQL. Em seguida, você pode usar esse relatório como guia para selecionar colunas para não sincronizar por meio do Gerenciador de Datas Warehouse.

>[!NOTE]
>
>Você sempre poderá iniciar a sincronização dessas colunas novamente no futuro. Cancelar a sincronização de uma coluna não removerá dados do data warehouse; isso significa apenas que essa coluna não será verificada em busca de valores novos ou atualizados durante o ciclo de atualização.

**Para dessincronizar uma coluna (ou colunas)**

1. Ir para **[!DNL Manage Data]**, em seguida **[!UICONTROL Data Warehouse]**.
1. No **[!UICONTROL Synced Tables]** navegue até a tabela que contém a coluna.
1. Marque as caixas ao lado das colunas que deseja cancelar a sincronização.
   >[!NOTE]
   >
   >Não é possível cancelar a sincronização de uma coluna Chave primária sem soltar toda a tabela.

1. Clique em **[!UICONTROL Remove]** para cancelar a sincronização das colunas.

Veja o processo inteiro:

![](../../mbi/assets/drop_column.png)

## Quebra de linha

Pronto! Seu [!DNL MBI] Agora, a conta deve ser mais fixa e fácil de navegar para você e para sua equipe.
