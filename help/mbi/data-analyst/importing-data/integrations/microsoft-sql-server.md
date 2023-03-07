---
title: Conectar o Microsoft&reg;&reg; SQL Server
description: Saiba como conectar seu banco de dados SQL do Microsoft&reg; ao [!DNL MBI] em um processo de quatro etapas.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Conectar o Microsoft® SQL Server

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Este artigo explica como conectar seu `Microsoft SQL` banco de dados para [!DNL MBI] em um processo de quatro etapas. Esse processo requer alguma experiência técnica relacionada às conexões do servidor e ao SQL, e pode exigir suporte de desenvolvedores em sua equipe.

Compatibilidade com MBI [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]e a maioria dos outros provedores de servidor em nuvem. Se você tiver uma pergunta sobre seu host específico, [enviar um tíquete de suporte](../../../guide-overview.md) solicitando que forneçamos essas informações.

O sistema precisa executar consultas SELECT no banco de dados. Isso é feito inicialmente para obter um instantâneo da estrutura do banco de dados e, em seguida, regularmente ao longo do tempo para manter seus dados atualizados. Suas atualizações são incrementais e Adobe restringem a frequência e o tempo de atualização para evitar qualquer carga indesejada em seu servidor.

A melhor maneira de fazer isso é conectarmos ao seu servidor de banco de dados via TCP/IP. Crie um usuário que possa apenas executar consultas SELECT (e, opcionalmente, só possa selecionar dados das tabelas especificadas). Isso deve ser feito para cada servidor ao qual você está se conectando [!DNL MBI].

## Conectando `Microsoft SQL` para [!DNL MBI]:

1. Verifique se o servidor permite conexões por TCP/IP e autenticação de modo misto.

1. Certifique-se de que o firewall permite a conexão do IP dedicado do servidor.

   Você pode encontrar o endereço IP usado para se conectar ao servidor na seção de conexões do `Settings` página.

1. Crie um usuário que será usado para efetuar login no servidor de banco de dados. Você tem duas opções: por meio de `UI` ou por meio de `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (segundo exemplo)

1. Insira o endereço IP, o nome de usuário e a senha do servidor no [!DNL MBI] em **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Clique em **[!UICONTROL Add a Data Source]**.

1. Selecione para conectar um `Microsoft SQL` banco de dados e insira suas credenciais nos campos da nova `Connections` página.

   Se você estiver usando `Windows Azure`, você também deve especificar um nome de banco de dados.
