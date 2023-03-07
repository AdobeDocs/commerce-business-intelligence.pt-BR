---
title: Conectar o Amazon RDS
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Conectar o Amazon RDS

O Amazon Relational Database Services (RDS) é um serviço de banco de dados gerenciado que é executado em mecanismos de banco de dados com os quais você provavelmente já está familiarizado - [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft® SQL]](../integrations/microsoft-sql-server.md), e [[!DNL PostgreSQ]](../integrations/postgresql.md).

As etapas para conectar a instância do RDS variam, dependendo do tipo de banco de dados que você está usando e se você está usando uma conexão criptografada (como uma [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), mas veja as noções básicas:

## Autorizar [!DNL MBI] para acessar seu banco de dados

Na página de credenciais (**[!UICONTROL Manage Data** > **Integrations]**) para cada banco de dados, você verá uma caixa contendo os endereços IP que devem ser autorizados a conectar o RDS ao MBI: `54.88.76.97` e `34.250.211.151`. Aqui está uma visão do `MySQL credentials` , onde você realçou a caixa de endereço IP:

![](../../../assets/RDS_IP.png)

Para [!DNL MBI] para se conectar com êxito à instância do RDS, você deve adicionar esses endereços IP ao grupo de segurança de banco de dados apropriado por meio do console de gerenciamento do AWS. Esses endereços IP podem ser adicionados a um grupo existente ou você pode criar um. O importante é que o grupo esteja autorizado a acessar a instância à qual deseja se conectar [!DNL MBI].

Ao adicionar a variável [!DNL MBI] Endereços IP, certifique-se de adicionar um `/32` ao final do endereço para indicar à Amazon que ele é um endereço IP exato. Não se preocupe; a interface do AWS deixa claro que isso é necessário.

## Criar um `Linux` usuário para [!DNL MBI] {#linux}

>[!NOTE]
>
>Esta etapa só será necessária se você estiver usando uma conexão criptografada. Para obter instruções sobre como fazer isso, consulte o artigo de configuração do banco de dados que você está usando (por exemplo: MySQL). A variável `Linux` o usuário nos permite criar um `SSH tunnel`, que é o método mais seguro de envio de dados pela Internet.

## Criar um usuário do banco de dados para o MBI

Essa é a parte do processo em que, dependendo do banco de dados que você está usando, as etapas variam. No entanto, a ideia é a mesma: criar um usuário para [!DNL MBI] que é usado para acessar seu banco de dados. Instruções para a criação de um banco de dados [!DNL MBI] usuário pode ser encontrado no artigo de configuração do banco de dados que você está usando.

## Inserir informações de conexão no MBI

Depois de conceder [!DNL MBI] acesso à sua instância e criou um usuário para nós, a última coisa que você precisa fazer é inserir as informações de conexão em [!DNL MBI].

As páginas de credencial para `MySQL`, `Microsoft SQL`, e `PostgreSQL` são acessados por meio da `Integrations` página (**[!UICONTROL Manage Data** > **Integrations]**) clicando em **[!UICONTROL Add Integration]**. Quando a lista de integrações for exibida, clique no ícone do banco de dados que você está usando para acessar a página de credenciais. Se, atualmente, você não tiver acesso à integração necessária, entre em contato com a equipe de conta do Adobe.

Para concluir a criação da conexão, você precisa das seguintes informações:

* O endereço público da sua instância do RDS: ele pode ser encontrado no console de gerenciamento do AWS.
* A porta usada pela instância do banco de dados: alguns bancos de dados têm uma porta padrão, que preenche automaticamente a `Port` campo. Essas informações também podem ser encontradas na documentação de configuração do banco de dados.
* O nome de usuário e a senha do usuário para o qual você criou [!DNL MBI].

Se você estiver usando uma conexão criptografada, altere o `Encrypted` alterne a página credenciais do banco de dados para `Yes`. Isso exibe um formulário extra para configurar a criptografia:

![](../../../assets/sql-integration-encrypted-yes.png)

Isso é tudo! A conexão da instância do RDS foi concluída.
