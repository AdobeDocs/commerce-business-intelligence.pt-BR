---
title: Configurando Verificações de Dados
description: Saiba como configurar colunas de dados com valores alteráveis.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Configurando Verificações de Dados

Em uma tabela de banco de dados, pode haver colunas de dados com valores alteráveis. Por exemplo, em uma tabela `orders` pode haver uma coluna chamada `status`. Quando um pedido é inicialmente gravado no banco de dados, a coluna de status pode conter o valor _pendente_. A ordem é replicada no seu [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) com este valor `pending`.

Os status dos pedidos podem mudar, embora nem sempre estejam com o status `pending`. Eventualmente, ele pode se tornar `complete` ou `cancelled`. Para garantir que o Data Warehouse sincronize essa alteração, a coluna deve ser verificada novamente quanto a novos valores.

Como isso se encaixa com os [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md) discutidos? O processamento de novas verificações varia de acordo com o método de replicação escolhido. O método de replicação `Modified\_At` é a melhor opção para processar valores alterados, já que não é necessário configurar novas verificações. Os métodos `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` exigem uma nova verificação da configuração.

Ao usar um desses métodos, as colunas alteráveis devem ser sinalizadas para nova verificação. Há três maneiras de fazer isso:

1. Um processo de auditoria que é executado como parte das colunas de sinalizadores de atualização a serem verificadas novamente.

   >[!NOTE]
   >
   >O auditor depende de um processo de amostragem e as colunas de alteração podem não ser capturadas imediatamente.

1. Você mesmo pode defini-las marcando a caixa de seleção ao lado da coluna no gerenciador do Data Warehouse, clicando em **[!UICONTROL Set Recheck Frequency]** e escolhendo um intervalo de tempo apropriado para quando você deve verificar as alterações.

1. Um membro da equipe do Data Warehouse [!DNL Adobe Commerce Intelligence] pode marcar manualmente as colunas para nova verificação no Data Warehouse. Se você tiver conhecimento de colunas que podem ser alteradas, entre em contato com a equipe do para solicitar que as novas verificações sejam definidas. Inclua uma lista de colunas, juntamente com a frequência, com sua solicitação.

## Verificar novamente as frequências {#frequency}

**Você sabia?**
Definir uma nova verificação em uma coluna `primary key` não verifica se há valores alterados na coluna. A tabela é verificada em busca de linhas excluídas e qualquer exclusão é removida do Data Warehouse.

Quando uma coluna é sinalizada para nova verificação, você também pode definir com que frequência uma nova verificação ocorre. Se uma determinada coluna não muda com frequência, uma nova verificação menos frequente pode [otimizar o ciclo de atualização](../../best-practices/reduce-update-cycle-time.md).

As opções de frequência são:

* `always` - nova verificação ocorre durante cada atualização
* `daily` - nova verificação ocorre primeira atualização após a meia-noite para o fuso horário declarado
* `weekly` - nova verificação ocorre após as 21h de atualização de sexta-feira toda semana para o seu fuso horário declarado
* `monthly` - a nova verificação ocorre após as 21h de atualização de sexta-feira a cada quatro semanas para o seu fuso horário declarado
* `once` - ocorre somente na próxima atualização (uma atualização única)

Como os tempos de atualização estão correlacionados à quantidade de dados que precisa ser sincronizada, a Adobe recomenda uma nova verificação do `daily`, `weekly` ou `monthly` em vez de cada atualização.

## Gerenciamento de frequências de reverificação {#manage}

As frequências de nova verificação podem ser gerenciadas na Data Warehouse clicando no nome de uma tabela e verificando colunas individuais. O status da sincronização e a frequência de nova verificação (as **Alterações?** coluna) é exibida para cada coluna na tabela.

Para alterar a frequência de reverificação, clique na caixa de seleção ao lado das colunas que deseja alterar. Clique na lista suspensa **[!UICONTROL Set Recheck Frequency]** e defina a frequência desejada.

![Data Warehouse Manager mostrando opções de reverificação da configuração](../../assets/dwm-recheck.png)

Às vezes, você pode ver `Paused` na coluna `Changes?`. Este valor é exibido quando o [método de replicação](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) da tabela é definido como `Paused`.

O [!DNL Adobe] recomenda revisar essas colunas para otimizar suas atualizações e garantir que as colunas alteráveis estejam sendo verificadas novamente. Se a frequência de nova verificação de uma coluna for alta, considerando a frequência com que os dados são alterados, a Adobe recomenda diminuí-la para otimizar suas atualizações.

Entre em contato conosco se tiver dúvidas ou para saber sobre os métodos de replicação atuais ou novas verificações.

**Relacionados:**

* [Redução dos tempos de atualização](../../best-practices/reduce-update-cycle-time.md)
* [Otimização do Banco de Dados para Análise](../../best-practices/opt-db-analysis.md)
