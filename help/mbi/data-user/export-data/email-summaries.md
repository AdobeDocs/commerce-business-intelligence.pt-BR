---
title: Criar resumos automatizados de email
description: Saiba como criar resumos automatizados de email.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Criar resumos automatizados de email

Os resumos de email são uma poderosa ferramenta de comunicação que pode ser usada para compartilhar o status e as tendências da sua empresa com as principais partes interessadas. Com os resumos de email, você pode:

* Resumos gráficos de email que incluem relatórios
* Incluir ou excluir o autor do resumo de email do recebimento do email
* Agendar quando o email será enviado
* Editar, excluir e pausar os resumos de emails agendados existentes

## Criar novo resumo de email

1. Clique em **[!DNL Manage Data]** e depois em **[!UICONTROL Email Summary]** na barra lateral.

   Se esta for a primeira vez que você está criando um resumo de email, esta página não exibirá resumos salvos.

1. Clique em **[!UICONTROL Create New Email Summary]** no canto superior direito.

1. Insira um nome para o resumo.

   Escolha um nome que transmita o que está incluído no resumo. Por exemplo, `AOV Comparison`.

1. Na seção `Choose Content`, selecione os relatórios que deseja incluir no resumo.

   Há duas opções para adicionar conteúdo:

   * **Selecionar Relatórios Individuais** - Escolha relatórios específicos nos seus painéis
   * **Selecionar Painel Inteiro** - Incluir todos os relatórios de um painel conforme eles aparecem no layout do painel

   Você pode selecionar até dez relatórios. Após selecionar um relatório, use os ícones exibidos para selecionar se deseja que o relatório seja enviado como uma tabela ou um gráfico. Se você tiver salvo o relatório como um número, só será possível enviá-lo como um número. Para obter informações sobre como enviar um resumo de email contendo um relatório com dados obsoletos, consulte [Gerenciando as configurações da sua conta](../../administrator/account-management/managing-account-settings.md).

   Para adicionar painéis inteiros, você tem as seguintes opções de formato e exclusão:

   * Alterar o formato do relatório para um gráfico ou uma tabela
   * Impedir a inclusão de relatórios no email
   * Selecione para incluir um arquivo CSV para relatórios tabulares - isso permite que os recipients acessem dados brutos e exportáveis diretamente da caixa de entrada.

   >[!NOTE]
   >
   >Os relatórios do `Cohort` só estarão disponíveis se você estiver usando a nova arquitetura.

   >[!NOTE]
   >
   >Anexos CSV grandes são suportados com um total combinado de até 25 MB por email.

1. (Opcional) Selecione `Send Email To Me` se desejar receber o email.

1. Para incluir outros usuários no email, insira seus endereços de email no campo `Add Email Recipients` separados por vírgulas, espaços, tabulações ou ponto e vírgula.

## Agendar resumo de email

No campo `Set when to send the Email Summary`, é possível especificar quando enviar os resumos de email. As opções são:

* `Manual`
* `Once`
* `Repeating`

### Salvar resumo de email para ser enviado em uma data posterior

1. Selecione `Manual` no campo `Set when to send the Email Summary`.

1. Clique em **[!UICONTROL Save]**.

   Isso salva o resumo na lista de resumos de email.

1. Quando estiver pronto para enviar o resumo, clique no ícone de engrenagem e selecione `Send Now`.

### Enviar resumo de email uma vez

1. Selecione `Once` no campo `Set when to send the Email Summary`.

1. Especifique a data de início no calendário `Select Start Date`.

1. Especifique a hora para enviar o email no campo `Select time to send`.

### Criar programação repetitiva

1. Selecione `Repeating` no campo `Set when to send the Email Summary`.

1. No campo `Set Frequency`, selecione `Daily`, `Weekly` ou `Monthly`.

1. Especifique a data de início no calendário `Select Start Date`.

1. Especifique a hora para enviar o email no campo `Select time to send`.

1. (Opcional) Para especificar uma data de término, selecione `End Date` e selecione a data de término no calendário.

## Modificar resumo de email existente

Depois de criar e salvar um resumo de email, a página `Email Summaries` exibe uma lista de todos os resumos salvos. Você pode expandir (`+`) em cada linha para obter mais informações. As colunas desta exibição são:

* `Email Name` - Nome do resumo de email
* `Content` - Tipo de conteúdo no resumo, como os nomes de todos os relatórios
* `Scheduled` - Frequência, data e hora em que o resumo do email é enviado
* `Recipients` - Destinatários do resumo de email
* `Created Date` - Data de criação do resumo do email
* `Status` - `Paused` ou `Active`

>[!NOTE]
>
>Para obter informações sobre como enviar um resumo de email contendo um relatório com dados obsoletos, consulte [Gerenciando as configurações da sua conta](../../administrator/account-management/managing-account-settings.md).

Clique no ícone de engrenagem à direita de cada linha para:

* `Send Now` - Enviar o resumo do email imediatamente para todos os destinatários especificados
* `Edit` - Modificar os detalhes do resumo do email
* `Pause/Active` - Pausar ou ativar a entrega de resumo de email
* `Delete` - Excluir o resumo do email
