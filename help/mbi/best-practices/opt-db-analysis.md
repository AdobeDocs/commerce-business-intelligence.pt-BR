---
title: Otimizando seu banco de dados para análise
description: Saiba como otimizar seu banco de dados para análise.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Otimizar o banco de dados

A principal vantagem de usar um banco de dados operacional para inteligência empresarial é que nada precisa ser criado ou modificado para coletar dados. Já existe informação valiosa; tudo o que você precisa fazer é desbloqueá-lo.

Este tópico contém algumas recomendações para ajudar você a otimizar seu banco de dados para análise e obter insights acionáveis dos dados brutos.

## Não excluir dados

>[!TIP]
>
>As leis locais e internacionais que afetam sua empresa (e seus próprios termos de serviço) podem afetar quais tipos de dados você pode reter e por quanto tempo pode retê-los. O cumprimento dessas leis deve ser a sua primeira prioridade.

Quando um pedido é cancelado, um usuário desativa sua conta ou um produto é descontinuado, é tentador excluir as informações associadas no banco de dados. As tabelas crescem e eliminar a desordem parece uma ideia prudente. No entanto, excluir linhas significa que essas informações serão perdidas para sempre ou que você precisará pesquisar por meio de backups antigos para encontrá-las.

Em vez disso, é possível adicionar uma coluna de status à tabela, que indicará quando a linha não está mais ativa ou relevante. Também é recomendável adicionar uma coluna que armazene a data em que a alteração foi feita ou criar um log para alterações históricas. Se as tabelas crescerem o suficiente para que o desempenho comece a sofrer, considere arquivar os dados antigos em uma tabela usada para análise.

## Raramente substituir dados

A substituição de dados deve ser feita com moderação e cuidado.

Usando datas de logon como exemplo, muitas empresas armazenarão a última data de logon em vez de uma tabela de logons históricos. Embora você possa precisar apenas da última data de logon para fins funcionais, esses dados sobrescritos são uma grande perda do ponto de vista analítico. Não manter um registro completo dessas ações elimina a capacidade de ver quantos usuários ficaram longe por longos períodos e depois foram reativados. Também torna impossível criar coisas como análises de coorte de engajamento do usuário com base em logons.

Como regra geral, se estiver atualizando um registro devido a algum tipo de ação do usuário, não substitua as informações sobre uma ação do usuário anterior ou separada.

## Incluir `Updated_at` Colunas para dados atualizados ao longo do tempo

Se as linhas de uma tabela tiverem valores alterados ao longo do tempo, por exemplo, **order\_status** alterações de`processing` para `complete`inclua um **atualizado\_at** para registrar quando ocorrer a última alteração. Certifique-se de que **atualizado\_at** está disponível ao inserir a nova linha de dados pela primeira vez, quando a variável **atualizado\_at** data corresponde a **criado\_em** data.

Além da otimização para análise, **atualizado\_at** colunas também permitem usar [Métodos de replicação incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), que pode ajudar a reduzir a duração dos ciclos de atualização.

## Armazenar fonte de aquisição do usuário

Um dos erros mais comuns é o [fonte de aquisição do usuário](../data-analyst/analysis/google-track-user-acq.md) (UAS) não sendo armazenado na base de dados operacional. Na maioria das situações em que isso é um problema, o UAS só está sendo rastreado [!DNL Google Analytics] ou alguma outra ferramenta de análise da Web. Embora estas ferramentas possam ser extremamente valiosas, existem algumas desvantagens em armazenar exclusivamente UAS nas mesmas; como, por exemplo, não é possível extrair dados a nível de usuário dessas ferramentas. Quando é possível, geralmente é um processo difícil. Deve ser fácil obter essas informações e combiná-las com dados de outras fontes, como as informações comportamentais e transacionais também armazenadas no banco de dados.

Armazenar o UAS em seu próprio banco de dados geralmente é a maior melhoria que uma empresa online pode fazer em seus recursos analíticos. Isso permite a análise de vendas, engajamento do usuário, períodos de recuperação, valor do tempo de vida do cliente, churn e outras métricas críticas por UAS. [Esses dados são cruciais ao decidir onde investir recursos de marketing](../data-analyst/analysis/most-value-source-channel.md).

Muitas empresas se concentram exclusivamente em encontrar canais que forneçam novos usuários com o menor custo, mas se você não estiver rastreando a qualidade dos usuários adquiridos de cada canal, correrá o risco de atrair usuários que não geram valor comercial.

## Configuração da tabela de dados

### Definir uma chave primária

A [chave primária](http://en.wikipedia.org/wiki/Unique_key) é uma coluna inalterável (ou um conjunto de colunas) que produz valores exclusivos em uma tabela. As chaves primárias são incrivelmente importantes, pois garantem que suas tabelas sejam replicadas corretamente em [!DNL MBI].

Ao criar chaves primárias, use um tipo de dados inteiro para a coluna que aumenta automaticamente. Também recomendamos evitar o uso de várias chaves primárias de coluna, quando possível.

Se a tabela for uma visualização SQL, adicione uma coluna que possa atuar como uma chave primária. [!DNL MBI] poderá identificar automaticamente essa coluna como uma chave primária.

### Atribuir um tipo de dados à coluna de dados

Se uma coluna de dados não tiver uma [tipo de dados](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] O adivinhe qual tipo de dados usar. Se o sistema adivinhar incorretamente, talvez você não consiga executar as análises relevantes até que nossa equipe de suporte ajuste a coluna para o tipo de dados adequado. Por exemplo, se uma coluna de data for adivinhada como um tipo de dados numéricos, você poderá analisar a tendência ao longo do tempo usando essa dimensão de data.

### Adicionar prefixos às suas tabelas de dados se houver vários bancos de dados

Se você tiver mais de um banco de dados conectado a [!DNL MBI], recomendamos que você adicione prefixos às tabelas para evitar confusão. Os prefixos ajudarão você a lembrar de onde as métricas ou dimensões de dados são originadas.
