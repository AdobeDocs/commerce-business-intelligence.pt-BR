---
title: Conectar bancos de dados via VPN
description: Saiba como conectar bancos de dados via VPN em vez do túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Conectar bancos de dados via VPN

Embora recomendemos que você conecte seus bancos de dados usando um túnel SSH, também pode usar uma conexão VPN criptografada para manter as coisas seguras. A `VPN` pode ser usado para qualquer uma de nossas integrações de banco de dados e, para simplificar, o processo é quase o mesmo que configurar um `SSH tunnel`:

1. [Crie um [!DNL MBI] usuário do banco de dados](#database)
1. [Crie um [!DNL MBI] Usuário VPN](#vpn)
1. [Permitir acesso ao [!DNL MBI] Endereço IP](#allowlist)
1. [Introduza a ligação e as informações do utilizador VPN no MBI](#finish)

Além das credenciais do banco de dados, você terá que inserir credenciais para que um usuário da VPN conclua tudo. Qualquer usuário de VPN funcionará, mas recomendamos que você crie um [!DNL MBI] usuário - facilita o rastreamento dos usuários em sua conta.

Vamos começar.

## Criando um usuário de banco de dados para [!DNL MBI] {#database}

O processo para criar um usuário de banco de dados varia dependendo do tipo de banco de dados que você está conectando. Para ver as instruções para cada tipo de banco de dados, clique nos links abaixo.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Criação de um `VPN` usuário para [!DNL MBI] {#vpn}

Como já referimos, qualquer `VPN` o usuário funcionará, mas recomendamos que você crie um usuário somente para [!DNL MBI] use.

## Permitir acesso ao [!DNL MBI] Endereços IP {#allowlist}

Para que a conexão seja bem-sucedida, é necessário configurar o firewall para permitir o acesso dos endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está no `credentials` para qualquer integração de banco de dados:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Inserir a conexão e `VPN` informações do usuário em [!DNL MBI] {#finish}

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou o banco de dados `credentials` página aberta? Caso contrário, acesse **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, em seguida, o ícone do banco de dados que você está conectando. não se esqueça de mudar a `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com `Database Connection` seção:

* `Username`: O nome de usuário para a [!DNL MBI] usuário do banco de dados
* `Password`: A senha do [!DNL MBI] usuário do banco de dados
* `Port`: A porta do banco de dados no seu servidor. Os padrões são:
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: Por padrão, será host local `127.0.0.1`, mas também pode ser o endereço IP público do seu servidor ou um endereço de rede local.
* `Database Name (optional)`: Se você permitiu acesso somente a um banco de dados (isso é especificado durante a etapa de criação do usuário do banco de dados), digite o nome desse banco de dados aqui.

Em `Encryption Connection` seção:

* `Encryption Type`: Defina como `Cisco IPsec VPN`
* `Gateway Address`: O endereço IP do servidor VPN
* `Group Name`: O nome do grupo usado para autenticação de grupo
* `Group Secret`: A senha correspondente ao grupo.
* `Username`: O [!DNL MBI] `VPN` username
* `Password`: O [!DNL MBI] `VPN` senha do usuário

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.
