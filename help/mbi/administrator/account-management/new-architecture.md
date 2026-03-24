---
title: Nova arquitetura
description: Saiba mais sobre os benefícios de migrar para a nova arquitetura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
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

A [!DNL Adobe Commerce Intelligence] [Equipe de serviços](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pode realizar sua reimplementação por um custo extra. Contate a sua [Equipe de Conta da Adobe](../../guide-overview.md#Submitting-a-Support-Ticket) e esteja preparado para fornecer uma lista de painéis/relatórios que você deseja priorizar a criar na nova conta

### Permanecendo com a arquitetura existente

Se esses recursos não forem importantes para você, é possível manter a conta existente. Não há custo extra para manter sua conta existente. A Adobe continua oferecendo suporte a essas contas sem alterações.
