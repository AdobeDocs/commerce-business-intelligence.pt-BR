---
title: Otimização do Banco de Dados para Análise
description: Saiba como otimizar seu banco de dados para análise.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Developer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/5UkWGr-YOIfCy-BSomo2HWexXd-oM9ONvXpJkzyTPT0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 864
ht-degree: 0%

---

# Otimizar seu banco de dados

O principal benefício de usar um banco de dados operacional para [!DNL Adobe Commerce Intelligence] é que nada precisa ser compilado ou modificado para coletar dados. Informações valiosas já estão disponíveis - você só precisa desbloqueá-las.

Este tópico contém algumas recomendações para ajudá-lo a otimizar seu banco de dados para análise e desenhar insights acionáveis a partir de dados brutos.

## Não excluir dados

>[!TIP]
>
>As leis locais e internacionais que afetam sua empresa (e seus próprios termos de serviço) podem afetar os tipos de dados que você pode reter e por quanto tempo você pode mantê-los. O cumprimento dessas leis deve ser a sua primeira prioridade.

Quando um pedido é cancelado, um usuário desativa sua conta ou um produto é descontinuado, ele está tentando excluir as informações associadas no banco de dados. As tabelas crescem e eliminar a desordem parece uma ideia prudente. No entanto, a exclusão de linhas significa que essas informações são perdidas para sempre ou que é necessário pesquisar os backups antigos para localizá-las.

Em vez disso, você pode adicionar uma coluna de status à tabela, a qual indica quando a linha não está mais ativa ou relevante. Também é recomendável adicionar uma coluna que armazene a data em que a alteração foi feita ou criar um log para alterações históricas. Se as tabelas aumentarem o suficiente para que o desempenho comece a sofrer, considere arquivar os dados antigos em uma tabela usada para análise.

## Raramente Substituir Dados

A substituição de dados deve ser feita com moderação e cuidado.

Usando as datas de logon como exemplo, muitas empresas armazenam a data do último logon em vez de uma tabela de logons históricos. Embora talvez você só precise da última data de logon para fins funcionais, esses dados substituídos são uma grande perda da perspectiva do Analytics. Não manter um registro completo dessas ações elimina a capacidade de ver quantos usuários ficaram longe por longos períodos e depois foram reativados. Também impossibilita criar itens como análises de coorte de engajamento do usuário com base em logons.

Geralmente, se você estiver atualizando um registro devido a algum tipo de ação do usuário, não substitua as informações sobre uma ação do usuário anterior ou separada.

## Incluir `Updated_at` colunas para dados atualizados ao longo do tempo

Se as linhas de uma tabela tiverem valores alterados com o tempo, por exemplo, **order\_status** alterações de`processing` para `complete`, inclua uma coluna **updated\_at** para registrar quando ocorrer a alteração mais recente. Verifique se um valor de **atualizado\_às** está disponível ao inserir a nova linha de dados pela primeira vez, quando a data **atualizada\_às** corresponder à data **criada\_às**.

Além da otimização para análise, as colunas **updated\_at** também permitem que você use os [Métodos de replicação incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), o que pode ajudar a reduzir a duração dos ciclos de atualização.

## Armazenar Source de aquisição de usuário

Um dos erros mais comuns é que a [fonte de aquisição do usuário](../data-analyst/analysis/google-track-user-acq.md) (UAS) não está sendo armazenada no banco de dados operacional. Na maioria das situações quando isso é um problema, o UAS só está sendo rastreado por meio do [!DNL Google Analytics] ou alguma outra ferramenta de análise da Web. Embora essas ferramentas possam ser valiosas, há algumas desvantagens em armazenar UAS nelas exclusivamente; como, você não pode extrair dados no nível do usuário dessas ferramentas. Quando é possível, geralmente é um processo difícil. Deve ser fácil obter essas informações e combiná-las com dados de outras fontes, como as informações comportamentais e transacionais também armazenadas no banco de dados.

Armazenar o UAS em seu próprio banco de dados geralmente é a maior melhoria que uma empresa online pode fazer em suas capacidades analíticas. Isso permite a análise de vendas, envolvimento do usuário, períodos de retorno, valor vitalício do cliente, churn e outras métricas críticas por UAS. [Esses dados são cruciais ao decidir onde investir os recursos de marketing](../data-analyst/analysis/most-value-source-channel.md).

Muitas empresas se concentram apenas em encontrar canais que forneçam novos usuários pelo menor custo. Se você não estiver rastreando a qualidade dos usuários adquiridos de cada canal, corre o risco de atrair usuários que não geram valor comercial.

## Configuração da tabela de dados

### Definir uma chave primária

Uma [chave primária](https://en.wikipedia.org/wiki/Unique_key) é uma coluna (ou conjunto de colunas) inalterável que produz valores únicos dentro de uma tabela. As chaves primárias são incrivelmente importantes, pois garantem que suas tabelas sejam replicadas corretamente em [!DNL Commerce Intelligence].

Ao criar chaves primárias, use um tipo de dados de número inteiro para a coluna que aumenta automaticamente. A Adobe recomenda evitar o uso de várias chaves primárias de coluna, quando possível.

Se a tabela for uma visualização SQL, adicione uma coluna que possa agir como uma chave primária. [!DNL Commerce Intelligence] pode identificar automaticamente esta coluna como uma chave primária.

### Atribuir um Tipo de Dados à Coluna de Dados

Se uma coluna de dados não tiver um [tipo de dados](https://en.wikipedia.org/wiki/Data_type) atribuído, [!DNL Commerce Intelligence] adivinhará qual tipo de dados usar. Se o sistema adivinhar incorretamente, talvez você não possa realizar as análises relevantes até que a equipe de suporte da Adobe ajuste a coluna ao tipo de dados correto. Por exemplo, se uma coluna de data for adivinhada como um tipo de dados numérico, você poderá analisar a tendência ao longo do tempo usando essa dimensão de data.

### Adicionar prefixos às tabelas de dados se você tiver vários bancos de dados

Se você tiver mais de um banco de dados conectado ao [!DNL Commerce Intelligence], a Adobe recomenda adicionar prefixos às tabelas para evitar confusão. Os prefixos ajudam a lembrar de onde as métricas ou dimensões de dados são originadas.
