---
title: Nova arquitetura
description: Saiba mais sobre os benefícios de migrar para a nova arquitetura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nova arquitetura

As equipes de produtos e engenharia da MBI têm se concentrado em fazer as melhorias mais abrangentes e solicitadas possíveis para o ano passado. O Adobe tem o prazer de anunciar a disponibilidade de um novo [!DNL MBI] que torna essas melhorias uma realidade.

## Benefícios da nova arquitetura

* Crie tipos de colunas na Data Warehouse, incluindo colunas calculadas com SQL.
* Novas colunas estão disponíveis imediatamente.
* A latência de dados é drasticamente melhorada.

## Benefícios técnicos

As principais diferenças estão listadas acima, mas a principal alteração é a maneira como os cálculos são executados durante o ciclo de atualização. Os cálculos não são mais executados em cada coluna durante cada atualização; em vez disso, são executados sob demanda a partir do Report Builder visual.

### Migrando para a nova arquitetura

Como as contas são fundamentalmente criadas de forma diferente, não há um processo automático para migrar sua Data Warehouse ou relatórios para uma nova conta de arquitetura. A migração para a nova arquitetura requer uma reimplementação da conta existente.

### Custo para migrar para a nova arquitetura

Sem custo adicional! O Adobe criará essa nova conta para que você comece a reimplementação, que é gratuita por pelo menos um mês. Isso permite que você tenha tempo para abrir ambas as contas para executar mais facilmente a reimplementação e garantir que sua equipe não tenha uma lacuna no serviço.

### Tempo necessário para reimplementar a conta na nova arquitetura

Os tempos de reimplementação variam dependendo do que você deseja reconstruir. A Adobe recomenda executar as seguintes etapas na conta existente para ter uma ideia do que estaria envolvido na reimplementação:

* Identificar um conjunto principal de relatórios/painéis.
* Identifique as métricas e dimensões necessárias para criar esses relatórios.
* Identifique as colunas necessárias para recriar essas métricas e dimensões.

Quando estiver concluído, você saberá quais dados precisam ser sincronizados com a nova Data Warehouse de arquitetura para reconstruir esses relatórios principais.

### Obtendo ajuda

A variável [!DNL MBI] A equipe de serviços pode realizar a reimplementação por um custo extra. Entre em contato com [Equipe da conta Adobe](../../guide-overview.md) e esteja preparado para fornecer uma lista de painéis/relatórios que você deseja priorizar ao criar na nova conta

### Permanecendo com a arquitetura existente

Se esses recursos não forem importantes para você, é possível manter a conta existente. Não há custo extra para manter sua conta existente. O Adobe continua oferecendo suporte a essas contas sem alterações.
