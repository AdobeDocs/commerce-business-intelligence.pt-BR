---
title: Reduzir o Tempo do Ciclo de Atualização
description: Saiba como reduzir o tempo do ciclo de atualização.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Reduzir o Tempo de Processamento do Ciclo de Atualização

O [!DNL Adobe Commerce Intelligence] sincroniza com seu banco de dados durante todo o dia para replicar novos dados, garantindo que seus painéis sempre mostrem as informações mais recentes.

Muitos fatores podem aumentar um tempo de atualização já longo. Determinados métodos de replicação, frequências de reverificação mais altas e o número de painéis e gráficos são apenas alguns colaboradores. Este tópico discute algumas práticas recomendadas para reduzir o tempo de atualização.

## Diminuir Frequência de Nova Verificação

Em uma tabela de banco de dados, pode haver colunas de dados com valores alteráveis. Por exemplo, em uma tabela **pedidos**, pode haver uma coluna chamada **status**. Quando um pedido é inicialmente gravado no banco de dados, a coluna de status pode conter o valor `pending`. A ordem é replicada em sua [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) com este valor `pending`.

As colunas alteráveis devem ser [verificadas novamente quanto a valores atualizados](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) ao longo do tempo. Por padrão, o [!DNL Commerce Intelligence] verifica novamente essas colunas durante cada atualização, mas se houver uma grande quantidade de dados a serem verificados novamente e replicados, isso poderá afetar negativamente seu tempo de atualização. Em vez de executar reverificações durante cada atualização, o Adobe recomenda definir a frequência de reverificação como diária, semanal ou mensal.

## Usar métodos de replicação incremental

Como mencionado acima, longos tempos de atualização estão diretamente relacionados à quantidade de dados que devem ser verificados novamente e replicados. [Os métodos de replicação incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) podem reduzir muito a quantidade de dados processados durante o ciclo de atualização. Sempre que possível, o Adobe recomenda o uso desses métodos ou a modificação do banco de dados para suportar um método incremental.

## Remover Gráficos Não Utilizados dos Painéis

No final do ciclo de atualização, [!DNL Commerce Intelligence] executa uma operação de cache para todos os gráficos. Um cache armazena dados para que solicitações futuras de informações possam ser concluídas mais rapidamente. Em [!DNL Commerce Intelligence], isso significa que os painéis são carregados rapidamente porque os gráficos não precisam consultar dados sempre que são carregados.

Como o [!DNL Commerce Intelligence] executa apenas operações de cache para gráficos encontrados em um painel, a remoção de gráficos não utilizados dos seus painéis diminui o tempo de atualização. Lembre-se de que o mesmo gráfico pode estar em vários painéis. Verifique com sua equipe se eles também removeram os gráficos não usados.

>[!NOTE]
>
>Remover gráficos do painel não exclui o gráfico. Você pode [adicioná-lo novamente a qualquer momento](../data-user/dashboards/add-charts-dashboard.md).

## Otimizar o Banco de Dados para Análise

Além de reavaliar as frequências de reverificação, os métodos de replicação e a utilidade do gráfico, você também pode [otimizar seu banco de dados para análise](../best-practices/opt-db-analysis.md).

## Encapsulamento

Se o tempo de atualização ainda parecer lento mesmo após a implementação dessas recomendações, [contate a equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
