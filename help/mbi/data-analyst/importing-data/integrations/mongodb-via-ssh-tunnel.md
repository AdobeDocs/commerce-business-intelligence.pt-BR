---
title: Conectar [!DNL MongoDB] via túnel SSH
description: Saiba como se conectar [!DNL MongoDB] via túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Conectar [!DNL MongoDB] via Túnel SSH

Para conectar seu [!DNL MongoDB] banco de dados para [!DNL Commerce Intelligence] por meio de um túnel SSH, você deve fazer algumas coisas:

1. [Recuperar o [!DNL Commerce Intelligence] chave pública](#retrieve)
1. [Permitir acesso à [!DNL Commerce Intelligence] Endereço IP](#allowlist)
1. [Criar um usuário do Linux para Commerce Intelligence](#linux)
1. [Criar um [!DNL MongoDB] usuário para Commerce Intelligence](#mongodb)
1. [Insira a conexão e as informações do usuário em [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Devido à natureza técnica dessa configuração, o Adobe recomenda que você faça o loop em um desenvolvedor para ajudar se você não tiver feito isso antes.

## Recuperação de [!DNL Commerce Intelligence] chave pública {#retrieve}

A variável `public key` é usado para autorizar a [!DNL Commerce Intelligence] `Linux` usuário. A próxima seção aborda a criação do usuário e a importação das chaves.

1. Ir para **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique em [!DNL MONGODB] ícone.
1. Depois que a variável [!DNL MongoDB] credenciais for aberta, altere a `Encrypted` alternar para `Yes`. Isso exibe o formulário de configuração SSH.
1. A variável `public key` O está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Se você está um pouco perdido, veja como navegar [!DNL Commerce Intelligence] para recuperar a chave:

![Recuperando a chave pública de RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permitir acesso à [!DNL Commerce Intelligence] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está no [!DNL MongoDB] página de credenciais:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criação de um `Linux` usuário para [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Se a variável `sshd_config` o arquivo associado ao servidor não está definido como a opção padrão, somente determinados usuários têm acesso ao servidor - isso impede uma conexão bem-sucedida com o [!DNL Commerce Intelligence]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o `rjmetric` acesso do usuário ao servidor.

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode restringir esse usuário da maneira que desejar, contanto que ele mantenha o direito de se conectar à [!DNL MongoDB] servidor.

Para adicionar o novo usuário, execute os seguintes comandos como root em seu `Linux` servidor:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Lembre-se do `public key` você recuperou na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, é necessário importar a chave para o `authorized_keys`. Copie toda a chave na `authorized_keys` do seguinte modo:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para concluir a criação do usuário, altere as permissões no diretório /home/rjmetric para permitir acesso via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Criação de um [!DNL Commerce Intelligence] [!DNL MongoDB] usuário {#mongodb}

[!DNL MongoDB] os servidores têm dois modos de execução - [um com a opção &quot;auth&quot;](#auth) `(mongod -- auth)` e um sem, [que é o padrão](#default). As etapas para criar um [!DNL MongoDB] O usuário varia de acordo com o modo usado pelo servidor. Certifique-se de verificar o modo antes de continuar.

### Se o servidor usar a variável `Auth` Opção: {#auth}

Ao conectar-se a vários bancos de dados, você pode adicionar o usuário efetuando login no [!DNL MongoDB] como um usuário administrador e executando os comandos a seguir.

>[!NOTE]
>
>Para ver todos os bancos de dados disponíveis, a variável [!DNL Commerce Intelligence] o usuário requer permissões para executar `listDatabases.`

Esse comando concede a [!DNL Commerce Intelligence] acesso do usuário `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use este comando para conceder a [!DNL Commerce Intelligence] acesso do usuário `to a single database`:

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

Se o servidor não usar `auth` modo, seu [!DNL MongoDB] o servidor pode ser acessado mesmo sem um nome de usuário e senha. No entanto, você deve garantir a `mongodb.conf` arquivo `(/etc/mongodb.conf)` O tem as seguintes linhas - caso contrário, reinicie o servidor depois de adicioná-las.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para vincular o [!DNL MongoDB] para um endereço diferente, ajuste o nome do host do banco de dados na próxima etapa de acordo.

## Inserção das informações de conexão e usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]. Você deixou o [!DNL MongoDB] página de credenciais aberta? Caso contrário, acesse **[!UICONTROL Data > Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o [!DNL MongoDB] ícone. Não se esqueça de alterar o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com o `Database Connection` seção:

* `Host`: `127.0.0.1`
* `Username`: A variável [!DNL Commerce Intelligence] [!DNL MongoDB] nome de usuário (deve ser `rjmetric`)
* `Password`: A variável [!DNL Commerce Intelligence] [!DNL MongoDB] senha
* `Port`: porta do MongoDB no servidor (`27017` por padrão)
* `Database Name` (Opcional): Se você só permitiu o acesso a um banco de dados, especifique o nome desse banco de dados aqui.

No `SSH Connection` seção:

* `Remote Address`: O endereço IP ou o nome de host do servidor no qual você executará o SSH
* `Username`: A variável [!DNL Commerce Intelligence] Nome de usuário do Linux (SSH) (deve ser rjmetric)
* `SSH Port`: a porta SSH no servidor (22 por padrão)

Quando terminar, clique em **[!UICONTROL Save Test]** para concluir a configuração.

### Relacionados

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
