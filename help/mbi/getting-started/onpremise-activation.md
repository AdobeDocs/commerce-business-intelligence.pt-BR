---
title: 'Ativar sua conta  [!DNL Adobe Commerce Intelligence] '
description: Saiba com quem contatar para ativar sua conta do  [!DNL Commerce Intelligence] .
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Ativar a conta [!DNL Commerce Intelligence] para Assinaturas no Local e de Início

Para ativar o [!DNL Commerce Intelligence] para assinaturas locais, primeiro crie uma conta do [!DNL Commerce Intelligence], insira suas informações de configuração e conecte o [!DNL Commerce Intelligence] ao banco de dados do [!DNL Commerce]. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Crie sua conta do [!DNL Commerce Intelligence]

Para criar sua conta, entre em contato com a equipe de conta da Adobe ou com o consultor técnico do cliente.

## Crie sua senha

Depois que sua conta for criada, verifique se há um email de notificação de conta de [!DNL The Magento BI Team@rjmetrics.com]. Use o link fornecido no email para acessar sua conta do [!DNL Commerce Intelligence] e criar sua senha. Vá para sua caixa de entrada e verifique seu endereço de email.

Se você não recebeu um email, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![Criar tela de senha para a nova conta do Commerce Intelligence](../assets/create-account-4.png)

## Definir as preferências da loja

Antes de configurar a conexão de banco de dados, preencha o formulário de informações de armazenamento. Essas informações são necessárias para concluir a configuração do **[!UICONTROL Connect your Database]**.

![Armazenar formulário de informações com campos de nome da empresa, moeda e fuso horário](../assets/create-account-6.png)

## Adicionar [!DNL Commerce Intelligence] usuários

Depois de definir sua senha e fazer logon no [!DNL Commerce Intelligence], você pode adicionar outros usuários à sua conta do [!DNL Commerce Intelligence]. Ao adicionar usuários, adicione usuários administradores com as permissões apropriadas para concluir o processo de ativação.

![Adicionar formulário de usuário com campos de endereço de email e nível de permissão](../assets/create-account-5.png)

## Criar um usuário [!DNL Commerce Intelligence] dedicado no administrador [!DNL Commerce]

Para usar o [!DNL Commerce Intelligence], você deve adicionar um usuário permanente e dedicado ao projeto [!DNL Commerce]. Este usuário dedicado serve como uma conexão permanente com o [!DNL Commerce] que permite a busca e a transferência de novos dados para o Data Warehouse [!DNL Commerce Intelligence] da conta.

A configuração de um usuário [!DNL Commerce Intelligence] dedicado garante que a conta não seja desativada ou excluída, interrompendo assim a conexão [!DNL Commerce Intelligence].


>[!NOTE]
>
>A Adobe incentiva o uso de um nome de conta que indique seu status permanente (por exemplo, ACI-dedicated, ACI-database-connector e assim por diante).

Depois de criar o usuário dedicado para [!DNL Commerce Intelligence] no Administrador, adicione o mesmo usuário ao ambiente primário do projeto [!DNL Commerce] com uma configuração **[!UICONTROL Master]** de `Contributor`.

![Commerce adiciona interface de usuário com função definida como Colaborador](../assets/commerce-add-user-settings.png)

## Obtenha suas chaves SSH do Commerce Intelligence

1. Na página [!UICONTROL Connect your database] da instalação do [!DNL Commerce Intelligence], role para baixo e selecione **[!UICONTROL Encryption settings]**.

1. Para **Tipo de Criptografia**, selecione `SSH Tunnel`.

1. No menu suspenso, copie a chave pública fornecida.

   ![Página de configurações de criptografia mostrando o tipo de túnel SSH e o campo de chave pública](../assets/encryption-setting-new-account.png)

## Adicione sua chave pública ao [!DNL Commerce Intelligence]

1. No [!DNL Commerce Admin], entre usando as informações de logon do usuário [!DNL Commerce Intelligence] que você acabou de criar.

1. Selecione a guia **Configurações da conta**.

1. Role para baixo e expanda o menu suspenso **[!UICONTROL SSH Keys]**. Em seguida, selecione **[!UICONTROL Add a public key]**.

   ![Página de configurações da conta com a seção Chaves SSH e botão Adicionar chave pública](../assets/add-public-key.png)

