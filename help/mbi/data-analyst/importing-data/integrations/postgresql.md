---
title: Conectar o PostgreSQL via Túnel SSH
description: Saiba como conectar seu banco de dados PostgreSQL ao [!DNL MBI] via túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Conectar `PostgreSQL` via `SSH` Túnel

Para conectar seu `PostgreSQL` banco de dados para [!DNL MBI] por meio de um `SSH tunnel`, você (ou sua equipe, se não for um técnico) deve fazer algumas coisas:

1. [Recuperar o [!DNL MBI] chave pública](#retrieve)
1. [Permitir acesso à [!DNL MBI] Endereço IP](#allowlist)
1. [Criar um Linux](#linux)
1. [Criar um usuário Postgres para [!DNL MBI] ](#postgres)
1. [Insira as informações de conexão e usuário no MBI](#finish)

Não é tão complicado quanto poderia parecer. Comece já.

## Recuperação de [!DNL MBI] `public key` {#retrieve}

A variável `public key` é usado para autorizar a [!DNL MBI] Usuário do Linux®. Na próxima seção, você criará o usuário e importará a chave.

1. Ir para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add a Data Source]**.
1. Clique em `PostgreSQL` ícone.
1. Depois que a variável `PostgreSQL credentials` for aberta, defina o `Encrypted` alternar para `Yes`. Isso exibe o `SSH` formulário de configuração.
1. A variável `public key` O está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Se você está um pouco perdido, esta é a forma de navegar [!DNL MBI] para recuperar a chave:

![Recuperando a chave pública de RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permitir acesso à [!DNL MBI] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso pelo seu endereço IP. É necessário `54.88.76.97/32`, mas também está no `PostgreSQL` página de credenciais. Vê a caixa azul no GIF acima? Pronto!

## Criação de um `Linux` usuário para [!DNL MBI] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) de qualquer maneira que desejar, desde que ele mantenha o direito de se conectar ao servidor PostgreSQL.

1. Para adicionar o novo usuário, execute os seguintes comandos como root em seu `Linux` servidor:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Lembre-se do `public key` você recuperou na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, é necessário importar a chave para o `authorized\_keys`.

   Copie toda a chave na `authorized\_keys` do seguinte modo:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para concluir a criação do usuário, altere as permissões no `/home/rjmetric` diretório para permitir acesso via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Se a variável `sshd\_config` o arquivo associado ao servidor não está definido como a opção padrão, somente determinados usuários têm acesso ao servidor - isso impede uma conexão bem-sucedida com o [!DNL MBI]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o usuário rjmetric acesse o servidor.

## Criação de um [!DNL MBI] Usuário Postgres {#postgres}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte consulta quando conectado ao Postgres como usuário com o direito de conceder privilégios. O usuário também deve ser o proprietário do esquema que [!DNL MBI] está recebendo acesso ao.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Substituir `secure password` com sua própria senha segura, que pode ser diferente da senha SSH. Além disso, substitua `database name` e `schema name` com os nomes apropriados em seu banco de dados.

Se quiser conectar vários bancos de dados ou esquemas, repita esse processo conforme necessário.

## Inserção das informações de conexão e usuário em [!DNL MBI] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais do PostgreSQL aberta? Caso contrário, acesse **[!UICONTROL Manage Data > Connections]** e clique em **[!UICONTROL Add a Data Source]**, depois o ícone PostgreSQL. Não se esqueça de definir o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com a seção Conexão de Banco de Dados:

* `Username`: O nome de usuário Postgres de RJMetrics (deve ser rjmetric)
* `Password`: a senha Postgres do RJMetrics
* `Port`: Porta PostgreSQL no servidor (5432 por padrão)
* `Host`: 127.0.0.1

Em `SSH Connection`:

* `Remote Address`: O endereço IP ou o nome de host do servidor no qual você executará o SSH
* `Username`: seu nome de logon SSH (deve ser rjmetric)
* `SSH Port`: Porta SSH no servidor (22 por padrão)

Pronto! Quando terminar, clique em **Salvar e testar** para concluir a configuração.

### Relacionados

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
