---
title: Reduzir o Tempo do Ciclo de Atualização
description: Saiba como reduzir o tempo do ciclo de atualização.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# Reduzir o Tempo de Processamento do Ciclo de Atualização

O [!DNL Adobe Commerce Intelligence] sincroniza com seu banco de dados durante todo o dia para replicar novos dados, garantindo que seus painéis sempre mostrem as informações mais recentes.

Muitos fatores podem aumentar um tempo de atualização já longo. Determinados métodos de replicação, frequências de reverificação mais altas e o número de painéis e gráficos são apenas alguns colaboradores. Este tópico discute algumas práticas recomendadas para reduzir o tempo de atualização.

## Diminuir Frequência de Nova Verificação

Em uma tabela de banco de dados, pode haver colunas de dados com valores alteráveis. Por exemplo, em uma tabela **pedidos**, pode haver uma coluna chamada **status**. Quando um pedido é inicialmente gravado no banco de dados, a coluna de status pode conter o valor `pending`. A ordem é replicada no seu [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) com este valor `pending`.

As colunas alteráveis devem ser [verificadas novamente quanto a valores atualizados](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) ao longo do tempo. Por padrão, o [!DNL Commerce Intelligence] verifica novamente essas colunas durante cada atualização, mas se houver uma grande quantidade de dados a serem verificados novamente e replicados, isso poderá afetar negativamente seu tempo de atualização. Em vez de executar novas verificações durante cada atualização, a Adobe recomenda definir a frequência de novas verificações como diária, semanal ou mensal.

## Usar métodos de replicação incremental

Como mencionado acima, longos tempos de atualização estão diretamente relacionados à quantidade de dados que devem ser verificados novamente e replicados. [Os métodos de replicação incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) podem reduzir muito a quantidade de dados processados durante o ciclo de atualização. Sempre que possível, a Adobe recomenda usar esses métodos ou modificar seu banco de dados para suportar um método incremental.

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
