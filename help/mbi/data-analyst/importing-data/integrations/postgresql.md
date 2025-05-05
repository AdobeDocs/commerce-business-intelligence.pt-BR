---
title: Conectar o PostgreSQL via Túnel SSH
description: Saiba como conectar seu banco de dados PostgreSQL ao Commerce Intelligence por um túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Conectar [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Para conectar o banco de dados do [!DNL PostgreSQL] ao [!DNL Commerce Intelligence] por meio de um `SSH tunnel`, faça o seguinte:

1. [Recuperar a  [!DNL Commerce Intelligence] chave pública](#retrieve)
1. [Permitir acesso ao endereço IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Criar um  [!DNL Linux] usuário para [!DNL Commerce Intelligence]](#linux)
1. [Criar um  [!DNL PostgreSQL] usuário para [!DNL Commerce Intelligence]](#postgres)
1. [Insira as informações de conexão e usuário em  [!DNL Commerce Intelligence]](#finish)

## Recuperando o [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

O `public key` é usado para autorizar o usuário [!DNL Commerce Intelligence] [!DNL Linux]. Agora, você criará o usuário e importará a chave.

1. Vá para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add a Data Source]**.
1. Clique no ícone [!DNL PostgreSQL].
1. Depois que a página `PostgreSQL credentials` for aberta, defina o botão `Encrypted` como `Yes`. Isso exibe o formulário de configuração `SSH`.
1. O `public key` está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Abaixo demonstra como navegar pelo [!DNL Commerce Intelligence] para recuperar a chave:

![Recuperando a chave pública de RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permitir acesso ao endereço IP [!DNL Commerce Intelligence] {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso pelo seu endereço IP. Ele é `54.88.76.97/32`, mas também está na página de credenciais `PostgreSQL`. Consulte a caixa azul no GIF acima.

## Criando um usuário [!DNL Linux] para [!DNL Commerce Intelligence] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) da maneira que desejar, contanto que ele mantenha o direito de se conectar ao servidor [!DNL PostgreSQL].

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
```

>[!IMPORTANT]
>
>Se o arquivo `sshd\_config` associado ao servidor não estiver definido como a opção padrão, somente determinados usuários terão acesso ao servidor; isso impede uma conexão bem-sucedida com o [!DNL Commerce Intelligence]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o usuário rjmetric acesse o servidor.

## Criando um usuário [!DNL Commerce Intelligence] [!DNL Postgres] {#postgres}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte consulta quando conectado ao Postgres como usuário com o direito de conceder privilégios. O usuário também deve ser o proprietário do esquema ao qual [!DNL Commerce Intelligence] está sendo concedido acesso.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Substitua `secure password` com sua própria senha de segurança, que pode ser diferente da senha SSH. Além disso, substitua `database name` e `schema name` pelos nomes apropriados em seu banco de dados.

Se quiser conectar vários bancos de dados ou esquemas, repita esse processo conforme necessário.

## Inserindo a conexão e as informações do usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir as informações de conexão e usuário em [!DNL Commerce Intelligence]. Você deixou a página de credenciais [!DNL PostgreSQL] aberta? Caso contrário, vá para **[!UICONTROL Manage Data > Connections]**, clique em **[!UICONTROL Add a Data Source]** e depois no ícone [!DNL PostgreSQL]. Não se esqueça de definir a alternância de `Encrypted` para `Yes`.

Insira as seguintes informações nesta página, começando com a seção `Database Connection`:

* `Username`: O nome de usuário RJMetrics Postgres (deve ser rjmetric)
* `Password`: A senha Postgres de RJMetrics
* `Port`: Porta PostgreSQL no servidor (5432 por padrão)
* `Host`: 127.0.0.1

Em `SSH Connection`:

* `Remote Address`: O endereço IP ou o nome de host do servidor no qual você fará SSH
* `Username`: Seu nome de logon SSH (deve ser rjmetric)
* `SSH Port`: Porta SSH no servidor (22 por padrão)

Quando terminar, clique em **Salvar e testar** para concluir a configuração.

### Relacionados

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
