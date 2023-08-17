---
title: Conectar MySQL via cPanel
description: Saiba como conectar o MySQL pelo cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---

# Conectar [!DNL MySQL] via [!DNL cPanel]

* [Criar um [!DNL Commerce Intelligence] [!DNL MySQL] usuário em [!DNL cPanel]](#cpanel)
* [Insira as informações de conexão e usuário em [!DNL Commerce Intelligence]](#finish)

## Ir para

* [[!DNL MySQL] via túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via conexão direta](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] A recomenda que você use SSH ou alguma outra forma de criptografia para proteger seus dados! Se isso não for uma opção, você ainda poderá se conectar diretamente [!DNL Commerce Intelligence] ao banco de dados usando as instruções neste tópico.

Este tópico orienta você na conexão direta com o [!DNL MySQL] banco de dados para [!DNL Commerce Intelligence] usar [!DNL cPanel]. Esse processo também pode ser usado para conectar [!DNL Adobe Commerce] e qualquer outro banco de dados de comércio eletrônico baseado em MySQL para [!DNL Commerce Intelligence].

1. Criar um [!DNL Commerce Intelligence] [!DNL MySQL] usuário em [!DNL cPanel]
1. Insira as informações de conexão e usuário em [!DNL Commerce Intelligence]

Introdução.

## Criação de um [!DNL Commerce Intelligence] [!DNL MySQL] usuário em [!DNL cPanel] {#cpanel}

1. Efetue logon no [!DNL cPanel] por meio de seu provedor de hospedagem.
1. Clique em **[!UICONTROL [!DNL MySQL] Databases]**, localizado na `Database` seção.
1. Role para baixo até `Add New User` e criar um usuário para [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clique em **[!UICONTROL Create User]**.
1. Agora que você criou o usuário, é necessário associá-lo a um banco de dados. Volte para o `Add New User` seção - consulte as configurações de `Add User to Database?` Isso é o que você precisa.
1. No `User` nesta seção, selecione o usuário que você criou.
1. No `Database` lista suspensa desta seção, selecione o banco de dados ao qual deseja se conectar [!DNL Commerce Intelligence].
1. Clique em **[!UICONTROL Add]**.
1. Quando a lista de verificação de privilégios for exibida, marque a caixa ao lado de `SELECT` - isso é tudo [!DNL Commerce Intelligence] precisa se conectar ao banco de dados.

## Inserção das informações de conexão e usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]. Você deixou o [!DNL MySQL] página de credenciais aberta? Caso contrário, acesse **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o [!DNL MySQL] ícone.

Insira as seguintes informações nesta página nas `Database Connection` seção:

* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Password`: A senha para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Port`: porta do MySQL no servidor (`3306` por padrão)
* `Host`: O endereço público do `MySQL` server [!DNL Commerce Intelligence] conecta-se ao. Normalmente, esse é o URL usado para fazer logon no `[!DNL cPanel]`.

Se você estiver usando um [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), você deve inserir as informações de criptografia. Defina o `Encrypted` alternar para `Yes` para exibir o formulário.

* `Connection Type`: Defina como `SSH Tunnel`
* `Remote Address`: O endereço IP ou o nome de host do servidor [!DNL Commerce Intelligence] encaminhará por túnel para
* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] `SSH (Linux)` usuário, consulte [instruções](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre como fazer isso, se você ainda não tiver feito)
* `SSH Port`: porta SSH no servidor (`22` por padrão)

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Relacionados:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
