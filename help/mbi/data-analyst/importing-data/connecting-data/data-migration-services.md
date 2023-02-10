---
title: Serviços de migração de dados
description: Saiba tudo o que você precisa para enviar uma solicitação e começar a migração.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Migração de dados

A migração para um novo schema de banco de dados, servidor ou banco de dados de relatórios não precisa ser estressante. Nosso **[!DNL Adobe Commerce Services - Analytics]** A equipe oferece assistência à migração - fazemos todo o trabalho pesado para que não seja necessário.

Para garantir que sua transição seja o mais tranquila possível, pedimos que você seja o mais detalhado possível ao enviar sua solicitação de migração. Neste artigo, há tudo o que você precisa para enviar uma solicitação e começar a migração. Fornecer-nos uma visão abrangente das suas necessidades garantirá que o seu projeto tenha um escopo adequado e que a estimativa seja precisa.

## Introdução {#started}

Antes de mergulharmos, você deverá saber as respostas para estas perguntas:

* **O novo banco de dados está em um novo servidor?** Antes de enviar uma solicitação, atualize as configurações da conexão de dados em **[!UICONTROL Manage Data** > **Connections]**. Se precisar de um atualizador para saber como fazer isso, acesse o [`Integrations`](../integrations/integrations.md) e localize as instruções para o tipo de banco de dados que você está usando.
* **Todos os dados históricos existem no novo banco de dados ou ele precisa ser migrado?** Podemos consolidar os dados históricos e novos durante o processo de migração. Mesmo que você não precise de uma consolidação, pedimos que nos informe em sua solicitação.

Depois de obter as respostas para o acima, precisaremos saber o tipo de migração: O novo banco de dados terá o [`same`](#sameschema) ou terá um [`different`](#newschema) esquema? Nas seções abaixo, você encontrará instruções detalhadas para cada tipo de migração.

## Migração para um novo banco de dados com o mesmo schema {#sameschema}

Ao enviar a solicitação, informe-nos que o esquema do banco de dados não está sendo alterado e que a conexão já está configurada em [!DNL MBI].

Se o banco de dados tiver um novo nome, inclua-o na solicitação para que seus painéis possam ser migrados corretamente.

Se o nome do banco de dados não estiver sendo alterado, a migração será concluída. Os painéis e relatórios serão atualizados após a conclusão da próxima atualização completa. Pedimos que continue a contactar-nos para que possamos ficar à frente de quaisquer problemas que possam resultar da migração.

## Migração para um novo banco de dados com um schema diferente {#newschema}

>[!IMPORTANT]
>
>Se determinadas colunas de dados não tiverem colunas equivalentes no novo banco de dados, há uma chance de certas análises serem perdidas no processo.

Para concluir com êxito esse tipo de migração, as colunas de dados existentes devem ser correspondidas com seus equivalentes no novo banco de dados. Isso não é obrigatório, mas executar a correspondência para nós ajudará a acelerar o tempo de resposta de sua solicitação e diminuir o preço da migração.

Se você se sentir confortável em fazer a correspondência sozinho, siga estas instruções e anexe a planilha concluída à sua solicitação:

1. Revise todas as tabelas e colunas que estão sendo sincronizadas na Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. Em uma planilha, crie uma guia para cada tabela a ser migrada para o novo banco de dados.
1. Em cada guia, crie uma coluna para todas as colunas existentes que precisam ser migradas. Recomendamos nomeá-lo como `Existing column name`.
1. Também é necessário fazer outra coluna para os equivalentes de coluna no novo banco de dados em cada guia da planilha. Recomendamos nomear a coluna como `New column name`.
1. Insira as colunas existentes e seus equivalentes. Se uma coluna existente não tiver um novo equivalente, basta inserir `N/A`.

   Além disso, se houver uma nova maneira de calcular as mesmas informações no novo banco de dados, insira-a no [`New column name`] coluna.

Veja um exemplo:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Se determinadas colunas de dados não tiverem colunas equivalentes no novo banco de dados, há uma chance de certas análises serem perdidas no processo.

## Como enviar uma solicitação? {#submitreq}

Você pode entrar em contato conosco [envio de um pedido de suporte](../../../guide-overview.md).

Se você seguir as etapas da seção anterior para criar a planilha correspondente à coluna, não se esqueça de anexá-la.

## O que vem a seguir? {#wrapup}

Determinar o escopo do projeto exige alguma colaboração entre você e o analista da equipe do Commerce Services que realiza a migração. A complexidade das alterações e a capacidade de resposta de você e do analista afeta diretamente o tempo que a migração pode levar. Depois de anotar os detalhes, será estabelecido um cronograma e enviado a você com uma declaração de trabalho.
