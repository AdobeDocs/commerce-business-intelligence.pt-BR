---
title: Nova arquitetura
description: Saiba mais sobre os benefícios da mudança para a nova arquitetura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Nova arquitetura

Nossas equipes de produtos e engenharia têm se concentrado em tornar as melhorias mais abrangentes e altamente solicitadas possíveis no último ano. Estamos felizes em anunciar a disponibilidade de um novo [!DNL MBI] arquitetura de produto que torna essas melhorias uma realidade.

## Benefícios da nova arquitetura

* Crie novos tipos de colunas no data warehouse, incluindo colunas calculadas com SQL.
* Novas colunas estão disponíveis imediatamente.
* A latência de dados é significativamente melhorada.

## Benefícios técnicos

As principais diferenças estão listadas acima, mas o que mudou tecnicamente é a maneira como realizamos cálculos durante o ciclo de atualização. Os cálculos não são mais executados em cada coluna durante cada atualização; em vez disso, são executados sob demanda do Visual Report Builder.

### Migração para nova arquitetura

Como as contas são fundamentalmente criadas de forma diferente, não há processo automático que possamos usar para migrar seu data warehouse ou relatórios para uma nova conta de arquitetura, portanto, mudar para a nova arquitetura requer uma reimplementação da sua conta existente.

### Custo para migrar para a nova arquitetura

Nenhum custo adicional! Criaremos uma nova conta para que você comece a reimplementação, que é gratuita por pelo menos um mês. Isso permite que você tenha tempo para abrir ambas as contas, de modo que possa realizar mais facilmente a reimplementação e garanta que sua equipe não tenha uma lacuna no serviço.

### Tempo necessário para reimplementar a conta na nova arquitetura

Os tempos de reimplementação variam dependendo do que você deseja reconstruir. Recomendamos executar as seguintes etapas em sua conta existente para ter uma ideia do que estaria envolvido na reimplementação:

* Identifique um conjunto principal de relatórios/painéis.
* Identifique as métricas e dimensões necessárias para criar esses relatórios.
* Identifique as colunas necessárias para recriar essas métricas e dimensões.

Quando isso estiver concluído, você saberá quais dados precisam ser sincronizados com o data warehouse da nova arquitetura para reconstruir esses relatórios principais.

### Obter ajuda

O [!DNL MBI] A equipe de serviços pode realizar a reimplementação por um custo adicional. Entre em contato com nosso [Equipe de sucesso do cliente](../../guide-overview.md) e esteja preparado para fornecer uma lista de painéis/relatórios que você deseja priorizar a criação na nova conta

### Manter a arquitetura existente

Se esses recursos não forem importantes para você, você poderá manter sua conta existente. Não há custo adicional para manter sua conta existente, e continuaremos a oferecer suporte a essas contas sem alterações.
