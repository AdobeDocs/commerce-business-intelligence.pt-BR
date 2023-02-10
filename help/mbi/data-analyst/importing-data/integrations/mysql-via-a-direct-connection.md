---
title: Conexão do MySQL via conexão direta
description: Saiba como se conectar [!DNL MongoDB] por conexão direta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Connect [!DNL MongoDB] por ligação direta

## No presente artigo

* [Permitir acesso ao [!DNL MBI] Endereço IP](#allowlist)
* [Crie um ](#steptwo)
* [Insira informações de conexão em [!DNL MBI]](#stepthree)

## Ir para

* [&quot;MySQL via túnel SSH`](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&quot;MySQL via cPanel&quot;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Recomendamos que você use [SSH](../integrations/mysql-via-ssh-tunnel.md) ou qualquer outra forma de criptografia para proteger seus dados! Se essa não for uma opção, você ainda poderá se conectar diretamente [!DNL MBI] ao seu banco de dados usando as instruções deste artigo.

Neste artigo, o orientamos a conectar diretamente o banco de dados do MySQL ao [!DNL MBI]. Essas configurações também podem ser usadas com o Commerce ou qualquer outro banco de dados de eCommerce que use o MySQL.

## Permitir acesso ao [!DNL MBI] Endereços IP {#allowlist}

Para que a conexão seja bem-sucedida, é necessário configurar o firewall para permitir o acesso dos endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está na página de credenciais do MySQL :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criar um usuário do MySQL para [!DNL MBI]

A maneira mais simples de criar uma `MySQL` usuário para [!DNL MBI] é executar a seguinte query quando conectado `MySQL` com `GRANT` privilégios. Substituir `MBI IP Address` com o [!DNL MBI] Endereço IP e substituir `secure password` com uma senha segura de sua escolha:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar `GRANT` consultas que permitem acesso somente aos dados permitidos.

**Execute novamente a consulta GRANT para todos os IPs necessários usando o mesmo usuário e senha.**

## Inserir informações de conexão no MBI

Para fechar os itens, precisamos inserir a conexão e as informações do usuário em [!DNL MBI]. Você deixou a página de credenciais do MySQL aberta? Caso contrário, acesse **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]**, depois o ícone MySQL . Não se esqueça de alterar a `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com `Database Connection` seção:

* `Connection Nickname`: Insira um nome para a integração (por exemplo, Loja Ecommerce)
* `Username`: O nome de usuário para a [!DNL MBI] Usuário do MySQL
* `Password`: A senha do [!DNL MBI] Usuário do MySQL
* `Port`: Porta do MySQL no seu servidor (`3306` por padrão)
* `Host`: Por padrão, será localhost. Em geral, será o valor bind-address do seu servidor MySQL, que por padrão é `127.0.0.1 (localhost)`, mas também pode ser algum endereço de rede local (por exemplo, `192.168.0.1`) ou o endereço IP público do seu servidor.

   O valor pode ser encontrado no `my.cnf` (normalmente localizado em `/etc/my.cnf`) abaixo da linha que lê `\[mysqld\]`. Se a linha bind-address estiver comentada nesse arquivo, o servidor será protegido de tentativas de conexão externas.

Pronto! Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Documentação relacionada

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
