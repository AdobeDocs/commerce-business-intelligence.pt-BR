---
title: Configuração de verificações de dados
description: Saiba como configurar colunas de dados com valores que podem ser alterados.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Configuração de verificações de dados

Em uma tabela de banco de dados, pode haver colunas de dados com valores que podem ser alterados. Por exemplo, em um `orders`) pode haver uma coluna chamada `status`. Quando um pedido é gravado inicialmente no banco de dados, a coluna de status pode conter o valor _pendente_. A ordem será replicada em sua [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) com `pending` valor.

No entanto, os status da ordem podem mudar; eles nem sempre estarão em um `pending` status. Eventualmente pode se tornar `complete` ou `cancelled`. Para garantir que sua Data Warehouse sincronize essa alteração, a coluna precisará ser verificada novamente em busca de novos valores.

Como isso se encaixa no cenário [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md) discutimos? O processamento de verificações varia com base no método de replicação escolhido. O `Modified\_At` o método de replicação é a melhor opção para processar valores que mudam, pois as verificações novamente não precisam ser configuradas. O `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` métodos exigem configuração de reverificação.

Ao usar qualquer um desses métodos, as colunas alteráveis devem ser sinalizadas para nova verificação. Há três maneiras de fazer isso:

* Um processo de auditoria que é executado como parte da atualização sinalizará colunas a serem remarcadas.

   >[!NOTE]
   >
   >O auditor depende de um processo de amostragem e as colunas em mudança não podem ser capturadas imediatamente.

* Você mesmo pode defini-los marcando a caixa de seleção ao lado da coluna no gerenciador de Datas Warehouse, clicando em **[!UICONTROL Set Recheck Frequency]** e escolhendo um intervalo de tempo apropriado para quando devemos verificar as alterações.
* Um membro da [!DNL MBI] A equipe de Datas Warehouse pode marcar manualmente as colunas para verificação novamente em sua Data Warehouse. Se você tiver conhecimento de colunas alteráveis, entre em contato com a equipe para solicitar que as verificações novamente sejam definidas. Inclua uma lista de colunas, juntamente com a frequência, com sua solicitação.

## Verificar frequências novamente {#frequency}

**Você sabia?**
Configurar uma reverificação em um `primary key` não verifica se há valores alterados na coluna. A tabela será verificada para linhas excluídas e quaisquer exclusões serão eliminadas da Data Warehouse.

Quando uma coluna é sinalizada para reverificação, você também pode definir a frequência com que uma reverificação ocorre. Se uma coluna específica for alterada com menos frequência, escolher uma verificação menos frequente pode [otimizar seu ciclo de atualização](../../best-practices/reduce-update-cycle-time.md).

As opções de frequência são:

* `always` - a verificação ocorre durante cada atualização
* `daily` - a reverificação ocorre na primeira atualização pós-meia-noite para o fuso horário declarado
* `weekly` - a reverificação ocorre depois das 21 horas, atualização de sexta-feira toda semana para o fuso horário declarado
* `monthly` - a reverificação ocorre depois das 21h, atualização sexta-feira a cada 4 semanas para o fuso horário declarado
* `once` - ocorre somente na próxima atualização (uma atualização única)

Como os tempos de atualização estão correlacionados à quantidade de dados que precisa ser sincronizada, recomendamos escolher uma `daily`, `weekly`ou `monthly` marque novamente em vez de cada atualização.

## Gerenciamento de frequências de reverificação {#manage}

A verificação de frequências pode ser gerenciada na Data Warehouse clicando no nome da tabela e verificando colunas individuais. O status da sincronização e a frequência de reverificação (a variável **Mudanças?** ) será exibida para cada coluna na tabela.

Para alterar a frequência de reverificação, clique na caixa de seleção ao lado das colunas que você deseja alterar e clique no botão **[!UICONTROL Set Recheck Frequency]** e defina a frequência desejada.

![](../../assets/dwm-recheck.png)

Às vezes, você pode ver `Paused` no `Changes?` coluna. Esse valor será exibido quando a tabela [método de replicação](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) está definida como `Paused`.

Recomendamos revisar essas colunas para otimizar suas atualizações e garantir que as colunas alteráveis estejam sendo remarcadas. Se a frequência de reverificação de uma coluna for desnecessariamente alta, considerando a frequência com que os dados serão alterados, recomendamos diminuí-la para otimizar suas atualizações.

Entre em contato conosco com perguntas ou para saber sobre os métodos de replicação ou reverificações atuais.

**Relacionadas:**

* [Redução dos tempos de atualização](../../best-practices/reduce-update-cycle-time.md)
* [Otimização do Banco de Dados para Análise](../../best-practices/opt-db-analysis.md)
