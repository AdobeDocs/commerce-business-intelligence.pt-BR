---
title: Integração ao Adobe Commerce Intelligence
description: Saiba mais sobre a integração do Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Integração [!DNL Adobe Commerce Intelligence]

As perguntas de integração relacionadas ao `store` e `database` as configurações garantem que seus relatórios sejam configurados corretamente. Com essas respostas, o Adobe fornece relatórios que são adaptados precisamente para a configuração de sua loja.

## Configurações da loja

- *Sua loja aceita o check-out de convidado?* - Selecionar **sim** se você permitir que os clientes façam uma compra em sua loja sem se registrarem em uma conta.

- `Timezone` - Selecione o `timezone` que você gostaria de ver nos seus relatórios.

- `Currency` - Selecione o `currency` em que sua loja opera.

- `Your week starts on...` - Selecione o dia da semana que você gostaria que fosse o início da semana em seus relatórios.

- *Qual versão do Commerce você usa?* - Selecione o `currency` em que sua loja opera.

- *Sua loja está localizada na União Europeia?* - Se você responder `Yes` Para responder a essa pergunta, o Adobe hospeda sua Data Warehouse e todos os seus dados na União Europeia, em conformidade com o GDPR.

## Configurações do banco de dados

- `Database name` - O que é o *nome do [!DNL MySQL] banco de dados* onde estão os dados transacionais do Commerce?

- `Table prefix (optional)` - As tabelas contidas no banco de dados do Commerce são precedidas de qualquer item (por exemplo, `store_`)? Normalmente, não é o caso, mas é uma personalização que pode ser feita.
