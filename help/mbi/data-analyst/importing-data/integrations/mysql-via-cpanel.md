---
title: Conectar MySQL via cPanel
description: Saiba como conectar o MySQL pelo cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/Ou9gOlYKFuoYQHTi7zhyecvfGlKEKF2eRSr5vctsW1s
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 366
ht-degree: 0%

---

# Conectar [!DNL MySQL] via [!DNL cPanel]

* [Criar um usuário  [!DNL Commerce Intelligence] [!DNL MySQL] em  [!DNL cPanel]](#cpanel)
* [Inserir informações de conexão e usuário em  [!DNL Commerce Intelligence]](#finish)

## Ir para

* [[!DNL MySQL] via túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via conexão direta](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>O [!DNL Adobe] recomenda que você use SSH ou alguma outra forma de criptografia para proteger seus dados! Se isso não for uma opção, você ainda poderá conectar o [!DNL Commerce Intelligence] diretamente ao banco de dados usando as instruções neste tópico.

Este tópico orienta você na conexão direta do banco de dados do [!DNL MySQL] ao [!DNL Commerce Intelligence] usando o [!DNL cPanel]. Este processo também pode ser usado para conectar [!DNL Adobe Commerce] e qualquer outro banco de dados de comércio eletrônico baseado em MySQL a [!DNL Commerce Intelligence].

1. Criar um usuário [!DNL Commerce Intelligence] [!DNL MySQL] em [!DNL cPanel]
1. Inserir informações de conexão e usuário em [!DNL Commerce Intelligence]

Comece já.

## Criando um usuário [!DNL Commerce Intelligence] [!DNL MySQL] em [!DNL cPanel] {#cpanel}

1. Faça logon em [!DNL cPanel] por meio de seu provedor de hospedagem.
1. Clique em **[!UICONTROL [!DNL MySQL] Databases]**, localizado na seção `Database`.
1. Role para baixo até a seção `Add New User` e crie um usuário para [!DNL Commerce Intelligence]:

   ![Interface de bancos de dados MySQL do cPanel mostrando a opção criar formulário de usuário](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clique em **[!UICONTROL Create User]**.
1. Agora que você criou o usuário, é necessário associá-lo a um banco de dados. Volte para a seção `Add New User` - veja as configurações para `Add User to Database?`. É disso que você precisa.
1. Na lista suspensa `User` dessa seção, selecione o usuário que você criou.
1. Na lista suspensa `Database` desta seção, selecione o banco de dados ao qual deseja se conectar [!DNL Commerce Intelligence].
1. Clique em **[!UICONTROL Add]**.
1. Quando a lista de verificação de privilégios for exibida, marque a caixa ao lado de `SELECT` - tudo o que [!DNL Commerce Intelligence] precisa para se conectar ao banco de dados.

## Inserindo a conexão e as informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir as informações de conexão e usuário em [!DNL Commerce Intelligence]. Você deixou a página de credenciais [!DNL MySQL] aberta? Caso contrário, vá para **[!UICONTROL Manage Data** > **Connections]**, clique em **[!UICONTROL Add New Data Source]** e depois no ícone [!DNL MySQL].

Insira as seguintes informações nesta página na seção `Database Connection`:

* `Username`: O nome de usuário de [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: A senha para o usuário [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: Porta do MySQL no servidor (`3306` por padrão)
* `Host`: O endereço público do servidor `MySQL` do [!DNL Commerce Intelligence] se conecta ao. Normalmente, esta é a URL que você usa para fazer logon no `[!DNL cPanel]`.

Se você estiver usando um [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), deverá inserir as informações de criptografia. Ajuste o botão `Encrypted` para `Yes` para exibir o formulário.

* `Connection Type`: Defina como `SSH Tunnel`
* `Remote Address`: O endereço IP ou o nome de host do servidor [!DNL Commerce Intelligence] será encapsulado em
* `Username`: O nome de usuário de [!DNL Commerce Intelligence] `SSH (Linux)`, veja [instruções](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre como fazer isso, se você ainda não tiver feito isso)
* `SSH Port`: Porta SSH no servidor (`22` por padrão)

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a instalação.

## Relacionados:

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
