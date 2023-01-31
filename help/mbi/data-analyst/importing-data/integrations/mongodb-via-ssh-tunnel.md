---
title: Connect [!DNL MongoDB] via túnel SSH
description: Saiba como se conectar [!DNL MongoDB] via túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Connect [!DNL MongoDB] via túnel SSH


Para conectar seu [!DNL MongoDB] banco de dados para [!DNL MBI] por meio de um túnel SSH, você (ou sua equipe, se você não for um técnico) precisará fazer algumas coisas:

1. [Recupere o [!DNL MBI] chave pública](#retrieve)
1. [Permitir acesso ao [!DNL MBI] Endereço IP](#allowlist)
1. [Criar um usuário Linux para MBI](#linux)
1. [Crie um [!DNL MongoDB] usuário para MBI](#mongodb)
1. [Insira a conexão e as informações do usuário em [!DNL MBI]](#finish)

>[!NOTE]
>
>Devido à natureza técnica dessa configuração, sugerimos que você faça um loop em um desenvolvedor para ajudar caso ainda não tenha feito isso.

## Recuperação de [!DNL MBI] chave pública {#retrieve}

O `public key` é usada para autorizar a variável [!DNL MBI] `Linux` usuário. Na próxima seção, criamos o usuário e importamos a chave.

1. Ir para **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique no botão [!DNL MONGODB] ícone .
1. Depois que a variável [!DNL MongoDB] a página credenciais é aberta, altere a `Encrypted` alternar para `Yes`. Isso exibirá o formulário de configuração SSH.
1. O `public key` está localizado abaixo deste formulário.

Deixe essa página aberta em todo o tutorial; será necessário tê-la na próxima seção e no final.

Se você estiver um pouco perdido, veja como navegar [!DNL MBI] para recuperar a chave:

![Recuperação da chave pública RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permitir acesso ao [!DNL MBI] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, é necessário configurar o firewall para permitir o acesso dos endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está no [!DNL MongoDB] página de credenciais:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criação de um `Linux` usuário para [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Se a variável `sshd_config` o arquivo associado ao servidor não está definido como a opção padrão, somente determinados usuários terão acesso ao servidor - isso impedirá uma conexão bem-sucedida com o [!DNL MBI]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir `rjmetric` acesso do usuário ao servidor.

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode restringir este usuário da maneira que desejar, desde que ele mantenha o direito de se conectar ao [!DNL MongoDB] servidor.

Para adicionar o novo usuário, execute os seguintes comandos como root em seu `Linux` servidor:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Lembre-se do `public key` recuperamos na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, precisamos importar a chave para `authorized_keys`. Copie a chave inteira no `authorized_keys` como segue:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para concluir a criação do usuário, altere as permissões no diretório /home/rjmetric para permitir acesso via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Criação de um [!DNL MBI] [!DNL MongoDB] usuário {#mongodb}

[!DNL MongoDB] os servidores têm dois modos de execução - [um com a opção &quot;auth&quot;](#auth) `(mongod -- auth)` e uma sem, [que é o padrão](#default). As etapas para criar uma [!DNL MongoDB] o usuário varia um pouco dependendo do modo usado pelo servidor, portanto, verifique o modo antes de continuar.

### Se o servidor usar a variável `Auth` Opção: {#auth}

Ao se conectar a vários bancos de dados, é possível adicionar o usuário fazendo logon em [!DNL MongoDB] como um usuário administrador e executando os seguintes comandos.

>[!NOTE]
>
>Para ver todos os bancos de dados disponíveis, a variável [!DNL MBI] O usuário requer permissões para execução `listDatabases.`

Este comando concederá a [!DNL MBI] acesso do usuário `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use este comando para conceder o [!DNL MBI] acesso do usuário `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Isso imprimirá uma resposta com esta aparência:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Se o servidor usar a opção padrão {#default}

Se o servidor não usar `auth` , seu [!DNL MongoDB] O servidor ainda estará acessível mesmo sem um nome de usuário e senha. No entanto, você deve garantir que a variável `mongodb.conf` arquivo `(/etc/mongodb.conf)` tem as seguintes linhas: caso contrário, reinicie o servidor depois de adicioná-las.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para vincular seu [!DNL MongoDB] para um endereço diferente, ajuste o nome do host do banco de dados na próxima etapa de acordo.

## Inserir a conexão e as informações do usuário em [!DNL MBI] {#finish}

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou o [!DNL MongoDB] página de credenciais aberta? Caso contrário, acesse **[!UICONTROL Data > Connections]** e clique em **[!UICONTROL Add New Data Source]**, em seguida, o [!DNL MongoDB] ícone . não se esqueça de mudar a `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com `Database Connection` seção:

* `Host`: `127.0.0.1`
* `Username`: O [!DNL MBI] [!DNL MongoDB] nome de usuário (deve ser `rjmetric`)
* `Password`: O [!DNL MBI] [!DNL MongoDB] senha
* `Port`: Porta do MongoDB no seu servidor (`27017` por padrão)
* `Database Name` (Opcional): Se você tiver permitido acesso a apenas um banco de dados, especifique o nome desse banco de dados aqui.

Em `SSH Connection` seção:

* `Remote Address`: O endereço IP ou o nome do host do servidor no qual vamos SSH
* `Username`: O [!DNL MBI] Nome de usuário do Linux (SSH) (deve ser rjmetric)
* `SSH Port`: A porta SSH em seu servidor (22 por padrão)

Pronto! Quando terminar, clique em **[!UICONTROL Save Test]** para concluir a configuração.

### Relacionado

* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
