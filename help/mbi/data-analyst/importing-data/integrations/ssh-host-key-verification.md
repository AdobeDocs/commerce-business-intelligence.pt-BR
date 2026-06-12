---
title: Verificação da chave do host SSH
description: Saiba como o Commerce Intelligence registra chaves de host SSH, como atualizá-las, solucionar erros e quando entrar em contato com o Suporte para conexões de túnel SSH.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# Verificação da chave do host SSH {#ssh-host-keys}

[!DNL Commerce Intelligence] usa verificação de chave de host SSH estrita para conexões de banco de dados criptografadas (túnel SSH), incluindo [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md) e [PostgreSQL](postgresql.md).

Durante o **[!UICONTROL Save & Test]**, o sistema registra as chaves do host da bastição SSH para sua conexão e as armazena com segurança por conexão. Após a inscrição, a replicação e o tunelamento só têm êxito quando as chaves do host do bastião ativo correspondem às chaves inscritas.

Esse modelo melhora a segurança, bloqueando ataques intermediários e alterações inesperadas no host. Também significa que a rotação de chaves do host, a falta de material de confiança ou as alterações na infraestrutura podem aparecer como erros de chave do host SSH na conexão, em vez de falhas genéricas de túnel.

>[!NOTE]
>
>**Administrador** significa um usuário com permissões de Administrador na sua conta [!DNL Commerce Intelligence], não seu console da organização da Adobe, a menos que indicado de outra forma. Somente Administradores podem executar **[!UICONTROL Refresh SSH Host Keys]**. Se você não vir esse controle, peça a um Administrador em sua conta para executar a atualização ou entre em contato com o Suporte da Adobe.

Você não edita, carrega nem gerencia `known_hosts` arquivos. A inscrição e a atualização são executadas na infraestrutura do Adobe atribuída à sua conta.

>[!IMPORTANT]
>
>A rotação de chaves do host requer um Administrador para executar **[!UICONTROL Refresh SSH Host Keys]**. Se as chaves do host do bastião foram alteradas ou a identidade do bastião foi alterada (nome do host, IP ou porta), executar **[!UICONTROL Save & Test]** novamente ou salvar novamente a conexão não atualizará as chaves registradas. A conexão pode continuar falhando até que um Administrador atualize as chaves do host.

## Salvar e testar {#save-and-test}

**[!UICONTROL Save & Test]** executa **somente inscrição inicial de chave de host SSH**. Ele é conservador por design e não gira nem substitui chaves que já estão inscritas na conexão.

| Estado da chave de host inscrita | O que salvar e testar faz |
| --- | --- |
| As chaves do host ainda não estão inscritas | O **[!UICONTROL Save & Test]** verifica o host e a porta do bastião, registra as chaves do host e armazena-as para esta conexão. |
| As chaves do host já estão inscritas | **[!UICONTROL Save & Test]** ignora a inscrição. Ela não substitui, gira ou exclui chaves inscritas existentes, mesmo que as chaves de bastião ativas não correspondam mais. |
| As chaves inscritas estão ausentes, vazias ou são inválidas | **[!UICONTROL Save & Test]** não repara o material de confiança inválido sozinho. Um Administrador deve executar **[!UICONTROL Refresh SSH Host Keys]** ou contatar o Suporte se os erros continuarem |

Após uma primeira inscrição bem-sucedida, mais tarde **[!UICONTROL Save & Test]** executará as credenciais de validação e as configurações de conexão, mas deixará as chaves de host SSH registradas inalteradas.

## Atualizar chaves do host SSH {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** atualiza as chaves do host SSH registradas quando o bastião foi alterado ou quando o material de confiança deve ser reparado. Um Administrador inicia a atualização da conexão em **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

A atualização é executada de forma assíncrona na infraestrutura do Adobe atribuída à sua conta. [!DNL Commerce Intelligence] retorna depois que a atualização é enfileirada. Ele não executa a varredura na estação de trabalho.

Uma atualização **reescreve** chaves de host inscritas somente quando uma destas condições for verdadeira:

* Chaves do host registradas estão ausentes
* As chaves de host registradas estão vazias
* Não é possível ler as chaves de host registradas
* Falha na validação de chaves de host registradas
* Uma nova verificação retorna linhas de chave de host diferentes das chaves inscritas
* As impressões digitais da digitalização e das chaves registradas não correspondem

Se as chaves inscritas forem atuais e válidas, a atualização será concluída sem alterá-las.

>[!TIP]
>
>Execute **[!UICONTROL Refresh SSH Host Keys]** depois que sua equipe girar as chaves do host SSH na base, alterar o nome do host ou IP da base ou substituir o ponto de extremidade SSH. Aguarde alguns minutos e execute **[!UICONTROL Save & Test]** para confirmar a conexão.

## Migração de conta {#migration}

Você não aciona a migração de contas. O Adobe executa movimentações do servidor de dados durante a manutenção ou o dimensionamento e copia chaves de host SSH registradas para que a verificação estrita continue a funcionar após a movimentação.

Depois que a Adobe notificar que a migração foi concluída:

1. Execute **[!UICONTROL Save & Test]** para confirmar a conexão. O registro deve ser ignorado se as chaves foram copiadas com êxito.
1. Se os erros de chave do host SSH persistirem, peça a um Administrador para executar **[!UICONTROL Refresh SSH Host Keys]**, aguarde alguns minutos e execute **[!UICONTROL Save & Test]** novamente.
1. Entre em contato com o Suporte da Adobe se os erros continuarem após **[!UICONTROL Save & Test]** e até duas tentativas de **[!UICONTROL Refresh SSH Host Keys]**.

