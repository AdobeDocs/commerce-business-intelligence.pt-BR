---
title: Conectando [!DNL MySQL] via túnel SSH
description: Saiba como se conectar [!DNL MySQL] via túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Conectar [!DNL MySQL] via [!DNL SSH Tunnel]

* [Recuperar a  [!DNL Commerce Intelligence] chave pública](#retrieve)
* [Permitir acesso ao endereço IP  [!DNL Commerce Intelligence] ](#allowlist)
* [Criar um usuário do Linux para  [!DNL Commerce Intelligence]](#linux)
* [Criar um  [!DNL MySQL] usuário para [!DNL Commerce Intelligence]](#mysql)
* [Insira as informações de conexão e usuário em  [!DNL Commerce Intelligence]](#finish)

## IR PARA

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Para conectar o banco de dados do [!DNL MySQL] ao [!DNL Commerce Intelligence] por meio de um `SSH tunnel`, faça o seguinte:

1. Recuperar o [!DNL Commerce Intelligence] `public key`
1. Permitir acesso ao [!DNL Commerce Intelligence] `IP address`
1. Criar um usuário `Linux` para [!DNL Commerce Intelligence]
1. Criar um usuário `MySQL` para [!DNL Commerce Intelligence]
1. Inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]


## Recuperando a chave pública [!DNL Commerce Intelligence] {#retrieve}

O `public key` é usado para autorizar o usuário [!DNL Commerce Intelligence] `Linux`. Na próxima seção, você criará o usuário e importará a chave.

1. Vá para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique no ícone `MySQL`.
1. Depois que a página `MySQL credentials` for aberta, defina o botão `Encrypted` como `Yes`. Isso exibe o formulário de configuração SSH.
1. O `public key` está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Veja como navegar pelo [!DNL Commerce Intelligence] para recuperar a chave:

![Demonstração animada da conexão MySQL via túnel SSH](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permitir acesso ao endereço IP [!DNL Commerce Intelligence] {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles estão `54.88.76.97` e `34.250.211.151`, mas também estão na página `MySQL credentials`. Consulte a caixa azul no GIF acima.

## Criando um usuário [!DNL Linux] para [!DNL Commerce Intelligence] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) da maneira que desejar, contanto que ele mantenha o direito de se conectar ao servidor `MySQL`.

1. Para adicionar o novo usuário, execute os seguintes comandos como raiz no servidor [!DNL Linux]:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Lembra do `public key` que você recuperou na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, você precisa importar a chave para `authorized\_keys`.

   Copie toda a chave no arquivo `authorized\_keys` da seguinte maneira:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para concluir a criação do usuário, altere as permissões no diretório `/home/rjmetric` para permitir acesso via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se o arquivo `sshd\_config` associado ao servidor não estiver definido como a opção padrão, somente determinados usuários terão acesso ao servidor; isso impede uma conexão bem-sucedida com o [!DNL Commerce Intelligence]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o usuário `rjmetric` acesse o servidor.

## Criando um usuário [!DNL MySQL] para [!DNL Commerce Intelligence] {#mysql}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte consulta quando conectado a [!DNL MySQL] como um usuário com o direito de conceder privilégios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Substitua `secure password here` por uma senha segura, que pode ser diferente da senha `SSH`.

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar queries GRANT que só permitem acesso aos dados permitidos.

## Inserindo a conexão e as informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir as informações de conexão e usuário em [!DNL Commerce Intelligence]. Você deixou a página `MySQL credentials` aberta? Caso contrário, vá para **[!UICONTROL Data** > **Connections]**, clique em **[!UICONTROL Add New Data Source]** e depois no ícone [!DNL MySQL]. Não se esqueça de definir a alternância de `Encrypted` para `Yes`.

Insira as seguintes informações nesta página, começando com a seção `Database Connection`:

* `Username`: O nome de usuário de [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: A senha para o usuário [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: porta [!DNL MySQL] no servidor (3306 por padrão)
* `Host` Por padrão, este é localhost. Em geral, esse é o valor do endereço de ligação do servidor [!DNL MySQL], que por padrão é `127.0.0.1 (localhost)`, mas que também pode ser algum endereço de rede local (por exemplo, `192.168.0.1`) ou o endereço IP público do servidor.

  O valor pode ser encontrado no arquivo `my.cnf` (localizado em `/etc/my.cnf`) abaixo da linha que lê `\[mysqld\]`. Se a linha de vinculação de endereço for comentada nesse arquivo, seu servidor estará protegido contra tentativas de conexão externa.

Na seção `SSH Connection`:

* `Remote Address`: O endereço IP ou o nome de host do servidor [!DNL Commerce Intelligence] será encapsulado em
* `Username`: O nome de usuário do [!DNL Commerce Intelligence] usuário SSH ([!DNL Linux])
* `SSH Port`: Porta SSH no servidor (22 por padrão)

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a instalação.

## Relacionados:

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
