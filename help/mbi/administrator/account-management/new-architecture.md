---
title: Nova arquitetura
description: Saiba mais sobre os benefícios de migrar para a nova arquitetura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nova arquitetura

As equipes de Produtos e Engenharia do [!DNL Adobe Commerce Intelligence] concentraram-se em realizar as melhorias mais abrangentes e solicitadas possíveis no último ano. A Adobe tem o prazer de anunciar a disponibilidade de uma nova arquitetura de produto do [!DNL Commerce Intelligence] que torna essas melhorias uma realidade.

## Benefícios da nova arquitetura

* Crie tipos de colunas no Data Warehouse, incluindo colunas calculadas com SQL.
* Novas colunas estão disponíveis imediatamente.
* A latência de dados é drasticamente melhorada.

## Benefícios técnicos

As principais diferenças estão listadas acima, mas a principal alteração é a maneira como os cálculos são executados durante o ciclo de atualização. Os cálculos não são mais executados em cada coluna durante cada atualização; em vez disso, são executados sob demanda no Visual Report Builder.

### Migrando para a nova arquitetura

Como as contas são criadas de forma fundamentalmente diferente, não há um processo automático para migrar seu Data Warehouse ou relatórios para uma nova conta de arquitetura. A migração para a nova arquitetura requer a reimplementação da conta existente.

### Custo para migrar para a nova arquitetura

Sem custo adicional! A Adobe criará essa nova conta para você começar a reimplementação, que é gratuita por pelo menos um mês. Isso permite que você tenha tempo para abrir ambas as contas para executar mais facilmente a reimplementação e garantir que sua equipe não tenha uma lacuna no serviço.

### Tempo necessário para reimplementar a conta na nova arquitetura

Os tempos de reimplementação variam dependendo do que você deseja reconstruir. A Adobe recomenda executar as seguintes etapas na conta existente para ter uma ideia do que estaria envolvido na reimplementação:

* Identificar um conjunto principal de relatórios/painéis.
* Identifique as métricas e dimensões necessárias para criar esses relatórios.
* Identifique as colunas necessárias para recriar essas métricas e dimensões.

Quando estiver concluído, você saberá quais dados precisam ser sincronizados com a nova arquitetura do Data Warehouse para reconstruir esses relatórios principais.

### Obtendo ajuda

A [!DNL Adobe Commerce Intelligence] [Equipe de serviços](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) pode realizar sua reimplementação por um custo extra. Contate a sua [Equipe de Conta da Adobe](../../guide-overview.md#Submitting-a-Support-Ticket) e esteja preparado para fornecer uma lista de painéis/relatórios que você deseja priorizar a criar na nova conta

### Permanecendo com a arquitetura existente

Se esses recursos não forem importantes para você, é possível manter a conta existente. Não há custo extra para manter sua conta existente. A Adobe continua oferecendo suporte a essas contas sem alterações.
