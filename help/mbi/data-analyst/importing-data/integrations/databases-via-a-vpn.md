---
title: Conectar bancos de dados via VPN
description: Saiba como conectar bancos de dados via VPN em vez de Túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Conectar bancos de dados via VPN

Embora a Adobe recomende que você conecte seus bancos de dados usando um `SSH tunnel`, você também pode usar um criptografado `VPN` conexão para manter as coisas seguras. A `VPN` pode ser usado para qualquer uma das integrações de banco de dados e, para simplificar, o processo é o mesmo que configurar um `SSH tunnel`:

1. [Criar um [!DNL Commerce Intelligence] usuário do banco de dados](#database)
1. [Criar um [!DNL Commerce Intelligence] Usuário VPN](#vpn)
1. [Permitir acesso à [!DNL Commerce Intelligence] Endereço IP](#allowlist)
1. [Insira a conexão e as informações de usuário da VPN no Commerce Intelligence](#finish)

Além das credenciais do banco de dados, você deve inserir credenciais para um usuário VPN para concluir tudo. Qualquer usuário VPN funciona, mas o Adobe recomenda que você crie um [!DNL Commerce Intelligence] usuário, pois facilita o rastreamento dos usuários em sua conta.

## Criando um usuário do banco de dados para [!DNL Commerce Intelligence] {#database}

O processo de criação de um usuário de banco de dados varia dependendo do tipo de banco de dados ao qual você está se conectando. Para ver as instruções de cada tipo de banco de dados, clique nos links abaixo.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Criação de um `VPN` usuário para [!DNL Commerce Intelligence] {#vpn}

Como mencionado anteriormente, qualquer `VPN` usuário funciona - mas o Adobe recomenda que você crie um usuário exclusivamente para [!DNL Commerce Intelligence] usar.

## Permitir acesso à [!DNL Commerce Intelligence] Endereços IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está no `credentials` página para qualquer integração de banco de dados:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Entrando na conexão e `VPN` informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]. Você deixou o banco de dados? `credentials` abrir página? Caso contrário, acesse **[!UICONTROL Manage Data** > **Connections]**. Clique em **[!UICONTROL Add New Data Source]** e, em seguida, clique no ícone do banco de dados que você está conectando. Não se esqueça de alterar o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com o `Database Connection` seção:

* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] usuário do banco de dados
* `Password`: A senha para o [!DNL Commerce Intelligence] usuário do banco de dados
* `Port`: a porta do banco de dados no servidor. Os padrões são:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: por padrão, é localhost `127.0.0.1`, mas também pode ser o endereço IP público do servidor ou um endereço de rede de área local.
* `Database Name (optional)`: Se você só permitiu o acesso a um banco de dados (isso é especificado durante a etapa de criação do usuário do banco de dados), digite o nome desse banco de dados aqui.

No `Encryption Connection` seção:

* `Encryption Type`: Defina como `Cisco IPsec VPN`
* `Gateway Address`: o endereço IP do servidor VPN
* `Group Name`: O nome do grupo usado para autenticação de grupo
* `Group Secret`: a senha correspondente ao grupo.
* `Username`: A variável [!DNL Commerce Intelligence] `VPN` nome de usuário
* `Password`: A variável [!DNL Commerce Intelligence] `VPN` senha do usuário

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.
