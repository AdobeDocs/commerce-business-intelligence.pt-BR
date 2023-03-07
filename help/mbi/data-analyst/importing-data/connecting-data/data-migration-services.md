---
title: Serviços de migração de dados
description: Saiba tudo de que precisa para enviar uma solicitação e começar a migração.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Migração de dados

A migração para um novo esquema de banco de dados, servidor ou banco de dados de relatórios não precisa ser complicada. A variável **[!DNL Adobe Commerce Services - Analytics]** A equipe do oferece assistência à migração.

Para garantir que sua transição seja a mais tranquila possível, você deve estar o mais detalhado possível ao enviar sua solicitação de migração. Neste artigo, há tudo o que você precisa para enviar uma solicitação e começar a migração. Fornecer uma visão abrangente de suas necessidades garante que seu projeto tenha o escopo adequado e que a estimativa seja precisa.

## Introdução {#started}

Antes de começar, você deve saber as respostas para estas perguntas:

* **O novo banco de dados está em um novo servidor?** Antes de enviar uma solicitação, atualize as configurações da conexão de dados em **[!UICONTROL Manage Data** > **Connections]**. Se precisar de uma atualização sobre como fazer isso, acesse o [`Integrations`](../integrations/integrations.md) e localize as instruções para o tipo de banco de dados que você está usando.
* **Todos os seus dados históricos existem no novo banco de dados ou precisam ser migrados?** Você pode consolidar os dados históricos e novos durante o processo de migração. Mesmo que você não precise de uma consolidação, informe-nos em sua solicitação.

Depois de obter as respostas para as perguntas acima, é necessário saber o tipo de migração: o novo banco de dados terá a [`same`](#sameschema) esquema ou terá um [`different`](#newschema) esquema? Nas seções abaixo, você encontrará instruções detalhadas para cada tipo de migração.

## Migração para um novo banco de dados com o mesmo esquema {#sameschema}

Ao enviar a solicitação, informe que o esquema do banco de dados não está sendo alterado e que a conexão já está configurada no [!DNL MBI].

Se o banco de dados tiver um novo nome, inclua-o na solicitação para que seus painéis possam ser migrados corretamente.

Se o nome do banco de dados não for alterado, a migração será concluída. Os painéis e relatórios serão atualizados após a conclusão da próxima atualização completa. Entre em contato com o Adobe para que você possa se manter à frente de qualquer problema que possa resultar da migração.

## Migração para um novo banco de dados com um schema diferente {#newschema}

>[!IMPORTANT]
>
>Se determinadas colunas de dados não tiverem colunas equivalentes no novo banco de dados, há uma chance de determinadas análises serem perdidas no processo.

Para concluir com êxito esse tipo de migração, as colunas de dados existentes devem corresponder aos seus equivalentes no novo banco de dados. Isso não é obrigatório, mas fazer a correspondência para nós ajuda a acelerar o tempo de inversão de sua solicitação e diminuir o preço da migração.

Se você se sentir confortável em fazer a correspondência sozinho, siga estas instruções e anexe a planilha concluída à sua solicitação:

1. Revise todas as tabelas e colunas que estão sendo sincronizadas com sua Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. Em uma planilha, crie uma guia para cada tabela a ser migrada para o novo banco de dados.
1. Em cada guia, crie uma coluna para todas as colunas existentes que precisam ser migradas. O Adobe recomenda dar um nome semelhante a `Existing column name`.
1. Você também precisa fazer outra coluna para os equivalentes da coluna no novo banco de dados em cada guia da planilha. O Adobe recomenda nomear a coluna como `New column name`.
1. Insira as colunas existentes e seus equivalentes. Se uma coluna existente não tiver um novo equivalente, insira `N/A`.

   Além disso, se houver uma nova maneira de calcular as mesmas informações no novo banco de dados, insira-as no campo [`New column name`] coluna.

Veja um exemplo:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Se determinadas colunas de dados não tiverem colunas equivalentes no novo banco de dados, há uma chance de determinadas análises serem perdidas no processo.

## Como faço para enviar uma solicitação? {#submitreq}

Entre em contato conosco [enviar uma solicitação de suporte](../../../guide-overview.md).

Se você seguiu as etapas da seção anterior para criar a planilha correspondente à coluna, não se esqueça de anexá-la.

## O que vem a seguir? {#wrapup}

A determinação do escopo do projeto exige alguma colaboração entre você e o analista da equipe de Commerce Services que está executando a migração. A complexidade das alterações e a capacidade de resposta de você e do analista afetam diretamente o tempo que a migração pode levar. Depois de detalhar, uma linha do tempo será estabelecida e enviada a você com uma declaração de trabalho.
