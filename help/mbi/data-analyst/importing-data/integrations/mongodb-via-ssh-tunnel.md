---
title: Conectar [!DNL MongoDB] via túnel SSH
description: Saiba como se conectar [!DNL MongoDB] via túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Conectar [!DNL MongoDB] via túnel SSH

Para conectar o banco de dados do [!DNL MongoDB] ao [!DNL Commerce Intelligence] por meio de um túnel SSH, faça o seguinte:

1. [Recuperar a  [!DNL Commerce Intelligence] chave pública](#retrieve)
1. [Permitir acesso ao endereço IP  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
1. [Criar um usuário do Linux para o Commerce Intelligence](#linux)
1. [Criar um  [!DNL MongoDB] usuário para o Commerce Intelligence](#mongodb)
1. [Insira as informações de conexão e usuário em  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Devido à natureza técnica dessa configuração, a Adobe recomenda que você faça um loop em um desenvolvedor para ajudar caso ainda não tenha feito isso.

## Recuperando a chave pública [!DNL Commerce Intelligence] {#retrieve}

O `public key` é usado para autorizar o usuário [!DNL Commerce Intelligence] `Linux`. A próxima seção aborda a criação do usuário e a importação das chaves.

1. Vá para **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique no ícone [!DNL MONGODB].
1. Depois que a página de credenciais do [!DNL MongoDB] for aberta, altere a opção `Encrypted` para `Yes`. Isso exibe o formulário de configuração SSH.
1. O `public key` está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Se você perder um pouco, veja como navegar pelo [!DNL Commerce Intelligence] para recuperar a chave:

![Recuperando a chave pública de RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permitir acesso ao endereço IP [!DNL Commerce Intelligence] {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também estão na página de credenciais [!DNL MongoDB]:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criando um usuário `Linux` para [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Se o arquivo `sshd_config` associado ao servidor não estiver definido como a opção padrão, somente determinados usuários terão acesso ao servidor; isso impede uma conexão bem-sucedida com o [!DNL Commerce Intelligence]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o usuário `rjmetric` acesse o servidor.

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode restringir esse usuário da maneira que desejar, contanto que ele mantenha o direito de se conectar ao servidor [!DNL MongoDB].

Para adicionar o novo usuário, execute os seguintes comandos como raiz no servidor `Linux`:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Lembra do `public key` que você recuperou na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, você precisa importar a chave para `authorized_keys`. Copie toda a chave no arquivo `authorized_keys` da seguinte maneira:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para concluir a criação do usuário, altere as permissões no diretório /home/rjmetric para permitir acesso via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Criando um usuário [!DNL Commerce Intelligence] [!DNL MongoDB] {#mongodb}

[!DNL MongoDB] servidores têm dois modos de execução - [um com a opção &quot;auth&quot;](#auth) `(mongod -- auth)` e outro sem, [que é o padrão](#default). As etapas para criar um usuário [!DNL MongoDB] variam de acordo com o modo que seu servidor está usando. Certifique-se de verificar o modo antes de continuar.

### Se o servidor usar a Opção `Auth`: {#auth}

Ao se conectar a vários bancos de dados, você pode adicionar o usuário fazendo logon em [!DNL MongoDB] como um usuário administrador e executando os comandos a seguir.

>[!NOTE]
>
>Para ver todos os bancos de dados disponíveis, o usuário [!DNL Commerce Intelligence] requer as permissões para executar `listDatabases.`

Este comando concede ao usuário [!DNL Commerce Intelligence] acesso `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use este comando para conceder ao usuário [!DNL Commerce Intelligence] acesso `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Isso imprime uma resposta com esta aparência:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Se o servidor usar a opção padrão, {#default}

Se o servidor não usar o modo `auth`, o servidor [!DNL MongoDB] poderá ser acessado mesmo sem um nome de usuário e uma senha. No entanto, você deve garantir que o arquivo `mongodb.conf` `(/etc/mongodb.conf)` tenha as seguintes linhas; caso contrário, reinicie o servidor depois de adicioná-las.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para associar o servidor [!DNL MongoDB] a um endereço diferente, ajuste o nome de host do banco de dados na próxima etapa de acordo.

## Inserindo a conexão e as informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir as informações de conexão e usuário em [!DNL Commerce Intelligence]. Você deixou a página de credenciais [!DNL MongoDB] aberta? Caso contrário, vá para **[!UICONTROL Data > Connections]**, clique em **[!UICONTROL Add New Data Source]** e depois no ícone [!DNL MongoDB]. Não se esqueça de alterar a opção `Encrypted` para `Yes`.

Insira as seguintes informações nesta página, começando com a seção `Database Connection`:

* `Host`: `127.0.0.1`
* `Username`: O nome de usuário [!DNL Commerce Intelligence] [!DNL MongoDB] (deveria ser `rjmetric`)
* `Password`: A senha de [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port`: porta do MongoDB no seu servidor (`27017` por padrão)
* `Database Name` (Opcional): Se você só permitiu acesso a um banco de dados, especifique o nome desse banco de dados aqui.

Na seção `SSH Connection`:

* `Remote Address`: O endereço IP ou o nome de host do servidor no qual você fará SSH
* `Username`: O nome de usuário do Linux [!DNL Commerce Intelligence] (SSH) (deve ser rjmetric)
* `SSH Port`: a porta SSH no servidor (22 por padrão)

Quando terminar, clique em **[!UICONTROL Save Test]** para concluir a instalação.

### Relacionados

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
