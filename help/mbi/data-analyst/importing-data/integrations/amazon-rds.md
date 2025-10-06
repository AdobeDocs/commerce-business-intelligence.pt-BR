---
title: Conectar o Amazon RDS
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Conectar [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] é um serviço de banco de dados gerenciado que é executado em mecanismos de banco de dados com os quais você provavelmente já está familiarizado:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

As etapas para conectar sua instância do [!DNL RDS] variam, dependendo do tipo de banco de dados que você está usando e se você está usando uma conexão criptografada (como um [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), mas estas são as noções básicas.

## Autorizar [!DNL Commerce Intelligence] a acessar seu banco de dados

Na página de credenciais (**[!UICONTROL Manage Data** > **Integrations]**) de cada banco de dados, você verá uma caixa contendo os endereços IP que devem ser autorizados a conectar R[!DNL RDS] a [!DNL Commerce Intelligence]: `54.88.76.97` e `34.250.211.151`. Veja a página `MySQL credentials`, onde você realçou a caixa de endereço IP:

![Configurações do grupo de segurança do Amazon RDS mostrando a configuração do endereço IP](../../../assets/RDS_IP.png)

Para que o [!DNL Commerce Intelligence] se conecte com êxito à instância [!DNL RDS], você deve adicionar esses endereços IP ao grupo de segurança de banco de dados apropriado por meio do console de gerenciamento do AWS. Esses endereços IP podem ser adicionados a um grupo existente ou você pode criar um. O importante é que o grupo esteja autorizado a acessar a instância à qual você deseja se conectar [!DNL Commerce Intelligence].

Ao adicionar os endereços IP [!DNL Commerce Intelligence], adicione um `/32` ao final do endereço para indicar a [!DNL Amazon] que ele é um endereço IP exato. Não se preocupe; a interface do AWS deixa claro que isso é necessário.

## Criar um usuário `Linux` para [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Esta etapa só será necessária se você estiver usando uma conexão criptografada. Para obter instruções sobre como fazer isso, consulte o tópico de configuração do banco de dados que você está usando (por exemplo: MySQL). O usuário `Linux` nos permite criar um `SSH tunnel`, que é o método mais seguro de envio de dados pela Internet.

## Criar um usuário do banco de dados para [!DNL Commerce Intelligence]

Essa é a parte do processo em que, dependendo do banco de dados que você está usando, as etapas variam. A ideia é a mesma, no entanto, você cria um usuário para [!DNL Commerce Intelligence], que é usado para acessar seu banco de dados. As instruções para criar um usuário do banco de dados [!DNL Commerce Intelligence] podem ser encontradas no tópico de configuração para o banco de dados que você está usando.

## Inserir informações de conexão em [!DNL Commerce Intelligence]

Depois de conceder acesso de [!DNL Commerce Intelligence] à sua instância e criar um usuário para nós, a última coisa a fazer é inserir as informações de conexão em [!DNL Commerce Intelligence].

As páginas de credencial para `MySQL`, `Microsoft SQL` e `PostgreSQL` são acessadas através da página `Integrations` (**[!UICONTROL Manage Data** > **Integrations]**) clicando em **[!UICONTROL Add Integration]**. Quando a lista de integrações for exibida, clique no ícone do banco de dados que você está usando para acessar a página de credenciais. Se, atualmente, você não tiver acesso à integração necessária, entre em contato com a equipe de conta da Adobe.

Para concluir a criação da conexão, você precisa das seguintes informações:

* O endereço público da sua instância do RDS: ele pode ser encontrado no console de gerenciamento [!DNL AWS].
* A porta usada pela instância do banco de dados: alguns bancos de dados têm uma porta padrão, que preenche automaticamente o campo `Port`. Essas informações também podem ser encontradas na documentação de configuração do banco de dados.
* O nome de usuário e a senha do usuário que você criou para [!DNL Commerce Intelligence].

Se você estiver usando uma conexão criptografada, altere o botão `Encrypted` na página de credenciais do banco de dados para `Yes`. Isso exibe um formulário extra para configurar a criptografia:

![Formulário de integração do SQL com criptografia habilitada mostrando a opção Sim](../../../assets/sql-integration-encrypted-yes.png)


