---
title: Restrição do acesso ao banco de dados
description: Saiba como restringir o acesso, limitando o acesso ao servidor que hospeda seu banco de dados.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Restringir acesso

Quando criamos um túnel SSH para seu servidor, não há necessidade de [!DNL MBI] para ter acesso a qualquer item exceto o banco de dados. Se você não quiser [!DNL MBI] para ter acesso total ao servidor que aloja seu banco de dados, você pode restringir o acesso forçando o [!DNL MBI Linux] usuário em um [concha de baixo nível restrito](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Você pode ter adivinhado pelo nome, mas uma casca de baixo restrita é usada para configurar um ambiente mais controlado do que a shell padrão. O importante desse tipo de shell é que os usuários restritos do shell não podem acessar funções do sistema ou fazer qualquer tipo de modificação.

Para restringir o [!DNL MBI Linux] usuário, você deve fazer duas coisas:

1. Altere a variável de ambiente PATH para ser a string vazia. Isso significa que o usuário não poderá acessar os executáveis do sistema.

1. Certifique-se de que o shell executado seja `bash -r`

Ambos podem ser feitos dentro do `authorized_keys` na página inicial do usuário `dir/.ssh` como parte do comando que é executado quando o usuário faz logon. Será algo como isto:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Depois de concluído, o usuário criado para o [!DNL MBI] O não terá a capacidade de fazer alterações no seu sistema.
