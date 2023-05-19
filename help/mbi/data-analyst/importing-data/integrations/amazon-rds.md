---
title: Conectar o Amazon RDS
description: Saiba mais sobre as etapas para conectar sua instância do RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Conectar [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] é um serviço de banco de dados gerenciado que é executado em mecanismos de banco de dados com os quais você provavelmente já está familiarizado:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

As etapas para conectar seu [!DNL RDS] dependendo do tipo de banco de dados que você está usando e se você está usando uma conexão criptografada (como uma [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), mas eis o básico.

## Autorizar [!DNL Commerce Intelligence] para acessar seu banco de dados

Na página de credenciais (**[!UICONTROL Manage Data** > **Integrations]**) para cada banco de dados, você verá uma caixa contendo os endereços IP que devem ser autorizados a conectar o R[!DNL RDS] para [!DNL Commerce Intelligence]: `54.88.76.97` e `34.250.211.151`. Aqui está uma visão do `MySQL credentials` , onde você realçou a caixa de endereço IP:

![](../../../assets/RDS_IP.png)

Para [!DNL Commerce Intelligence] para se conectar com sucesso ao seu [!DNL RDS] você deve adicionar esses endereços IP ao grupo de segurança de banco de dados apropriado por meio do console de gerenciamento do AWS. Esses endereços IP podem ser adicionados a um grupo existente ou você pode criar um. O importante é que o grupo esteja autorizado a acessar a instância à qual deseja se conectar [!DNL Commerce Intelligence].

Ao adicionar a variável [!DNL Commerce Intelligence] Endereços IP, certifique-se de adicionar um `/32` ao final do endereço para indicar a [!DNL Amazon] que é um endereço IP exato. Não se preocupe; a interface do AWS deixa claro que isso é necessário.

## Criar um `Linux` usuário para [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Esta etapa só será necessária se você estiver usando uma conexão criptografada. Para obter instruções sobre como fazer isso, consulte o tópico de configuração do banco de dados que você está usando (por exemplo: MySQL). A variável `Linux` o usuário nos permite criar um `SSH tunnel`, que é o método mais seguro de envio de dados pela Internet.

## Criar um usuário do banco de dados para [!DNL Commerce Intelligence]

Essa é a parte do processo em que, dependendo do banco de dados que você está usando, as etapas variam. A ideia é a mesma, no entanto, você cria um usuário para [!DNL Commerce Intelligence] que é usado para acessar seu banco de dados. Instruções para a criação de um banco de dados [!DNL Commerce Intelligence] usuário pode ser encontrado no tópico de configuração do banco de dados que você está usando.

## Insira as informações de conexão em [!DNL Commerce Intelligence]

Depois de conceder [!DNL Commerce Intelligence] acesso à sua instância e criou um usuário para nós, a última coisa que você precisa fazer é inserir as informações de conexão em [!DNL Commerce Intelligence].

As páginas de credencial para `MySQL`, `Microsoft SQL`, e `PostgreSQL` são acessados por meio da `Integrations` página (**[!UICONTROL Manage Data** > **Integrations]**) clicando em **[!UICONTROL Add Integration]**. Quando a lista de integrações for exibida, clique no ícone do banco de dados que você está usando para acessar a página de credenciais. Se, atualmente, você não tiver acesso à integração necessária, entre em contato com a equipe de conta do Adobe.

Para concluir a criação da conexão, você precisa das seguintes informações:

* O endereço público da sua instância do RDS: ele pode ser encontrado no [!DNL AWS] console de gerenciamento.
* A porta usada pela instância do banco de dados: alguns bancos de dados têm uma porta padrão, que preenche automaticamente a `Port` campo. Essas informações também podem ser encontradas na documentação de configuração do banco de dados.
* O nome de usuário e a senha do usuário para o qual você criou [!DNL Commerce Intelligence].

Se você estiver usando uma conexão criptografada, altere o `Encrypted` alterne a página credenciais do banco de dados para `Yes`. Isso exibe um formulário extra para configurar a criptografia:

![](../../../assets/sql-integration-encrypted-yes.png)


