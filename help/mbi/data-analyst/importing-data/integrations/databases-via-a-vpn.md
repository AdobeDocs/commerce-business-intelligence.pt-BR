---
title: Conectar bancos de dados via VPN
description: Saiba como conectar bancos de dados via VPN em vez de Túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Conectar bancos de dados via VPN

Embora a Adobe recomende que você conecte seus bancos de dados usando um `SSH tunnel`, você também pode usar uma conexão `VPN` criptografada para manter as coisas seguras. Um `VPN` pode ser usado para qualquer uma de suas integrações de banco de dados e, para simplificar, o processo é o mesmo que configurar um `SSH tunnel`:

1. [Criar um usuário do banco de dados  [!DNL Commerce Intelligence] &#x200B;](#database)
1. [Criar um  [!DNL Commerce Intelligence] usuário VPN](#vpn)
1. [Permitir acesso ao endereço IP  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
1. [Insira a conexão e as informações de usuário da VPN no Commerce Intelligence](#finish)

Além das credenciais do banco de dados, você deve inserir credenciais para um usuário VPN para concluir tudo. Qualquer usuário VPN funciona, mas a Adobe recomenda que você crie um usuário [!DNL Commerce Intelligence], pois isso facilita o rastreamento dos usuários em sua conta.

## Criando um usuário de banco de dados para [!DNL Commerce Intelligence] {#database}

O processo de criação de um usuário de banco de dados varia dependendo do tipo de banco de dados ao qual você está se conectando. Para ver as instruções de cada tipo de banco de dados, clique nos links abaixo.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Criando um usuário `VPN` para [!DNL Commerce Intelligence] {#vpn}

Como mencionado anteriormente, qualquer usuário válido do `VPN` funciona, mas a Adobe recomenda que você crie um usuário exclusivamente para uso do [!DNL Commerce Intelligence].

## Permitir acesso aos endereços IP [!DNL Commerce Intelligence] {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também estão na página `credentials` para qualquer integração de banco de dados:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Entrando na conexão e `VPN` informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir as informações de conexão e usuário em [!DNL Commerce Intelligence]. Você deixou a página `credentials` do banco de dados aberta? Caso contrário, vá para **[!UICONTROL Manage Data** > **Connections]**. Clique em **[!UICONTROL Add New Data Source]** e depois no ícone do banco de dados ao qual você está se conectando. Não se esqueça de alterar a opção `Encrypted` para `Yes`.

Insira as seguintes informações nesta página, começando com a seção `Database Connection`:

* `Username`: O nome de usuário para o usuário do banco de dados [!DNL Commerce Intelligence]
* `Password`: A senha do usuário do banco de dados [!DNL Commerce Intelligence]
* `Port`: a porta do banco de dados no servidor. Os padrões são:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: por padrão, este é o host local `127.0.0.1`, mas também pode ser o endereço IP público do servidor ou um endereço de rede local.
* `Database Name (optional)`: Se você só permitiu acesso a um banco de dados (isso é especificado durante a etapa de criação do usuário do banco de dados), digite o nome desse banco de dados aqui.

Na seção `Encryption Connection`:

* `Encryption Type`: Defina como `Cisco IPsec VPN`
* `Gateway Address`: O endereço IP do servidor VPN
* `Group Name`: O nome do grupo usado para autenticação de grupo
* `Group Secret`: a senha correspondente ao grupo.
* `Username`: O nome de usuário [!DNL Commerce Intelligence] `VPN`
* `Password`: A senha de usuário [!DNL Commerce Intelligence] `VPN`

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a instalação.
