---
title: Conectando o MySQL por uma conexão direta
description: Saiba como se conectar [!DNL MongoDB] por conexão direta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Conectar [!DNL MongoDB] via conexão direta

## Neste artigo

* [Permitir acesso à [!DNL MBI] Endereço IP](#allowlist)
* [Criar um ](#steptwo)
* [Insira as informações de conexão em [!DNL MBI]](#stepthree)

## Ir para

* [&quot;MySQL via túnel SSH&quot;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&quot;MySQL via cPanel&quot;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>O Adobe recomenda usar [SSH](../integrations/mysql-via-ssh-tunnel.md) ou alguma outra forma de criptografia para proteger seus dados! Se isso não for uma opção, você ainda poderá se conectar diretamente [!DNL MBI] ao banco de dados usando as instruções deste artigo.

Este artigo o orienta pela conexão direta do banco de dados MySQL com o [!DNL MBI]. Essas configurações também podem ser usadas com Commerce ou qualquer outro banco de dados de eCommerce que use MySQL.

## Permitir acesso à [!DNL MBI] Endereços IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está na página de credenciais do MySQL:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criar um usuário MySQL para [!DNL MBI]

A maneira mais simples de criar uma `MySQL` usuário para [!DNL MBI] é para executar a seguinte consulta quando conectado `MySQL` com `GRANT` privilégios. Substituir `MBI IP Address` com o [!DNL MBI] Endereço IP e substituição `secure password` com uma senha segura de sua escolha:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar `GRANT` consultas que permitem acesso apenas aos dados permitidos.

**Execute novamente a consulta GRANT para todos os IPs necessários usando o mesmo usuário e senha.**

## Inserir informações de conexão no MBI

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais do MySQL aberta? Caso contrário, acesse **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o ícone MySQL. Não se esqueça de alterar o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com o `Database Connection` seção:

* `Connection Nickname`: digite um nome para a integração (por exemplo, Loja de comércio eletrônico)
* `Username`: O nome de usuário para o [!DNL MBI] Usuário MySQL
* `Password`: A senha para o [!DNL MBI] Usuário MySQL
* `Port`: porta do MySQL no servidor (`3306` por padrão)
* `Host`: por padrão, é localhost. Em geral, é o valor bind-address do servidor MySQL, que por padrão é `127.0.0.1 (localhost)`, mas também pode ser algum endereço de rede local (por exemplo, `192.168.0.1`) ou o endereço IP público do seu servidor.

   O valor pode ser encontrado no `my.cnf` arquivo (localizado em `/etc/my.cnf`) abaixo da linha que lê `\[mysqld\]`. Se a linha de vinculação de endereço for comentada nesse arquivo, seu servidor estará protegido contra tentativas de conexão externa.

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Documentação relacionada

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
