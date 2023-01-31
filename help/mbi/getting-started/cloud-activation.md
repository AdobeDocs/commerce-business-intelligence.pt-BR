---
title: Ative o [!DNL MBI] Conta para assinaturas do Cloud Starter
description: Saiba como ativar [!DNL MBI] para projetos do Cloud Starter.
exl-id: 172439ee-fa1d-4872-b6a9-c61a212a7cbe
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Ative o [!DNL MBI] Conta para `Cloud Starter` Subscrições

Para ativar [!DNL MBI] para `Cloud Starter` projetos, primeiro crie um [!DNL MBI] e, em seguida, crie uma `SSH` e, por fim, conecte-se ao banco de dados do Commerce. Consulte [ativação de assinaturas no local](../getting-started/onpremise-activation.md).

>[!NOTE]
>
>Para obter ajuda na ativação de [!DNL MBI] para `Cloud Pro` projetos, entre em contato com o Gerente de sucesso do cliente ou com o Consultor técnico do cliente.

1. Crie seu [!DNL MBI] Conta.

   - Ir para [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - Ir para **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clique em **[!UICONTROL Create Instance]**. Caso não veja esse botão, entre em contato com o Gerente de sucesso do cliente ou com o Consultor técnico do cliente.

   - Selecione seu `Cloud Starter` assinatura. Se você tiver apenas um `cloud starter` a assinatura será selecionada automaticamente.

   - Clique em **[!UICONTROL Continue]**.

   - Insira suas informações para criar sua conta.

   ![](../assets/create-account-2.png)

   - Vá para a caixa de entrada e verifique seu endereço de email.

   ![](../assets/create-account-3.png)

   - Crie sua senha.

   ![](../assets/create-account-4.png)

   - Depois de criar sua conta, você terá a opção de adicionar usuários a sua nova conta. Agora, administradores técnicos podem ser adicionados para executar as etapas a seguir.

   ![](../assets/create-account-5.png)

1. Insira informações sobre sua loja para definir suas preferências.

   ![](../assets/create-account-6.png)

   Há algumas informações que você precisa coletar antes de poder conectar seu banco de dados para a terceira etapa do fluxo de integração. Você preencherá a `Connect your database` na Etapa 9.

1. Criar dedicado [!DNL MBI] Usuário.

   - Criar um novo usuário em [https://accounts.magento.com](https://accounts.magento.com).

   - _Por que um novo usuário?_ [!DNL MBI] precisa que um usuário adicionado ao projeto busque continuamente novos dados para serem transferidos para a conta [!DNL MBI] data warehouse. Esse usuário servirá como essa conexão. A adição desse usuário ao projeto será feita na Etapa 4.

   - O motivo para ter uma [!DNL MBI] o usuário tem o objetivo de impedir que o usuário adicionado seja desativado ou excluído inadvertidamente e interromper o [!DNL MBI] conexão.

1. Adicionar o usuário recém-criado ao ambiente principal do projeto como um `Contributor`.

   ![](../assets/create-account-7.png)

1. Obtenha seus [!DNL MBI] `SSH` chaves.

   - Vá para o `Connect your database` da página [!DNL MBI] configurar a interface do usuário e rolar para baixo `Encryption settings`.

   - Para o `Encryption Type` , escolha `SSH Tunnel`.

   - Na lista suspensa, é possível copiar e colar o [!DNL MBI] `Public Key`.

   ![](../assets/create-account-8.png)

1. Adicione seu novo [!DNL MBI] `Public key` para [!DNL MBI] usuário criado na Etapa 5.

   - Ir para [https://accounts.magento.cloud/](https://accounts.magento.cloud/). Faça logon com as informações de logon da sua conta para o novo [!DNL MBI] usuário criado. Em seguida, vá para a `Account Settings` guia .

   - Role a página para baixo e expanda a lista suspensa para `SSH` chaves. Em seguida, clique em **[!UICONTROL Add a public key]**.

   ![](../assets/create-account-9.png)

   - Adicione o [!DNL MBI] `SSH Public Key` de cima.

   ![](../assets/create-account-10.png)

1. Fornecer [!DNL MBI] Credenciais do MySQL.

   - Atualize seu `.magento/services.yaml`

   ```sql
   mysql:
       type: mysql:10.0
       disk: 2048
       configuration:
           schemas:
               - main
           endpoints:
               mysql:
                   default_schema: main
                   privileges:
                       main: admin
               mbi:
                   default_schema: main
                   privileges:
                       main: ro
   ```

   - Atualize seu `.magento.app.yaml`

   ```sql
           relationships:
               database: "mysql:mysql"
               mbi: "mysql:mbi"
               redis: "redis:redis"
   ```

1. Obter informações para conectar seu banco de dados ao [!DNL MBI].

   Executar
   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

   para obter informações sobre como conectar seu banco de dados.

   Você deve receber informações semelhantes à saída abaixo:

   ```json
           "mbi" : [
                 {
                    "scheme" : "mysql",
                    "rel" : "mbi",
                    "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                    "query" : {
                       "is_master" : true
                    },
                    "ip" : "169.254.169.143",
                    "path" : "main",
                    "host" : "[!DNL MBI].internal",
                    "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                    "username" : "mbi",
                    "service" : "mysql",
                    "port" : 3306,
                    "password" : "[password]"
                 }
              ],
   ```

1. Conecte seu banco de dados do Commerce

   ![](../assets/create-account-11.png)

   - `Integration Name`: [Escolha um nome para a integração.]

   - `Host`: `[!DNL MBI].internal`

   - `Port`: `3306`

   - `Username`: `mbi`

   - `Password`: [senha de entrada fornecida na saída para a Etapa 8.]

   - `Database Name`: `main`

   - `Table Prefixes`: [deixe em branco se não houver prefixos de tabela]

1. Defina as configurações de fuso horário.

   ![Entradas](../assets/create-account-12.png)

   - `Database`: `Timezone: UTC`

   - `Desired Timezone`: [Escolha o fuso horário em que deseja exibir seus dados.]

1. Obtenha informações sobre as configurações de criptografia.

   - A interface do usuário do projeto fornece um `SSH` sequência de caracteres de acesso. Essa string pode ser usada para coletar as informações necessárias para `Remote Address` e `Username` ao configurar o `Encryption` configurações. Use o `SSH Access` sequência de caracteres encontrada clicando no botão acessar site na ramificação Principal da interface do usuário do projeto e localize `User Name` e `Remote Address` conforme mostrado abaixo.

   ![](../assets/create-account-13.png)

   ![](../assets/create-account-14.png)

1. Informações de entrada para seu `Encryption` configurações

   ![](../assets/create-account-15.png)

   **Entradas**

   - `Encryption Type`: `SSH Tunnel`

   - `Remote Address`: `ssh.us-3.magento.cloud`

   - `Username`: `vfbfui4vmfez6-master-7rqtwti--mymagento`

   - `Port`: `22`

1. Clique em **[!UICONTROL Save Integration]**.

1. Agora você se conectou com êxito ao [!DNL MBI] conta.

1. Depois de se conectar com êxito [!DNL MBI] para seu banco de dados do Commerce, entre em contato com o Gerente de sucesso do cliente para coordenar as próximas etapas, como configurar integrações e outras etapas de configuração.

1. Ao terminar a configuração, você pode [fazer logon](../getting-started/sign-in.md) para [!DNL MBI] conta.
