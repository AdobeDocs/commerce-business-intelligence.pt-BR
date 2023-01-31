---
title: Conectar MySQL via cPanel
description: Saiba como conectar o MySQL via Painel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Conectar MySQL via cPanel

* [Crie um [!DNL MBI] Usuário do MySQL no cPanel](#cpanel)
* [Inserir informações de conexão e do usuário no MBI](#finish)

## Ir para

* [MySQL via túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL via conexão direta](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>É altamente recomendável usar SSH ou alguma outra forma de criptografia para proteger seus dados! Se essa não for uma opção, você ainda poderá se conectar diretamente [!DNL MBI] ao seu banco de dados usando as instruções deste artigo.

Neste artigo, o orientamos a conectar diretamente o banco de dados do MySQL ao [!DNL MBI] usando o cPanel&quot;. Esse processo também pode ser usado para conexão [!DNL Magento] e qualquer outro banco de dados de comércio eletrônico baseado em MySQL para [!DNL MBI].

1. Crie um [!DNL MBI] Usuário do MySQL em `cPanel`
1. Insira as informações da conexão e do usuário em [!DNL MBI]

Comece já.

## Criação de um [!DNL MBI] Usuário do MySQL em `cPanel` {#cpanel}

1. Faça logon em [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) por seu provedor de hospedagem.
1. Clique em **[!UICONTROL MySQL Databases]**, localizada na `Database` seção.
1. Role para baixo até a `Add New User` e criar um usuário para [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clique em **[!UICONTROL Create User]**.
1. Agora que você criou o usuário, é necessário associá-lo a um banco de dados. Volte para o `Add New User` seção - consulte as configurações para `Add User to Database?` É disso que precisamos.
1. No `User` na lista suspensa desta seção, selecione o usuário que você criou.
1. No `Database` na lista suspensa desta seção, selecione o banco de dados ao qual deseja se conectar [!DNL MBI].
1. Clique em **[!UICONTROL Add]**.
1. Quando a lista de verificação de privilégios for exibida, marque a caixa ao lado de `SELECT` - é tudo [!DNL MBI] precisa se conectar ao banco de dados.

## Inserir a conexão e as informações do usuário em [!DNL MBI] {#finish}

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais do MySQL aberta? Caso contrário, acesse **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o ícone MySQL .

Insira as seguintes informações nesta página no `Database Connection` seção:

* `Username`: O nome de usuário para a [!DNL MBI] Usuário do MySQL
* `Password`: A senha do [!DNL MBI] Usuário do MySQL
* `Port`: Porta do MySQL no seu servidor (`3306` por padrão)
* `Host`: O endereço público da `MySQL` server [!DNL MBI] se conectará a. Esse é geralmente o URL usado para fazer logon `cPanel`.

Se estiver usando um [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), também será necessário inserir as informações de criptografia. Defina as `Encrypted` alternar para `Yes` para exibir o formulário.

* `Connection Type`: Defina como `SSH Tunnel`
* `Remote Address`: O endereço IP ou o nome do host do servidor [!DNL MBI] encapsulará
* `Username`: O nome de usuário para a [!DNL MBI] `SSH (Linux)` usuário, consulte [instruções](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre como fazer isso, se ainda não tiver feito)
* `SSH Port`: Porta SSH em seu servidor (`22` por padrão)

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Relacionadas:

* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