1. Cole a chave pública que você copiou na etapa [!DNL Encryption Type] acima.

   ![Adicionar formulário de chave pública com campo de texto de chave e botão Enviar](../assets/paste-public-key.png)

## Fornecer credenciais do [!DNL Commerce Intelligence] do `MySQL` Essentials

1. Atualize seu `.magento/services.yaml`.

   ![Código mostrando a configuração do serviço MySQL no arquivo services.yaml](../assets/update-magento-services-yaml.png)

1. Atualize seu `.magento.app.yaml`.

   ![Código mostrando a configuração de relações de banco de dados no arquivo app.yaml](../assets/magento-app-yaml-relationships.png)

## Obter informações de conexão do banco de dados

Obter as informações de conexão do banco de dados [!DNL Commerce] para [!DNL Commerce Intelligence]

1. Execute o seguinte para obter suas informações.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Revise as informações do banco de dados, que devem ser semelhantes ao exemplo a seguir.

   ![Saída JSON mostrando as credenciais de conexão do banco de dados, incluindo host, porta e nome de usuário](../assets/example-database-information.png)

## Conectar [!DNL Commerce Intelligence] ao banco de dados [!DNL Commerce] usando uma conexão criptografada

>[!NOTE]
>
>A Adobe recomenda que você use um túnel [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) para fazer a conexão com o banco de dados. No entanto, se esse método não for uma opção, você ainda poderá vincular [!DNL Commerce Intelligence] ao banco de dados usando um [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Insira suas informações de [!DNL Commerce Intelligence] na tela [!UICONTROL Connect your Magento Database].

![Conecte o formulário do banco de dados a campos para nome da integração, host, porta, nome de usuário, senha e nome do banco de dados](../assets/connect-magento-db.png)

**Entradas:**

[!UICONTROL Integration Name]: [escolha um nome para a instância [!DNL Commerce Intelligence]]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Nome de usuário]: `mbi`

[!UICONTROL Password]: [senha de entrada exibida na seção anterior]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [deixe em branco se não houver prefixos de tabela]

## Definir suas configurações de [!UICONTROL **Fuso Horário**]

![Formulário de configurações de fuso horário com fuso horário do banco de dados e campos suspensos de fuso horário desejados](../assets/time-zone-settings.png)

**Entradas:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [escolha o fuso horário para o qual deseja exibir seus dados]

## Obter informações de configurações de criptografia

A interface do projeto fornece uma cadeia de caracteres de acesso SSH. Esta cadeia de caracteres pode ser usada para coletar as informações necessárias para o [!UICONTROL **Endereço Remoto**] e o [!UICONTROL **Nome de Usuário**]. Use a cadeia de caracteres de Acesso SSH selecionando o botão de acesso do site na ramificação mestre da interface do usuário do projeto. Em seguida, localize seus [!UICONTROL User Name] e [!UICONTROL Remote Address] conforme mostrado abaixo.

![Interface do usuário do projeto mostrando informações de acesso SSH com nome de usuário e endereço remoto](../assets/master-branch-settings.png)

## Insira suas configurações de [!DNL Encryption]

![Formulário de configurações de criptografia com campos para tipo de criptografia, endereço remoto, nome de usuário e porta](../assets/encryption-settings-2.png)

**Entradas:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud` [da etapa anterior]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento` [da etapa anterior]

[!UICONTROL Port]: `22`

## Salve sua integração.

Após concluir as etapas de configuração, aplique as alterações selecionando [!UICONTROL **Salvar Integração**].

Você conectou com êxito o banco de dados [!DNL Commerce] à conta [!DNL Commerce Intelligence].

>[!NOTE]
>
>Se você for um cliente do [!DNL Adobe Commerce Intelligence Pro], entre em contato com seu Gerente de sucesso do cliente ou com o Consultor técnico do cliente para coordenar as próximas etapas.

Após concluir a configuração, [entre](../getting-started/sign-in.md) em sua conta do [!DNL Commerce Intelligence].

<!---# Activate your [!DNL Commerce Intelligence] Account

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
