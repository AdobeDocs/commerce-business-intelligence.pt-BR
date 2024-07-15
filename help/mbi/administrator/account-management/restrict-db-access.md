---
title: Restringindo o Acesso ao Banco de Dados
description: Saiba como restringir o acesso, limitando o acesso ao servidor que hospeda seu banco de dados.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Restringir acesso

Quando você cria um túnel SSH no servidor, o [!DNL Adobe Commerce Intelligence] não precisa ter acesso a nada além do banco de dados. Se você não quiser que o [!DNL Commerce Intelligence] tenha acesso total ao servidor que hospeda o banco de dados, poderá restringir o acesso forçando o usuário [!DNL Commerce Intelligence Linux] a entrar em um [bash shell restrito](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Você pode ter adivinhado pelo nome, mas um shell bash restrito é usado para configurar um ambiente mais controlado do que o shell padrão. O importante sobre este tipo de shell é que os usuários restritos do shell não podem acessar funções do sistema ou fazer qualquer tipo de modificação.

Para restringir o usuário [!DNL Commerce Intelligence Linux], você deve executar duas ações:

1. Altere a variável de ambiente PATH para que seja a string vazia. Isso significa que o usuário não pode acessar executáveis do sistema.

1. Verifique se o shell executado é `bash -r`

Ambos podem ser feitos dentro do arquivo `authorized_keys` no diretório inicial `dir/.ssh` do usuário como parte do comando executado quando o usuário faz logon. É mais ou menos assim:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Quando isso for concluído, o usuário que você criou para [!DNL Commerce Intelligence] não poderá fazer alterações no seu sistema.
