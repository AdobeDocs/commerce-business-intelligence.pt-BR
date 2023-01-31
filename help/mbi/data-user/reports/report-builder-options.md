---
title: Escolher um construtor de relatórios
description: Saiba como escolher o construtor de relatórios.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Escolher um construtor de relatórios

>[!NOTE]
>>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).


Todos nós gostamos de ter opções. Mas, quando confrontados com escolhas, alguns de nós podem ficar de braços cruzados e congelar a ideia de termos de nos comprometer com uma decisão. As opções são ótimas, mas também podem ser esmagadoras e confusas.

Agora que você tem mais opções para criar análises, às vezes pode ser difícil saber exatamente qual sabor do construtor de relatórios atenderá às suas necessidades. Se você precisar de orientação sobre como escolher a melhor maneira de criar sua análise, este artigo é para você.

## Quando devo usar a variável `SQL Report Builder`? {#whensql}

Veja alguns dos motivos mais comuns que você usaria o Report Builder SQL sobre o Report Builder tradicional.

### Se quiser usar funções específicas do SQL...

Parte da beleza do `SQL Report Builder` Ele oferece a capacidade de usar funções que não estão disponíveis no Gerenciador de Datas Warehouse. No passado, um analista pode ter tido que entrar para ajudá-lo a entender sua visão por completo.

O Report Builder SQL oferece suporte a funções como [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) e [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que não era possível usar anteriormente. Você pode acessar o [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), mas algumas outras funções específicas do SQL incluem:

* [`Bitwise aggregate` funções](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operador](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Se quiser fazer alguns testes..

Se quiser tentar técnicas e estratégias diferentes para descobrir o que funciona melhor para a análise, talvez você queira usar a variável `SQL Report Builder`. A criação de colunas no Gerenciador de Datas Warehouse leva tempo e as colunas criadas usando o DWM dependem dos ciclos de atualização.

Na melhor das hipóteses, é necessário aguardar um ciclo de atualização antes de usar a coluna. Se você perceber que cometeu um erro ao criar a coluna, você terá que aguardar *two* ciclos: um para preencher inicialmente a coluna e outro ciclo para que as revisões se propaguem.

### Se você só usará uma nova coluna uma vez...

Como mencionado na seção acima, a criação de uma nova coluna no Gerenciador de Datas Warehouse leva tempo. Caso planeje usar apenas uma coluna criada em um relatório, sugerimos usar a variável `SQL Report Builder`. Isso eliminará a necessidade de aguardar a conclusão de um ciclo de atualização, fazendo com que você volte a trabalhar mais rapidamente.

### Se estiver trabalhando com dados que têm uma relação um para muitos...

Em alguns casos, a estrutura de seus dados pode fazer com que o `SQL Report Builder` uma escolha mais eficiente e lógica para criar a análise. Criar colunas para relacionamentos de um para um é muito simples no Gerenciador de Datas Warehouse, mas as coisas podem ficar um pouco confusas quando você está lidando com relacionamentos de um para muitos.

Digamos que um único produto seja considerado parte de várias categorias de produto e você gostaria de visualizar a receita associada a cada categoria de produto. Tentar criar essa relação usando o DWM pode ser entediante e difícil, mas escrever uma consulta SQL pode ser um pouco mais simples:

![](../../assets/When_should_I_use_the_RB_2.png)

## Quando devo usar o Report Builder tradicional? {#whentraditionalrb}

Enquanto a variável `SQL Report Builder` oferece mais controle e acesso à funcionalidade indisponível anteriormente, talvez nem sempre seja a escolha correta. Sugerimos que você também considere o seguinte ao decidir qual sabor do construtor de relatórios usar.

### Se você estiver criando um relatório simples...

Se o que você deseja criar é simples, usar o Report Builder tradicional pode ser muito mais rápido do que escrever uma consulta SQL completa. Também ajudará se alguma coluna que você precise criar a análise já estiver no Gerenciador de Datas Warehouse.

### Se você compartilhará seu trabalho com outros usuários...

Os usuários em sua organização usarão/visualizarão essa análise? Dependendo de com quem você está compartilhando seu trabalho, aderir ao Visual Report Builder pode ser melhor em alguns casos. Os usuários podem olhar rapidamente a definição no Visual Report Builder versus ler uma consulta SQL potencialmente longa.

Se algumas pessoas precisarem do relatório, mas não estiverem familiarizadas com o SQL, recomendamos usar o sabor original do Report Builder. Isso facilitará as coisas para eles.

## Quebra de linha {#wrapup}

Ambos os `SQL Report Builder` e `Visual Report Builder` são adequadas para uma grande variedade de casos de uso. Isso geralmente depende de quais são suas necessidades analíticas e quem consumirá a análise.
