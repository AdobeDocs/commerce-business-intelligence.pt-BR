---
title: Conectar o Microsoft SQL Server
description: Saiba como conectar o banco de dados SQL do Microsoft ao [!DNL MBI] em um processo de quatro etapas.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Conectar o Microsoft SQL Server

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Este artigo explica como conectar seu `Microsoft SQL` banco de dados para [!DNL MBI] em um processo de quatro etapas. Esse processo requer alguma experiência técnica relacionada às conexões do servidor e ao SQL, e pode exigir suporte dos desenvolvedores de sua equipe.

Apoiamos [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]e a maioria dos outros provedores de servidor de nuvem. Se você tiver uma dúvida sobre seu host específico, [enviar um tíquete de suporte](../../../guide-overview.md) pedindo-nos que fornecêssemos estas informações.

Nosso sistema precisa executar consultas SELECT no banco de dados. Fazemos isso inicialmente para obter um instantâneo da estrutura do seu banco de dados e, em seguida, horas extras regularmente para manter nossos dados atualizados. Nossas atualizações são incrementais e restringimos a frequência e o tempo de atualização para evitar qualquer carga indesejada em seu servidor.

A melhor maneira de fazer isso é conectarmos seu servidor de banco de dados via TCP/IP. Crie um usuário para nós que só possa executar consultas SELECT (e, opcionalmente, só poderá selecionar dados a partir das tabelas especificadas). Isso precisa ser feito para cada um dos servidores aos quais você se conectará [!DNL MBI].

## Conexão `Microsoft SQL` para [!DNL MBI]:

1. Certifique-se de que o servidor permite ligações através de autenticação TCP/IP e modo misto.

1. Certifique-se de que o firewall permitirá a conexão do IP dedicado do servidor.

   Você pode encontrar o endereço IP que usaremos para se conectar ao seu servidor na seção de conexões de seu `Settings` página.

1. Crie um usuário que usaremos para fazer logon no servidor de banco de dados.  Você tem duas opções; ou `UI` ou através de `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (segundo exemplo)

1. Insira o endereço IP do servidor, o nome de usuário e a senha em [!DNL MBI] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Clique em **[!UICONTROL Add a Data Source]**.

1. Selecione para conectar um `Microsoft SQL` e insira suas credenciais nos campos do novo `Connections` página.

   Se estiver usando `Windows Azure`, também é necessário especificar um nome de banco de dados.
