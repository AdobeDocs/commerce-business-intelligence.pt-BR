---
title: Conectando o MySQL via túnel SSH
description: Saiba como conectar o MySQL via túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Connect `MySQL` via `SSH Tunnel`

* [Recupere o [!DNL MBI] chave pública](#retrieve)
* [Permitir acesso ao [!DNL MBI] Endereço IP](#allowlist)
* [Crie um usuário Linux para [!DNL MBI]](#linux)
* [Criar um usuário do MySQL para [!DNL MBI]](#mysql)
* [Insira a conexão e as informações do usuário em [!DNL MBI]](#finish)

## SALTAR PARA

* `MySQL via SSH tunnel`
* [`MySQL`](../integrations/mysql-via-a-direct-connection.md)
* [`MySQL`](../integrations/mysql-via-cpanel.md)

Para conectar seu `MySQL` banco de dados para [!DNL MBI] via `SSH tunnel`, você (ou sua equipe, se você não for um técnico) precisará fazer algumas coisas:

1. Recupere o [!DNL MBI] `public key`
1. Permitir acesso ao [!DNL MBI] `IP address`
1. Crie um `Linux` usuário para [!DNL MBI]
1. Crie um `MySQL` usuário para [!DNL MBI]
1. Insira a conexão e as informações do usuário em [!DNL MBI]

Não é tão complicado como pode parecer. Vamos começar.

## Recuperação de [!DNL MBI] chave pública {#retrieve}

O `public key` é usada para autorizar a variável [!DNL MBI] `Linux` usuário. Na próxima seção, criaremos o usuário e importaremos a chave.

1. Ir para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique no botão `MySQL` ícone .
1. Depois que a variável `MySQL credentials` será aberta, defina a variável `Encrypted` alternar para `Yes`. Isso exibirá o formulário de configuração SSH.
1. O `public key` está localizado abaixo deste formulário.

Deixe essa página aberta em todo o tutorial; será necessário tê-la na próxima seção e no final.

Se você estiver um pouco perdido, veja como navegar [!DNL MBI] para recuperar a chave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permitir acesso ao [!DNL MBI] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, é necessário configurar o firewall para permitir o acesso dos endereços IP. Eles são `54.88.76.97` e `34.250.211.151` mas também estão no `MySQL credentials` página. Veja a caixa azul no GIF acima? Pronto!

## Criação de um `Linux` usuário para [!DNL MBI] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) da maneira que desejar, desde que mantenha o direito de se conectar ao `MySQL` servidor.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se a variável `sshd\_config` o arquivo associado ao servidor não está definido como a opção padrão, somente determinados usuários terão acesso ao servidor - isso impedirá uma conexão bem-sucedida com o [!DNL MBI]. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir `rjmetric` acesso do usuário ao servidor.

## Criação de um `MySQL` usuário para [!DNL MBI] {#mysql}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte query ao fazer logon `MySQL` como usuário com direito a conceder privilégios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Substituir `secure password here` com uma senha segura, que pode ser diferente do `SSH` senha.

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar consultas GRANT que permitem somente acesso aos dados permitidos.

## Inserir a conexão e as informações do usuário em [!DNL MBI] {#finish}

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou o `MySQL credentials` página aberta? Caso contrário, acesse **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o ícone MySQL . não se esqueça de definir a variável `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando pela seção Conexão do Banco de Dados:

* `Username`: O nome de usuário para a [!DNL MBI] Usuário do MySQL
* `Password`: A senha do [!DNL MBI] Usuário do MySQL
* `Port`: Porta do MySQL no seu servidor (3306 por padrão)
* `Host` Por padrão, será localhost. Em geral, será o valor bind-address do seu servidor MySQL, que por padrão é `127.0.0.1 (localhost)`, mas também pode ser algum endereço de rede local (por exemplo, `192.168.0.1`) ou o endereço IP público do seu servidor.

   O valor pode ser encontrado no `my.cnf` (normalmente localizado em `/etc/my.cnf`) abaixo da linha que lê `\[mysqld\]`. Se a linha bind-address estiver comentada nesse arquivo, o servidor será protegido de tentativas de conexão externas.

No `SSH Connection` seção:

* `Remote Address`: O endereço IP ou o nome do host do servidor [!DNL MBI] encapsulará
* `Username`: O nome de usuário para a [!DNL MBI] Usuário do SSH (Linux)
* `SSH Port`: Porta SSH em seu servidor (22 por padrão)

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Relacionadas:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
