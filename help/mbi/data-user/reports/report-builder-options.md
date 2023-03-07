---
title: Escolha um Report Builder
description: Saiba como escolher o Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Escolha um Report Builder

>[!NOTE]
>>Exige [Permissões de administrador](../../administrator/user-management/user-management.md).


Agora que você tem mais opções para criar análises, às vezes pode ser difícil saber exatamente qual sabor do Report Builder atende às suas necessidades. Este artigo orienta você na escolha da melhor maneira de criar sua análise.

## Quando devo usar o `SQL Report Builder`? {#whensql}

Observe algumas das razões mais comuns pelas quais você usaria o Report Builder SQL em vez do Report Builder tradicional.

### Se você quiser usar funções específicas de SQL...

Parte da beleza do `SQL Report Builder` é a capacidade de usar funções que não estão disponíveis no momento no Gerenciador de Datas Warehouse. No passado, um analista pode ter tido que intervir para ajudá-lo a realizar plenamente sua visão.

O Report Builder SQL suporta funções como [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) e [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que não poderia ser usado anteriormente. Você pode acessar o [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), mas algumas outras funções específicas de SQL incluem:

* [`Bitwise aggregate` funções](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operador](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Se quiser fazer alguns testes...

Se você quiser tentar técnicas e estratégias diferentes para descobrir o que funciona melhor para sua análise, use o `SQL Report Builder`. A criação de colunas no Gerenciador de Datas Warehouse leva tempo e as colunas que você cria usando o DWM dependem dos ciclos de atualização.

Na melhor das hipóteses, você deve aguardar um ciclo de atualização antes de poder usar sua coluna. Se você perceber que cometeu um erro ao criar a coluna, é necessário aguardar *dois* ciclos: um para preencher inicialmente a coluna e outro ciclo para as revisões se propagarem.

### Se você usar uma nova coluna apenas uma vez...

Conforme mencionado na seção acima, a criação de uma coluna no Gerenciador de Datas Warehouse leva tempo. Se você pretende usar apenas uma coluna criada em um relatório, o Adobe sugere usar a variável `SQL Report Builder`. Isso elimina a necessidade de aguardar a conclusão de um ciclo de atualização, fazendo com que você volte ao trabalho mais rapidamente.

### Se estiver trabalhando com dados que tenham uma relação um para muitos...

Às vezes, a estrutura dos dados pode tornar `SQL Report Builder` uma opção mais eficiente e lógica para criar sua análise. Criar colunas para relações um para um é simples no Gerenciador de Datas Warehouse, mas as coisas podem ficar um pouco confusas quando você lida com relações um para muitos.

Digamos que um único produto seja considerado parte de várias categorias de produtos, e você gostaria de visualizar a receita associada a cada categoria de cada produto. Tentar criar essa relação usando o DWM pode ser tedioso e difícil, mas escrever uma consulta SQL pode ser um pouco mais simples:

![](../../assets/When_should_I_use_the_RB_2.png)

## Quando devo usar o Report Builder tradicional? {#whentraditionalrb}

Embora a `SQL Report Builder` O oferece mais controle e acesso à funcionalidade indisponível anteriormente, mas nem sempre pode ser a escolha correta. Adobe sugere que você também considere o seguinte ao decidir qual sabor do Report Builder usar.

### Se você estiver criando um relatório simples...

Se o que você deseja criar for simples, usar o Report Builder tradicional pode ser muito mais rápido do que escrever um query SQL completo. Ajuda se alguma coluna necessária para criar a análise já estiver no Gerenciador de Datas Warehouse.

### Se você estiver compartilhando seu trabalho com outros usuários...

Os usuários em toda a organização estão usando/visualizando essa análise? Dependendo de com quem você está compartilhando seu trabalho, às vezes é melhor usar o Report Builder visual. Os usuários podem ver rapidamente a definição no Report Builder visual em vez de ler uma consulta SQL potencialmente longa.

Se há algumas pessoas que precisam do relatório, mas não estão familiarizadas com o SQL, o Adobe sugere usar o sabor original do Report Builder. Isso facilita as coisas para eles.

## Encapsulamento {#wrapup}

Ambos os `SQL Report Builder` e `Visual Report Builder` são adequados para uma grande variedade de casos de uso. Isso normalmente depende de quais são suas necessidades analíticas e quem está consumindo a análise.
