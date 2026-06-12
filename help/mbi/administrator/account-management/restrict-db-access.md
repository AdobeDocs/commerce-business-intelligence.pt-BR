---
title: Restringindo o Acesso ao Banco de Dados
description: Saiba como restringir o acesso, limitando o acesso ao servidor que hospeda seu banco de dados.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
TQID: https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 225
ht-degree: 0%

---

# Restringir acesso

Quando você cria um túnel SSH no servidor, o [!DNL Adobe Commerce Intelligence] não precisa ter acesso a nada além do banco de dados. Para registro, erros e solução de problemas da chave do host SSH, consulte [Verificação da chave do host SSH](../../data-analyst/importing-data/integrations/ssh-host-key-verification.md). Se você não quiser que o [!DNL Commerce Intelligence] tenha acesso total ao servidor que hospeda o banco de dados, poderá restringir o acesso forçando o usuário [!DNL Commerce Intelligence Linux] a entrar em um [bash shell restrito](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

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
