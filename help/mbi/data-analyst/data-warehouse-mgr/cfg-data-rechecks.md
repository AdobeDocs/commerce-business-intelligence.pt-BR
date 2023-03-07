---
title: Configurando Verificações de Dados
description: Saiba como configurar colunas de dados com valores alteráveis.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Configurando Verificações de Dados

Em uma tabela de banco de dados, pode haver colunas de dados com valores alteráveis. Por exemplo, em uma `orders`) tabela pode haver uma coluna chamada `status`. Quando um pedido é inicialmente gravado no banco de dados, a coluna de status pode conter o valor _pendente_. A ordem é replicada em seu [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) com este `pending` valor.

No entanto, os status dos pedidos podem mudar - eles nem sempre estão em uma `pending` status. Eventualmente, poderá tornar-se `complete` ou `cancelled`. Para garantir que sua Data Warehouse sincronize essa alteração, a coluna deve ser verificada novamente em busca de novos valores.

Como isso se encaixa no [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md) isso foi discutido? O processamento de novas verificações varia de acordo com o método de replicação escolhido. A variável `Modified\_At` o método de replicação é a melhor opção para processar valores alterados, já que as reverificações não precisam ser configuradas. A variável `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` Os métodos exigem a reverificação da configuração.

Ao usar um desses métodos, as colunas alteráveis devem ser sinalizadas para nova verificação. Há três maneiras de fazer isso:

* Um processo de auditoria que é executado como parte das colunas de sinalizadores de atualização a serem verificadas novamente.

   >[!NOTE]
   >
   >O auditor depende de um processo de amostragem e as colunas de alteração podem não ser capturadas imediatamente.

* Você mesmo pode defini-las marcando a caixa de seleção ao lado da coluna no gerenciador de Datas Warehouse e clicando em **[!UICONTROL Set Recheck Frequency]** e escolhendo um intervalo de tempo apropriado para quando você deve verificar as alterações.
* Um membro da [!DNL MBI] A equipe de Data Warehouse pode marcar manualmente as colunas para nova verificação na Data Warehouse. Se você tiver conhecimento de colunas que podem ser alteradas, entre em contato com a equipe do para solicitar que as novas verificações sejam definidas. Inclua uma lista de colunas, juntamente com a frequência, com sua solicitação.

## Verificar novamente as frequências {#frequency}

**Você sabia?**
Definindo uma reverificação em uma `primary key` A coluna não verifica se há valores alterados na coluna. A tabela é verificada em busca de linhas excluídas e qualquer exclusão é removida da Data Warehouse.

Quando uma coluna é sinalizada para nova verificação, você também pode definir com que frequência uma nova verificação ocorre. Se uma coluna específica não for alterada com frequência, a escolha de uma reverificação menos frequente poderá [otimizar o ciclo de atualização](../../best-practices/reduce-update-cycle-time.md).

As opções de frequência são:

* `always` - a nova verificação ocorre durante cada atualização
* `daily` - a nova verificação ocorre primeiro após a atualização da meia-noite para o fuso horário declarado
* `weekly` - a reverificação ocorre após as 21h00 e a atualização é feita toda semana para o fuso horário declarado
* `monthly` - a reverificação ocorre após as 21h da sexta-feira, a cada quatro semanas para o fuso horário declarado
* `once` - ocorre somente na próxima atualização (uma atualização única)

Como os tempos de atualização estão correlacionados à quantidade de dados que precisa ser sincronizada, o Adobe recomenda escolher um `daily`, `weekly`ou `monthly` verifique novamente em vez de cada atualização.

## Gerenciamento de frequências de reverificação {#manage}

As frequências de nova verificação podem ser gerenciadas na Data Warehouse clicando no nome de uma tabela e verificando colunas individuais. O status da sincronização e a frequência de reverificação (a variável **Mudanças?** coluna) é exibida para cada coluna na tabela.

Para alterar a frequência de reverificação, clique na caixa de seleção ao lado das colunas que deseja alterar. Em seguida, clique no link **[!UICONTROL Set Recheck Frequency]** e defina a frequência desejada.

![](../../assets/dwm-recheck.png)

Às vezes, você pode ver `Paused` no `Changes?` coluna. Esse valor é exibido quando a variável [método de replicação](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) está definida como `Paused`.

A Adobe recomenda revisar essas colunas para otimizar suas atualizações e garantir que as colunas alteráveis estejam sendo verificadas novamente. Se a frequência de nova verificação de uma coluna for alta, considerando a frequência com que os dados são alterados, o Adobe recomenda diminuí-la para otimizar suas atualizações.

Entre em contato conosco se tiver dúvidas ou para saber sobre os métodos de replicação atuais ou novas verificações.

**Relacionados:**

* [Redução dos tempos de atualização](../../best-practices/reduce-update-cycle-time.md)
* [Otimização do Banco de Dados para Análise](../../best-practices/opt-db-analysis.md)
