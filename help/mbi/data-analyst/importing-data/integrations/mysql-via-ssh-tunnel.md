---
title: Conectando [!DNL MySQL] via túnel SSH
description: Saiba como se conectar [!DNL MySQL] via túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Conectar [!DNL MySQL] via [!DNL SSH Tunnel]

* [Recuperar o [!DNL Commerce Intelligence] chave pública](#retrieve)
* [Permitir acesso à [!DNL Commerce Intelligence] Endereço IP](#allowlist)
* [Criar um usuário do Linux para [!DNL Commerce Intelligence]](#linux)
* [Criar um [!DNL MySQL] usuário para [!DNL Commerce Intelligence]](#mysql)
* [Insira a conexão e as informações do usuário em [!DNL Commerce Intelligence]](#finish)

## IR PARA

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] Via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Para conectar seu [!DNL MySQL] banco de [!DNL Commerce Intelligence] dados por meio de um `SSH tunnel` , você deve fazer algumas coisas:

1. Recuperar o [!DNL Commerce Intelligence] `public key`
1. Permitir acesso ao [!DNL Commerce Intelligence] `IP address`
1. Criar um `Linux` usuário para [!DNL Commerce Intelligence]
1. Criar um `MySQL` usuário para [!DNL Commerce Intelligence]
1. Insira a conexão e as informações do usuário em [!DNL Commerce Intelligence]


## Recuperação de [!DNL Commerce Intelligence] chave pública {#retrieve}

A variável `public key` é usado para autorizar a [!DNL Commerce Intelligence] `Linux` usuário. Na próxima seção, você criará o usuário e importará a chave.

1. Ir para **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**.
1. Clique em `MySQL` ícone.
1. Depois que a variável `MySQL credentials` for aberta, defina o `Encrypted` alternar para `Yes`. Isso exibe o formulário de configuração SSH.
1. A variável `public key` O está localizado abaixo deste formulário.

Deixe esta página aberta durante todo o tutorial - você precisará dela na próxima seção e no final.

Veja como navegar por [!DNL Commerce Intelligence] para recuperar a chave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permitir acesso à [!DNL Commerce Intelligence] Endereço IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151` mas elas também estão no `MySQL credentials` página. Consulte a caixa azul no GIF acima.

## Criação de um [!DNL Linux] usuário para [!DNL Commerce Intelligence] {#linux}

Pode ser uma máquina de produção ou secundária, desde que contenha dados em tempo real (ou atualizados com frequência). Você pode [restringir este usuário](../../../administrator/account-management/restrict-db-access.md) de qualquer maneira que desejar, desde que mantenha o direito de se conectar à `MySQL` servidor.

1. Para adicionar o novo usuário, execute os seguintes comandos como root em seu [!DNL Linux] servidor:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Lembra-se da `public key` sua recuperação na primeira seção? Para garantir que o usuário tenha acesso ao banco de dados, é necessário importar a chave para `authorized\_keys` o.

   Copie a chave inteira para o arquivo da `authorized\_keys` seguinte maneira:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para concluir a criação do usuário, altere as permissões no `/home/rjmetric` diretório para permitir acesso via `SSH` :

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se o `sshd\_config` arquivo associado ao servidor não estiver definido para a opção padrão, apenas determinados usuários terão acesso ao servidor-isso evita uma conexão [!DNL Commerce Intelligence] com êxito. Nesses casos, é necessário executar um comando como `AllowUsers` para permitir que o `rjmetric` acesso do usuário ao servidor.

## Criação de um [!DNL MySQL] usuário para [!DNL Commerce Intelligence] {#mysql}

Sua organização pode exigir um processo diferente, mas a maneira mais simples de criar esse usuário é executar a seguinte consulta quando conectado [!DNL MySQL] como um usuário com o direito de conceder privilégios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Substituir `secure password here` com uma senha segura, que pode ser diferente da variável `SSH` senha.

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar queries GRANT que só permitem acesso aos dados permitidos.

## Inserção das informações de conexão e usuário em [!DNL Commerce Intelligence] {#finish}

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]. Você deixou o `MySQL credentials` abrir página? Caso contrário, acesse **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o [!DNL MySQL] ícone. Não se esqueça de definir o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com o `Database Connection` seção:

* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Password`: A senha para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Port`: [!DNL MySQL] porta no servidor (3306 por padrão)
* `Host` Por padrão, esse é o localhost. Em geral, é o valor do endereço do BIND para o seu [!DNL MySQL] servidor, que por padrão é `127.0.0.1 (localhost)` , mas também pode ser um endereço de rede local (por exemplo, `192.168.0.1` ) ou o endereço IP público do seu servidor.

   O valor pode ser encontrado no `my.cnf` arquivo (localizado em `/etc/my.cnf` ) abaixo da linha que lê `\[mysqld\]` . Se a linha do endereço do vínculo for comentada nesse arquivo, seu servidor estará protegido contra tentativas de conexão externa.

`SSH Connection`Na seção:

* `Remote Address`: O endereço IP ou o nome de host do servidor [!DNL Commerce Intelligence] encaminhará por túnel para
* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] SSH ([!DNL Linux]) usuário
* `SSH Port`: Porta SSH no servidor (22 por padrão)

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Relacionados:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
