---
title: Ativar [!DNL MBI] Conta para assinaturas no local
description: Saiba mais sobre como ativar seu [!DNL MBI] para Assinaturas no local.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Ative o [!DNL MBI] Conta para assinaturas no local

Para ativar [!DNL MBI] para assinaturas no local, primeiro crie um [!DNL MBI] conta, em seguida, conectar [!DNL MBI] ao banco de dados do Commerce. Para obter informações sobre a ativação em `Cloud Starter` projetos, consulte [Ativar [!DNL MBI] Conta para `Cloud Starter` Subscrições](../getting-started/cloud-activation.md).

1. Crie seu [!DNL MBI] Conta.

   - Ir para [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - Ir para **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clique em **[!UICONTROL Create Instance]**. Caso não veja esse botão, entre em contato com o Gerente de sucesso do cliente ou com o Consultor técnico do cliente.

   - Insira suas informações para criar sua conta.

   ![](../assets/create-account-2.png)

   - Vá para a caixa de entrada e verifique seu endereço de email. Se você não recebeu um email, [entrar em contato com o suporte](../guide-overview.md).

   - Crie sua senha.

   ![](../assets/create-account-4.png)

   - Após criar sua conta, você tem a opção de adicionar usuários a sua nova conta. Agora, administradores técnicos podem ser adicionados para executar as etapas a seguir.

   ![](../assets/create-account-5.png)

1. Insira informações sobre sua loja para definir suas preferências.

   ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] ao banco de dados do Commerce usando uma conexão criptografada.

   O Commerce recomenda que você se conecte usando um [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). No entanto, se essa não for uma opção, você ainda poderá vincular [!DNL MBI] ao seu banco de dados usando um [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Depois de se conectar com êxito [!DNL MBI] para seu banco de dados do Commerce, entre em contato com o Gerente de sucesso do cliente para coordenar as próximas etapas, como configurar integrações e outras etapas de configuração.

1. Ao terminar a configuração, você pode [fazer logon](../getting-started/sign-in.md) para [!DNL MBI] conta.
