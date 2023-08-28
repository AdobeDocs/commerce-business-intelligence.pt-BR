---
title: Ativar o [!DNL Adobe Commerce Intelligence] Conta
description: Saiba com quem entrar em contato para ativar o [!DNL Commerce Intelligence] conta.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Ativar o [!DNL Commerce Intelligence] Conta para Assinaturas no Local e de Início

Para ativar [!DNL Commerce Intelligence] para assinaturas no local, primeiro crie um [!DNL Commerce Intelligence] conta, insira as informações de configuração e conecte [!DNL Commerce Intelligence] ao seu [!DNL Commerce] banco de dados. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Crie seu [!DNL Commerce Intelligence] account

Para criar sua conta, entre em contato com a equipe de conta do Adobe ou com o consultor técnico do cliente.

## Crie sua senha

Depois que a conta for criada, verifique se há um email de notificação de conta do [!DNL The Magento BI Team@rjmetrics.com]. Use o link fornecido no email para acessar [!DNL Commerce Intelligence] e crie sua senha. Vá para sua caixa de entrada e verifique seu endereço de email.

Se você não recebeu um email, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![](../assets/create-account-4.png)

## Definir as preferências da loja

Antes de configurar a conexão de banco de dados, preencha o formulário de informações de armazenamento. Essas informações são necessárias para concluir a **[!UICONTROL Connect your Database]** configuração.

![](../assets/create-account-6.png)

## Adicionar [!DNL Commerce Intelligence] usuários

Depois de definir sua senha e fazer logon no [!DNL Commerce Intelligence], é possível adicionar outros usuários ao seu [!DNL Commerce Intelligence] conta. Ao adicionar usuários, adicione usuários administradores com as permissões apropriadas para concluir o processo de ativação.

![](../assets/create-account-5.png)

## Criar um dedicado [!DNL Commerce Intelligence] usuário no [!DNL Commerce] administrador

Para usar [!DNL Commerce Intelligence], você deve adicionar um usuário permanente e dedicado à [!DNL Commerce] projeto. Esse usuário dedicado serve como uma conexão permanente com o [!DNL Commerce] que permite a busca e a transferência de novos dados para o [!DNL Commerce Intelligence] Data Warehouse.

Configurar um dedicado [!DNL Commerce Intelligence] usuário garante que a conta não seja desativada ou excluída, interrompendo assim a [!DNL Commerce Intelligence] conexão.


>[!NOTE]
>
>O Adobe incentiva o uso de um nome de conta que indique seu status permanente (por exemplo, ACI-dedicated, ACI-database-connector e assim por diante).

Depois de criar o usuário dedicado para [!DNL Commerce Intelligence] no Administrador, adicione o mesmo usuário ao ambiente primário do [!DNL Commerce] projeto com um **[!UICONTROL Master]** configuração de `Contributor`.

![](../assets/commerce-add-user-settings.png)

## Obter suas chaves SSH de Inteligência do Commerce

1. No [!UICONTROL Connect your database] página para [!DNL Commerce Intelligence] configurar, rolar para baixo e selecionar **[!UICONTROL Encryption settings]**.

1. Para **Tipo de criptografia**, selecione `SSH Tunnel`.

1. No menu suspenso, copie a chave pública fornecida.

   ![](../assets/encryption-setting-new-account.png)

## Adicione sua chave pública à [!DNL Commerce Intelligence]

1. No [!DNL Commerce Admin], faça logon usando as informações de logon da [!DNL Commerce Intelligence] usuário que você acabou de criar.

1. Selecione o **Configurações da conta** guia.

1. Role para baixo e expanda a **[!UICONTROL SSH Keys]** menu suspenso. Em seguida, selecione **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. Cole a chave pública que você copiou na [!DNL Encryption Type] etapa acima.

   ![](../assets/paste-public-key.png)

## Fornecer [!DNL Commerce Intelligence] Fundamentos `MySQL` credenciais

1. Atualize seu `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. Atualize seu `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## Obter informações de conexão do banco de dados

Obtenha as informações de conexão do banco de dados para o [!DNL Commerce] banco de dados para [!DNL Commerce Intelligence]

1. Execute o seguinte para obter suas informações.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Revise as informações do banco de dados, que devem ser semelhantes ao exemplo a seguir.

   ![](../assets/example-database-information.png)

## Conectar [!DNL Commerce Intelligence] ao seu [!DNL Commerce] banco de dados usando uma conexão criptografada

>[!NOTE]
>
>A Adobe recomenda que você use um [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) túnel para estabelecer a conexão com o banco de dados. No entanto, se esse método não for uma opção, ainda será possível vincular [!DNL Commerce Intelligence] ao banco de dados usando uma [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Insira seu [!DNL Commerce Intelligence] informações na [!UICONTROL Connect your Magento Database] tela.

![](../assets/connect-magento-db.png)

**Entradas:**

[!UICONTROL Integration Name]: [escolha um nome para o seu [!DNL Commerce Intelligence] instância]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Nome de usuário]: `mbi`

[!UICONTROL Password]: [senha de entrada exibida na seção anterior]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [deixe em branco se não houver prefixos de tabela]

## Defina seu [!UICONTROL **Fuso Horário**] configurações

![](../assets/time-zone-settings.png)

**Entradas:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [escolha o fuso horário para o qual deseja exibir seus dados]

## Obter informações de configurações de criptografia

A interface do projeto fornece uma cadeia de caracteres de acesso SSH. Essa string pode ser usada para coletar as informações necessárias para o [!UICONTROL **Endereço remoto**] e [!UICONTROL **Nome de usuário**]. Use a cadeia de caracteres de Acesso SSH selecionando o botão de acesso do site na ramificação mestre da interface do usuário do projeto. Em seguida, encontre seu [!UICONTROL User Name] e [!UICONTROL Remote Address] conforme mostrado abaixo.

![](../assets/master-branch-settings.png)

## Insira seu [!DNL Encryption] configurações

![](../assets/encryption-settings-2.png)

**Entradas:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud`  [da etapa anterior]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento`  [da etapa anterior]

[!UICONTROL Port]: `22`

## Salve sua integração.

Após concluir as etapas de configuração, aplique as alterações selecionando [!UICONTROL **Salvar integração**].

Você conectou o seu agora com sucesso [!DNL Commerce] banco de dados para seu [!DNL Commerce Intelligence] conta.

>[!NOTE]
>
>Se você é um [!DNL Adobe Commerce Intelligence Pro] cliente, entre em contato com o Gerente de sucesso do cliente ou o Consultor técnico do cliente para coordenar as próximas etapas.

Após concluir a configuração, [fazer logon](../getting-started/sign-in.md) ao seu [!DNL Commerce Intelligence] conta.

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
