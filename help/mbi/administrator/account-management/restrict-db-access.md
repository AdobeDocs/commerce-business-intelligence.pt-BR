---
title: Restringindo o Acesso ao Banco de Dados
description: Saiba como restringir o acesso, limitando o acesso ao servidor que hospeda seu banco de dados.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Restringir acesso

Quando você cria um túnel SSH no servidor, não há necessidade de [!DNL Adobe Commerce Intelligence] para ter acesso a qualquer coisa além do banco de dados. Se não quiser [!DNL Commerce Intelligence] para ter acesso total ao servidor que hospeda seu banco de dados, é possível restringir o acesso forçando o [!DNL Commerce Intelligence Linux] usuário em um [shell bash restrito](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Você pode ter adivinhado pelo nome, mas um shell bash restrito é usado para configurar um ambiente mais controlado do que o shell padrão. O importante sobre este tipo de shell é que os usuários restritos do shell não podem acessar funções do sistema ou fazer qualquer tipo de modificação.

Para restringir o [!DNL Commerce Intelligence Linux] usuário, você deve executar duas ações:

1. Altere a variável de ambiente PATH para que seja a string vazia. Isso significa que o usuário não pode acessar executáveis do sistema.

1. Certifique-se de que o shell executado seja `bash -r`

Ambos podem ser feitos dentro do `authorized_keys` arquivo na página inicial do usuário `dir/.ssh` como parte do comando executado quando o usuário faz logon. É mais ou menos assim:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Quando estiver concluído, o usuário criado para [!DNL Commerce Intelligence] O não pode fazer alterações no sistema.
