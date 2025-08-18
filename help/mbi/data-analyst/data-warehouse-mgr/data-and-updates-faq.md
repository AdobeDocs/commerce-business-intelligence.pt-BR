---
title: Informações de Dados e Atualizações
description: Saiba como verificar o status do ciclo de atualização.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Informações de Dados e Atualizações

* [Por que meus dados foram alterados?](#datachange)
* [Qual é a diferença entre uma atualização regular e forçada?](#regularforcedupdates)
* [Por que o ciclo de atualização leva muito tempo?](#updatecycletime)
* [Posso ser notificado quando um ciclo de atualização for concluído?](#notifyupdate)
* [Por que os dados do  [!DNL Google ECommerce]  são diferentes do meu banco de dados?](#ecommdatabase)
* [Como solucionar problemas de discrepância de dados?](#datadiscrepancy)

## Por que meus dados foram alterados? {#datachange}

Os valores do gráfico podem mudar durante o dia devido aos novos dados que estão sendo sincronizados com sua Data Warehouse. Além disso, os valores para colunas de dados existentes podem mudar devido a [reverificações](../data-warehouse-mgr/cfg-data-rechecks.md). Uma nova verificação é um processo que procura valores alterados em colunas de dados, como um status de pedido movendo de `open` para `shipped`.

Há algumas maneiras diferentes [de verificar o status do ciclo de atualizações](../../best-practices/check-update-cycle.md), dependendo das configurações de permissões do usuário.

## Qual é a diferença entre uma atualização regular e forçada? {#regularforcedupdates}

As atualizações regulares são **processos agendados**, enquanto as atualizações forçadas são **processos manuais iniciados por você**. Se você tiver horas de blecaute (ou um período em que [!DNL Commerce Intelligence] não deve atualizar seus dados), forçar uma atualização inicia um ciclo que não respeita as limitações do período de blecaute.

## Por que o ciclo de atualização leva muito tempo? {#updatecycletime}

Vários fatores podem aumentar um tempo de atualização já longo. Determinados [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md), [frequências de reverificação mais altas](../data-warehouse-mgr/cfg-data-rechecks.md) e o número de painéis e gráficos são apenas alguns colaboradores. A Adobe recomenda [redefinir algumas de suas configurações](../../best-practices/reduce-update-cycle-time.md) e [otimizar o banco de dados para análise](../../best-practices/opt-db-analysis.md) para reduzir os tempos de atualização.

## Posso ser notificado quando um ciclo de atualização for concluído? {#notifyupdate}

Se uma atualização estiver em andamento, há um link na página `Connections` que você pode usar para solicitar uma notificação por email após a conclusão do ciclo.

## Por que os dados do [!DNL Google ECommerce] são diferentes do meu banco de dados? {#ecommdatabase}

Discrepâncias entre [!DNL Google Analytics] e seu banco de dados podem surgir por vários motivos. O rastreamento não está ativado corretamente, os usuários que visitam de forma incógnita e os eventos de clique que não estão funcionando corretamente são apenas alguns exemplos. Se a receita e os pedidos não parecerem corretos, [consulte este tópico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=pt-BR) para diagnosticar um problema.

## Como solucionar problemas de discrepância de dados? {#datadiscrepancy}

A Adobe sabe que ver dados inconsistentes pode ser uma experiência frustrante. Tente usar o [tutorial de Lista de Verificação de Discrepância de Dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=pt-BR) ou [de Exportações de Dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=pt-BR) para diagnosticar o problema. Se você ainda estiver com problemas, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).
