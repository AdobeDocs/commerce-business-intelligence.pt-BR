---
title: Reduza o tempo do ciclo de atualização
description: Saiba como reduzir o tempo do ciclo de atualização.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Reduza o tempo de processamento do ciclo de atualização

[!DNL MBI] sincroniza com seu banco de dados durante todo o dia para replicar novos dados, garantindo que seus painéis sempre mostrem as informações mais recentes.

Muitos fatores podem adicionar a um tempo de atualização já longo. Determinados métodos de replicação, frequências de reverificação mais altas e o número de painéis e gráficos são apenas alguns colaboradores. Este tópico discute algumas práticas recomendadas para reduzir os tempos de atualização.

## Diminuir Frequência de Verificação

Em uma tabela de banco de dados, pode haver colunas de dados com valores que podem ser alterados. Por exemplo, em um **ordens** pode haver uma coluna chamada **status**. Quando um pedido é gravado inicialmente no banco de dados, a coluna de status pode conter o valor `pending`. A ordem será replicada em sua [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) com `pending` valor.

Colunas que podem ser alteradas precisam ser [verificado novamente se há valores atualizados](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) ao longo do tempo. Por padrão, [!DNL MBI] verifica novamente essas colunas durante cada atualização, mas se houver uma grande quantidade de dados a serem verificados e replicados, isso pode afetar negativamente o tempo de atualização. Em vez de executar verificações novamente durante cada atualização, recomendamos definir a frequência de verificação como diária, semanal ou mensal.

## Usar métodos de replicação incremental

Como mencionado acima, longos tempos de atualização estão diretamente relacionados à quantidade de dados que deve ser reverificada e replicada. [Métodos de replicação incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) O pode reduzir bastante a quantidade de dados processados durante o ciclo de atualização. Sempre que possível, recomendamos usar esses métodos ou fazer modificações no seu banco de dados para oferecer suporte a um método incremental.

## Remover Gráficos Não Utilizados dos Painéis

No final do ciclo de atualização, [!DNL MBI] O executa uma operação de cache para todos os gráficos. Um cache armazena dados para que solicitações futuras de informações possam ser concluídas mais rapidamente. Em [!DNL MBI], isso significa que os painéis serão carregados rapidamente, pois os gráficos não precisam consultar dados sempre que carregarem.

Since [!DNL MBI] O só executa operações de cache para gráficos encontrados em um painel, a remoção de gráficos não utilizados de seus painéis diminuirá o tempo de atualização. Lembre-se de que o mesmo gráfico pode estar em vários painéis. Verifique com sua equipe para garantir que eles também removeram todos os gráficos não utilizados.

>[!NOTE]
>
>Remover gráficos de seu painel não exclui o gráfico. Você pode [adicione-o a qualquer momento](../data-user/dashboards/add-charts-dashboard.md).

## Otimizar seu banco de dados para análise

Além de reavaliar frequências de reverificação, métodos de replicação e utilidade do gráfico, você também pode [otimizar seu banco de dados para análise](../best-practices/opt-db-analysis.md).

## Quebra de linha

Se o tempo de atualização ainda parecer lento mesmo após a implementação dessas recomendações, [entre em contato com nossa equipe de suporte](../guide-overview.md).
