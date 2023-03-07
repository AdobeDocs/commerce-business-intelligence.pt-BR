---
title: Conectar MySQL via cPanel
description: Saiba como conectar o MySQL pelo cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Conectar MySQL via cPanel

* [Criar um [!DNL MBI] Usuário MySQL no cPanel](#cpanel)
* [Inserir informações de conexão e usuário no MBI](#finish)

## Ir para

* [MySQL via túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL via conexão direta](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>A Adobe recomenda que você use SSH ou alguma outra forma de criptografia para proteger seus dados! Se isso não for uma opção, você ainda poderá se conectar diretamente [!DNL MBI] ao banco de dados usando as instruções deste artigo.

Este artigo o orienta pela conexão direta do banco de dados MySQL com o [!DNL MBI] usar `cPanel`. Esse processo também pode ser usado para conectar [!DNL Adobe Commerce] e qualquer outro banco de dados de comércio eletrônico baseado em MySQL para [!DNL MBI].

1. Criar um [!DNL MBI] Usuário MySQL em `cPanel`
1. Insira as informações de conexão e usuário em [!DNL MBI]

Comece já.

## Criação de um [!DNL MBI] Usuário MySQL em `cPanel` {#cpanel}

1. Efetue logon no [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) por meio de seu provedor de hospedagem.
1. Clique em **[!UICONTROL MySQL Databases]**, localizado na `Database` seção.
1. Role para baixo até `Add New User` e criar um usuário para [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clique em **[!UICONTROL Create User]**.
1. Agora que você criou o usuário, é necessário associá-lo a um banco de dados. Volte para o `Add New User` seção - consulte as configurações de `Add User to Database?` Isso é o que você precisa.
1. No `User` nesta seção, selecione o usuário que você criou.
1. No `Database` lista suspensa desta seção, selecione o banco de dados ao qual deseja se conectar [!DNL MBI].
1. Clique em **[!UICONTROL Add]**.
1. Quando a lista de verificação de privilégios for exibida, marque a caixa ao lado de `SELECT` - isso é tudo [!DNL MBI] precisa se conectar ao banco de dados.

## Inserção das informações de conexão e usuário em [!DNL MBI] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais do MySQL aberta? Caso contrário, acesse **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o ícone MySQL.

Insira as seguintes informações nesta página nas `Database Connection` seção:

* `Username`: O nome de usuário para o [!DNL MBI] Usuário MySQL
* `Password`: A senha para o [!DNL MBI] Usuário MySQL
* `Port`: porta do MySQL no servidor (`3306` por padrão)
* `Host`: O endereço público do `MySQL` server [!DNL MBI] conecta-se ao. Normalmente, esse é o URL usado para fazer logon no `cPanel`.

Se você estiver usando um [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), você deve inserir as informações de criptografia. Defina o `Encrypted` alternar para `Yes` para exibir o formulário.

* `Connection Type`: Defina como `SSH Tunnel`
* `Remote Address`: O endereço IP ou o nome de host do servidor [!DNL MBI] encaminhará por túnel para
* `Username`: O nome de usuário para o [!DNL MBI] `SSH (Linux)` usuário, consulte [instruções](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre como fazer isso, se você ainda não tiver feito)
* `SSH Port`: porta SSH no servidor (`22` por padrão)

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Relacionados:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
