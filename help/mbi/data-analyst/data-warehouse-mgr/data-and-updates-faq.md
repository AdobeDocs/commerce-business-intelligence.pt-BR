---
title: Informações de dados e atualizações
description: Saiba como verificar o status do ciclo de atualização.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Informações de dados e atualizações

* [Por que meus dados mudaram?](#datachange)
* [Qual é a diferença entre uma atualização regular e forçada?](#regularforcedupdates)
* [Por que o ciclo de atualização leva muito tempo?](#updatecycletime)
* [Posso ser notificado quando um ciclo de atualização for concluído?](#notifyupdate)
* [Por que [!DNL Google ECommerce] dados diferentes do meu banco de dados?](#ecommdatabase)
* [Como soluciono problemas de discrepância de dados?](#datadiscrepancy)

## Por que meus dados mudaram? {#datachange}

Os valores do gráfico podem ser alterados durante o dia, devido aos novos dados que estão sendo sincronizados com seu data warehouse. Além disso, os valores para colunas de dados existentes podem ser alterados devido a [verificações](../data-warehouse-mgr/cfg-data-rechecks.md). Uma reverificação é um processo que busca valores alterados em colunas de dados - por exemplo, um status de pedido que muda de `open` para `shipped`.

Há algumas maneiras diferentes [para verificar o status do ciclo de atualização](../../best-practices/check-update-cycle.md), dependendo do tipo de permissões do usuário.

## Qual é a diferença entre uma atualização regular e forçada? {#regularforcedupdates}

As atualizações regulares são **agendado** processos enquanto as atualizações forçadas são **processos manuais iniciados por você**. Se tiver horas de blecaute - ou um período em que [!DNL MBI] não deve atualizar seus dados - forçar uma atualização iniciará um ciclo que não respeite as limitações do período de blecaute.

## Por que o ciclo de atualização leva muito tempo? {#updatecycletime}

Muitos fatores podem adicionar a um tempo de atualização já longo. Determinado [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md), [frequências de reverificação mais altas](../data-warehouse-mgr/cfg-data-rechecks.md), e o número de painéis e gráficos são apenas alguns colaboradores. Recomendamos [redefinição de algumas de suas configurações](../../best-practices/reduce-update-cycle-time.md) e [otimização do banco de dados para análise](../../best-practices/opt-db-analysis.md) para reduzir os tempos de atualização.

## Posso ser notificado quando um ciclo de atualização for concluído? {#notifyupdate}

Absolutamente! Se uma atualização estiver em andamento, haverá um link no `Connections` página que você pode usar para solicitar uma notificação por email após a conclusão do ciclo.

## Por que[!DNL Google ECommerce]dados diferentes do meu banco de dados? {#ecommdatabase}

Discrepâncias entre [!DNL Google Analytics] e seu banco de dados pode surgir por vários motivos. O rastreamento não está sendo habilitado corretamente, os usuários visitando incógnito e os eventos de clique não estão funcionando corretamente são apenas alguns exemplos. Se suas receitas e pedidos não parecerem corretos, [usar este artigo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) para diagnosticar o problema.

## Como soluciono problemas de discrepância de dados? {#datadiscrepancy}

Sabemos que ver dados inconsistentes pode ser uma experiência frustrante. Tente usar nosso [Lista de verificação de discrepância de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) ou [Tutorial de exportações de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) para diagnosticar o problema. Se você ainda estiver preso, [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
