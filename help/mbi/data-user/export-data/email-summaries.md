---
title: Criar resumos de email automatizados
description: Saiba como criar resumos de email automatizados.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Criar resumos de email automatizados

Resumos de email são uma poderosa ferramenta de comunicação que você pode usar para compartilhar o status e as tendências atuais de sua empresa com os principais participantes. Com resumos de email, você pode:

* Resumos gráficos por email que incluem relatórios
* Incluir ou excluir o autor do resumo do email de receber o email
* Agendar quando o email for enviado
* Editar, excluir e pausar resumos de email programados existentes

## Criar novo resumo de email

1. Clique em **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** na barra lateral.

   Se esta for a primeira vez que você estiver criando um resumo de email, esta página não exibirá nenhum resumo salvo.

1. Clique em **[!UICONTROL Create New Email Summary]** no canto superior direito.

1. Insira um nome para o resumo.

   Escolha um nome que transmita o que está incluído no resumo. Por exemplo, `AOV Comparison`.

1. No `Choose Content` selecione os relatórios que deseja incluir no resumo.

   Você pode selecionar até 10 relatórios de sua propriedade. Após selecionar um relatório, use os ícones que aparecem para selecionar se deseja que o relatório seja enviado como uma tabela ou um gráfico. Se você salvou o relatório como um número, só poderá enviá-lo como um número. Para obter informações sobre o envio de um resumo de email contendo um relatório com dados obsoletos, consulte [Gerenciamento das configurações da conta](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` os relatórios só estarão disponíveis se você estiver usando a nova arquitetura.

1. (Opcional) Selecione `Send Email To Me` se quiser receber o email.

1. Para incluir outros usuários no email, insira seus endereços de email no `Add Email Recipients` campo separado por vírgulas, espaços, guias ou ponto e vírgula.

## Agendar Resumo de Email

No `Set when to send the Email Summary` , é possível especificar quando enviar os resumos de email. As opções são:

* `Manual`
* `Once`
* `Repeating`

### Salvar resumo de email para ser enviado em uma data posterior

1. Selecionar `Manual` do `Set when to send the Email Summary` campo.

1. Clique em **[!UICONTROL Save]**.

   Isso salva o resumo na lista de resumos de email.

1. Quando estiver pronto para enviar o resumo, clique no ícone de engrenagem e selecione `Send Now`.

### Enviar resumo de email uma vez

1. Selecionar `Once` do `Set when to send the Email Summary` campo.

1. Especifique a data de início no `Select Start Date` calendário.

1. Especifique a hora para enviar o email no `Select time to send` campo.

### Criar Programação Repetitiva

1. Selecionar `Repeating` do `Set when to send the Email Summary` campo.

1. No `Set Frequency` , selecione `Daily`, `Weekly`ou `Monthly`.

1. Especifique a data de início no `Select Start Date` calendário.

1. Especifique a hora para enviar o email no `Select time to send` campo.

1. (Opcional) Para especificar uma data de término, selecione `End Date` e selecione a data final do calendário.

## Modificar Resumo de Email Existente

Depois de criar e salvar um resumo de email, a variável `Email Summaries` exibe uma lista de todos os resumos salvos. É possível expandir (`+`) cada linha para obter mais informações. As colunas nesta exibição são:

* `Email Name` - Nome do resumo do email
* `Content` - Tipo de conteúdo no resumo, como os nomes de qualquer relatório. Para obter informações sobre o envio de um resumo de email contendo um relatório com dados obsoletos, consulte [Gerenciamento das configurações da conta](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frequência, data e hora de envio do resumo do email
* `Recipients` - Recipients do email summary
* `Created Date` - Data de criação do resumo do email
* `Status` - `Paused` ou `Active`

Clique no ícone de engrenagem à direita de cada linha para:

* `Send Now` - Envia o resumo do email imediatamente para todos os recipients especificados
* `Edit` - Permite modificar os detalhes do resumo do email
* `Pause/Active` - Permite pausar o resumo do email de ser entregue ou habilitar o resumo com base em como ele foi configurado
* `Delete` - Exclui o resumo do email
