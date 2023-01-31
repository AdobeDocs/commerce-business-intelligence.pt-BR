---
title: Conecte o PostgreSQL via túnel SSH
description: Saiba como conectar o banco de dados PostgreSQL ao [!DNL MBI] através de um túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Connect `PostgreSQL` via `SSH` Túnel

Para conectar seu `PostgreSQL` banco de dados para [!DNL MBI] via `SSH tunnel`, você (ou sua equipe, se você não for um técnico) precisará fazer algumas coisas:

1. [Recupere o [!DNL MBI] chave pública](#retrieve)
1. [Permitir acesso ao [!DNL MBI] Endereço IP](#allowlist)
1. [Crie um usuário Linux para [!DNL MBI] ](#linux)
1. [Crie um usuário do Postgres para [!DNL MBI] ](#postgres)
1. [Inserir a conexão e as informações do usuário no MBI](#finish)

Não é tão complicado como pode parecer. Comece já.

## Recuperação de [!DNL MBI] `public key` {#retrieve}

O `public key` é usada para autorizar a variável [!DNL MBI] Usuário do Linux. Na próxima seção, criaremos o usuário e importaremos a chave.

1. Ir para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add a Data Source]**.
1. Clique no botão `PostgreSQL` ícone .
1. Depois que a variável `PostgreSQL credentials` será aberta, defina a variável `Encrypted` alternar para `Yes`. Isso exibirá a variável `SSH` formulário de configuração.
1. O `public key` está localizado abaixo deste formulário.

Deixe essa página aberta em todo o tutorial; será necessário tê-la na próxima seção e no final.

Se você estiver um pouco perdido, é assim que você navega [!DNL MBI] para recuperar a chave:

![Recuperação da chave pública RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permitir acesso ao [!DNL MBI] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, é necessário configurar o firewall para permitir o acesso do endereço IP. é `54.88.76.97/32`, mas também está no `PostgreSQL` credenciais. Veja a caixa azul no GIF acima? Pronto!

## Criação de um `Linux` usuário para [!DNL MBI] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) da maneira que desejar, desde que mantenha o direito de se conectar ao servidor PostgreSQL.

1. Para adicionar o novo usuário, execute os seguintes comandos como root em seu `Linux` servidor:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Lembre-se do `public key` recuperamos na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, precisamos importar a chave para `authorized\_keys`.

   Copie a chave inteira no `authorized\_keys` como segue:

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
>Se a variável `sshd\_config` o arquivo associado ao servidor não está definido como a opção padrão, somente determinados usuários terão acesso ao servidor - isso impedirá uma conexão bem-sucedida com o [!DNL MBI]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir o acesso do usuário rjmetric ao servidor.

## Criação de um [!DNL MBI] Usuário do Postgres {#postgres}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte query quando conectado aos Postgres como um usuário com o direito de conceder privilégios. O usuário também deve ser o proprietário do schema que [!DNL MBI] está sendo concedido acesso ao .

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Substituir `secure password` com sua própria senha segura, que pode ser diferente da senha SSH. Além disso, certifique-se de substituir `database name` e `schema name` com os nomes apropriados no banco de dados.

Se quiser conectar vários bancos de dados ou esquemas, repita esse processo conforme necessário.

## Inserir a conexão e as informações do usuário em [!DNL MBI] {#finish}

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais PostgreSQL aberta? Caso contrário, acesse **[!UICONTROL Manage Data > Connections]** e clique em **[!UICONTROL Add a Data Source]**, em seguida, o ícone PostgreSQL. Não se esqueça de definir a variável `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando pela seção Conexão do Banco de Dados:

* `Username`: O nome de usuário de RJMetrics Postgres (deve ser rjmetric)
* `Password`: A senha dos Postgres RJMetrics
* `Port`: Porta PostgreSQL em seu servidor (5432 por padrão)
* `Host`: 127.0.0.1

Em `SSH Connection`:

* `Remote Address`: O endereço IP ou o nome do host do servidor no qual vamos SSH
* `Username`: Nosso nome de logon SSH (deve ser rjmetric)
* `SSH Port`: Porta SSH em seu servidor (22 por padrão)

Pronto! Quando terminar, clique em **Salvar e testar** para concluir a configuração.

### Relacionado

* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
