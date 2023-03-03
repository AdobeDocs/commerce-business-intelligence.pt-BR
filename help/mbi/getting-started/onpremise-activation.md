---
title: Ativar o [!DNL MBI] Conta para Assinaturas no Local
description: Saiba como ativar o [!DNL MBI] conta para Assinaturas no Local.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Ativar o [!DNL MBI] Conta para Assinaturas no Local

Para ativar [!DNL MBI] para assinaturas no local, primeiro crie um [!DNL MBI] conta e, em seguida, conectar [!DNL MBI] ao banco de dados do Commerce. Para obter informações sobre a ativação no `Cloud Starter` projetos, consulte [Ativar o [!DNL MBI] Conta para `Cloud Starter` Assinaturas](../getting-started/cloud-activation.md).

1. Crie seu [!DNL MBI] Conta.

   - Vá para o [Logon na conta do Adobe Commerce](https://account.magento.com/customer/account/login)

   - Ir para **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clique em **[!UICONTROL Create Instance]**. Se você não vir esse botão, entre em contato com a equipe de conta do Adobe ou com o consultor técnico do cliente.

   - Insira suas informações para criar sua conta.

   ![](../assets/create-account-2.png)

   - Vá para sua caixa de entrada e verifique seu endereço de email. Se você não recebeu um email, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - Crie sua senha.

   ![](../assets/create-account-4.png)

   - Depois de criar sua conta, você tem a opção de adicionar usuários à nova conta. Agora é possível adicionar administradores técnicos para executar as etapas a seguir.

   ![](../assets/create-account-5.png)

1. Insira informações sobre sua loja para definir suas preferências.

   ![](../assets/create-account-6.png)

1. Conectar [!DNL MBI] ao banco de dados do Commerce usando uma conexão criptografada.

   O Commerce recomenda que você se conecte usando um [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). No entanto, se essa não for uma opção, ainda será possível vincular [!DNL MBI] ao banco de dados usando uma [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Depois de se conectar com êxito [!DNL MBI] ao banco de dados do Commerce, entre em contato com a equipe da conta do Adobe para coordenar as próximas etapas, como a configuração de integrações e outras etapas de configuração.

1. Ao concluir a configuração, você poderá [fazer logon](../getting-started/sign-in.md) ao seu [!DNL MBI] conta.