## Mensagens de erro da chave do host SSH {#ssh-host-key-errors}

O status da conexão mostra uma única mensagem de chave de host SSH amigável. Erros brutos de OpenSSH não são mostrados no painel.

A tabela a seguir mapeia mensagens comuns para as causas prováveis e as próximas etapas típicas.

| Mensagem ou status | O que significa | Possíveis causas | Próxima etapa típica |
| --- | --- | --- | --- |
| Falha na verificação da chave do host SSH | A chave do host do bastião não corresponde às chaves inscritas ou o material confiável não pode ser usado | Chaves do host SSH rotacionadas no bastião; nome do host bastião, IP, ou porta alterada; chaves registradas ausentes, vazias, inválidas ou ilegíveis | Confirme **Endereço Remoto** e **Porta SSH**. Pergunte à sua equipe de infraestrutura se as chaves do bastião do host foram alteradas. Peça a um Administrador para executar **[!UICONTROL Refresh SSH Host Keys]**, aguarde alguns minutos e execute **[!UICONTROL Save & Test]**. |
| Não foi possível inscrever as chaves do host SSH | **[!UICONTROL Save & Test]** não pôde verificar ou armazenar chaves de host de base | Base inacessível da infraestrutura Adobe; falha de DNS; bloqueio de firewall [!DNL Commerce Intelligence] endereços IP; **Endereço Remoto** ou **Porta SSH** incorretos; falha de verificação de chave de host na base | Verificar o incluir na lista de permissões do firewall usando os endereços IP [!DNL Commerce Intelligence] na página de credenciais do banco de dados. Confirme se o bastião aceita SSH na porta configurada. Corrija os campos de conexão e execute **[!UICONTROL Save & Test]** novamente. |
| Chaves do host SSH ausentes ou inválidas | A verificação rígida bloqueou o túnel porque o material de confiança inscrito está ausente ou corrompido | A primeira conexão nunca concluiu o registro; falha na atualização anterior; a migração não copiou chaves; problema na infraestrutura do Adobe | Peça a um administrador para executar **[!UICONTROL Refresh SSH Host Keys]**, depois **[!UICONTROL Save & Test]**. Entre em contato com o Suporte do se o erro persistir. |
| Não foi possível concluir a atualização das chaves do host SSH | A atualização não atualizou as chaves inscritas | Falha de rede, DNS ou verificação durante a atualização; problema na infraestrutura do Adobe | Espere alguns minutos. Peça a um administrador para executar **[!UICONTROL Refresh SSH Host Keys]** novamente (segunda tentativa se a primeira falhar). Confirme a acessibilidade do bastião e o incluir na lista de permissões. Contate o Suporte se a conexão ainda falhar após duas tentativas de atualização e **[!UICONTROL Save & Test]**. |

## Lista de verificação de solução de problemas {#troubleshooting}

1. Confirme se as configurações de usuário do **Endereço Remoto**, da **Porta SSH** e do Linux correspondem às suas configurações de bastião.
1. Confirmar se o firewall permite os endereços IP [!DNL Commerce Intelligence] mostrados na página de credenciais do banco de dados.
1. Pergunte à sua equipe de infraestrutura se as chaves do host SSH no bastião foram alteradas recentemente.
1. Execute **[!UICONTROL Save & Test]** para validar configurações e registrar chaves, se ainda não existirem chaves.
1. Peça a um Administrador para executar **[!UICONTROL Refresh SSH Host Keys]**, aguarde alguns minutos e execute **[!UICONTROL Save & Test]** novamente. Se a primeira atualização não resolver o erro, repita esta etapa.
1. Se a conexão ainda mostrar um erro de chave de host SSH após duas tentativas de atualização, clique em **[!UICONTROL Contact Support]** na página de conexão (ou no canal de suporte da sua conta).

## Quando entrar em contato com o suporte da Adobe {#contact-support}

Entrar em contato com o suporte quando:

* Os erros de chave do host SSH continuam depois que um Administrador executa **[!UICONTROL Refresh SSH Host Keys]** duas vezes e **[!UICONTROL Save & Test]** ainda falha
* **[!UICONTROL Refresh SSH Host Keys]** nunca é concluído ou o status da conexão não muda após 15-30 minutos
* Os erros começaram imediatamente após a Adobe notificar você sobre a migração de conta ou a manutenção do servidor de dados
* As configurações básicas e o incluir na lista de permissões do firewall estão corretos, sua equipe não tem chaves de host giradas e você ainda não pode se conectar
* Você precisa de um Administrador para executar **[!UICONTROL Refresh SSH Host Keys]**, mas nenhum Administrador está disponível na conta

Inclua o nome da conexão, o horário aproximado da última **[!UICONTROL Save & Test]** tentativa de atualização e se as chaves do host bastion foram alteradas recentemente. Não envie chaves privadas ou senhas.

## Relacionados {#related}

* [Conectar MySQL via túnel SSH](mysql-via-ssh-tunnel.md)
* [Conectar MongoDB via túnel SSH](mongodb-via-ssh-tunnel.md)
* [Conectar o PostgreSQL pelo túnel SSH](postgresql.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
