---
title: Conectando o MySQL por uma conexão direta
description: Saiba como se conectar [!DNL MongoDB] por conexão direta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Conectar [!DNL MySQL] via conexão direta

## Neste tópico

* [Permitir acesso à [!DNL Commerce Intelligence] Endereço IP](#allowlist)
* [Criar um [!DNL MySQL] usuário para [!DNL Commerce Intelligence]](#steptwo)
* [Insira as informações de conexão em [!DNL Commerce Intelligence]](#stepthree)

## Ir para

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] recomenda usar [SSH](../integrations/mysql-via-ssh-tunnel.md) ou alguma outra forma de criptografia para proteger seus dados! Se isso não for uma opção, você ainda poderá se conectar diretamente [!DNL Commerce Intelligence] ao banco de dados usando as instruções neste tópico.

Este tópico orienta você na conexão direta com o [!DNL MySQL] banco de dados para [!DNL Commerce Intelligence]. Essas configurações também podem ser usadas com [!DNL Adobe Commerce] ou qualquer outro banco de dados de comércio eletrônico que use MySQL.

## Permitir acesso à [!DNL Commerce Intelligence] Endereços IP {#allowlist}

Para que a conexão seja bem-sucedida, você deve configurar o firewall para permitir o acesso de seus endereços IP. Eles são `54.88.76.97` e `34.250.211.151`, mas também está no [!DNL MySQL] página de credenciais:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Criar um [!DNL MySQL] usuário para [!DNL Commerce Intelligence]

A maneira mais simples de criar uma `MySQL` usuário para [!DNL Commerce Intelligence] é para executar a seguinte consulta quando conectado `MySQL` com `GRANT` privilégios. Substituir `Commerce Intelligence IP Address` com o [!DNL Commerce Intelligence] Endereço IP e substituição `secure password` com uma senha segura de sua escolha:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Para impedir que esse usuário acesse dados em bancos de dados, tabelas ou colunas específicos, você pode executar `GRANT` consultas que permitem acesso apenas aos dados permitidos.

**Execute novamente a consulta GRANT para todos os IPs necessários usando o mesmo usuário e senha.**

## Inserir informações de conexão no Commerce Intelligence

Para finalizar, você precisa inserir a conexão e as informações do usuário em [!DNL Commerce Intelligence]. Você deixou o [!DNL MySQL] página de credenciais aberta? Caso contrário, acesse **[!UICONTROL Data** > **Connections]** e clique em **[!UICONTROL Add New Data Source]** e, em seguida, clique na guia [!DNL MySQL] ícone. Não se esqueça de alterar o `Encrypted` alternar para `Yes`.

Insira as seguintes informações nesta página, começando com o `Database Connection` seção:

* `Connection Nickname`: digite um nome para a integração (por exemplo, Loja de comércio eletrônico)
* `Username`: O nome de usuário para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Password`: A senha para o [!DNL Commerce Intelligence] [!DNL MySQL] usuário
* `Port`: porta do MySQL no servidor (`3306` por padrão)
* `Host`: por padrão, é localhost. Em geral, é o valor bind-address do [!DNL MySQL] servidor, que por padrão é `127.0.0.1 (localhost)`, mas também pode ser algum endereço de rede local (por exemplo, `192.168.0.1`) ou o endereço IP público do seu servidor.

   O valor pode ser encontrado no `my.cnf` arquivo (localizado em `/etc/my.cnf`) abaixo da linha que lê `\[mysqld\]`. Se a linha de vinculação de endereço for comentada nesse arquivo, seu servidor estará protegido contra tentativas de conexão externa.

Quando terminar, clique em **[!UICONTROL Save & Test]** para concluir a configuração.

## Documentação relacionada

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
