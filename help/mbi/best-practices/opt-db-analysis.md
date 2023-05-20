---
title: Otimização do banco de dados para análise
description: Aprenda a otimizar seu banco de dados para análise.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Otimizar seu banco de dados

O principal benefício do uso de um banco de dados operacional para [!DNL Adobe Commerce Intelligence] é que nada precise ser criado ou modificado no solicitar para coletar dados. Informações valiosas já estão lá: você só precisa desbloqueá-las.

Este tópico contém algumas recomendações para ajudar você a otimizar seu banco de dados para análise e desenhar insights acionáveis a partir de dados brutos.

## Não Excluir dados

>[!TIP]
>
>As leis locais e internacionais que afetam sua empresa (e seus próprios termos de serviço) podem afetar os tipos de dados que podem ser mantidos e por quanto tempo você pode mantê-lo. A conformidade com essas leis deve ser sua primeira prioridade.

Quando um solicitar é cancelado, um usuário desativa seu conta, ou um produto é descontinuado, é tentador excluir as informações associadas no banco de dados. Tables crescer e eliminar a desordem parece curtir uma ideia prudente. No entanto, a exclusão de linhas significa que essas informações são perdidas para sempre ou que você precisa analisar os backups antigos para localizá-la.

Em vez disso, você pode adicionar uma coluna de status à tabela que indica quando a linha não está mais ativa ou relevante. Também é recomendável adicionar uma coluna que armazene a data em que a alteração foi feita ou crie um log para alterações históricas. Se as tabelas aumentarem o suficiente para que o desempenho comece a ser prejudicado, considere o arquivamento dos dados antigos em uma tabela usada para análise.

## Raramente substituir dados

A substituição de dados deve ser feita com moderação e cuidado.

Usando datas fazer logon como exemplo, muitas empresas armazenamento a última data de fazer logon em vez de uma tabela de logons históricos. Embora você só possa precisar da última fazer logon data para fins funcionais, os dados substituídos são uma grande perda de uma perspectiva de análise. Não manter um log completo dessas ações elimina a capacidade de ver quantos usuários ficam distantes por longos períodos de tempo e, em seguida, reativados. Também torna impossível build coisas curtir engajamento do usuário análises coorte com base em logons.

Geralmente, se você estiver atualizando um registro devido a algum tipo de usuário ação, não substitua as informações sobre uma ação usuário anterior ou separada.

## Incluir `Updated_at` colunas para dados atualizados ao longo do tempo

Se as linhas de uma tabela tiverem de alterar valores ao longo do tempo, por exemplo, **solicitar \ _status** alterações de `processing` para `complete` , inclua uma **coluna de \ _at** atualizada para registrar quando a última alteração ocorrer. Certifique-se de que um valor de **\ _at** atualizado esteja disponível ao inserir pela primeira vez a nova linha de dados, quando a data de **atualização \ _at** corresponde à data de criação de **\ _at** .

Além da otimização para análise, **as colunas atualizadas para o _at** também permitem usar [ métodos ](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) de replicação incremental, o que pode ajudar a reduzir o tamanho dos ciclos de atualização.

## Armazenamento de aquisição do usuário Origem

Um dos erros mais comuns é que a [ usuário atração fonte ](../data-analyst/analysis/google-track-user-acq.md) (uas) não está sendo armazenada no banco de dados operacional. Na maioria das situações, quando isso é um problema, o UAS está sendo rastreado por [!DNL Google Analytics] qualquer outro análise da web ferramenta. Embora essas ferramentas possam ser valiosas, há algumas desvantagens em armazenar exclusivamente os UAS. como, você não pode extrair dados de nível usuário dessas ferramentas. Quando possível, geralmente é um processo difícil. Deve ser fácil obter essas informações e se unir a dados de outras fontes, como as informações comportamentais e transacionais também armazenadas no banco de dados.

O armazenamento de UAS em seu próprio banco de dados geralmente é a maior melhoria que um ebusiness pode fazer em seus recursos analíticos. Isso permite a análise de vendas, engajamento do usuário, períodos de retorno, valor vitalício do cliente, churn e outras métricas de crítico por UAS. [Esses dados são cruciais ao decidir onde investir marketing recursos ](../data-analyst/analysis/most-value-source-channel.md) .

Muitas empresas focalizar unicamente para encontrar canais que fornecem novos usuários pelo menor custo. Se você não estiver rastreamento a qualidade dos usuários adquiridos de cada canal, correrá o risco de atrair usuários que não geram valor comercial.

## Configuração da tabela de dados

### Definir uma chave primária

Uma [ chave ](https://en.wikipedia.org/wiki/Unique_key) primária é uma coluna inalterável (ou conjunto de colunas) que produz valores únicos em uma tabela. As chaves primárias são incrivelmente importantes, pois garantem que suas tabelas sejam replicadas corretamente no [!DNL Commerce Intelligence] .

Ao criar chaves primárias, use um tipo de dados Integer para a coluna que aumenta automaticamente. Adobe Systems recomenda evitar o uso de chaves primárias de várias colunas sempre que possível.

Se sua tabela for um visualização SQL, adicione uma coluna que possa atuar como uma chave primária. [!DNL Commerce Intelligence] pode identificar automaticamente esta coluna como uma chave primária.

### Atribuir um Tipo de Dados à Coluna de Dados

Se uma coluna de dados não tiver um tipo ](https://en.wikipedia.org/wiki/Data_type) de dados atribuído [ , [!DNL Commerce Intelligence] o adivinhará o tipo de dados a ser usado. Se o sistema adivinhar incorretamente, você pode não conseguir executar as análises relevantes até que o suporte a Adobe Systems equipe ajusta a coluna para o tipo de dados apropriado. Por exemplo, se uma coluna de data for adivinhada como um tipo de dados numérico, você poderá usar uma tendência ao longo do tempo usando essa data dimensão.

### Adicione prefixos aos seus dados Tables se você tiver vários bancos de dados

Se você tiver mais de um banco de dados conectado [!DNL Commerce Intelligence] , o Adobe Systems recomenda adicionar prefixos às tabelas para evitar confusão. Os prefixos ajudam você a lembrar de onde as métricas ou dimensões de dados são originadas.
