---
title: Integração ao Adobe Commerce Intelligence
description: Saiba mais sobre a integração do Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Integração de [!DNL Adobe Commerce Intelligence]

As perguntas de integração relacionadas às configurações do `store` e do `database` garantem que você configure seus relatórios corretamente. Com essas respostas, a Adobe fornece relatórios que são adaptados precisamente à configuração de sua loja.

## Configurações da loja

- *Sua loja aceita o check-out de convidado?* - Selecione **sim** se você permitir que os clientes façam uma compra em sua loja sem se registrarem em uma conta.

- `Timezone` - Selecione o `timezone` no qual você deseja ver seus relatórios.

- `Currency` - Selecione o `currency` em que seu armazenamento opera.

- `Your week starts on...` - Selecione o dia da semana que você gostaria que fosse o início da semana em seus relatórios.

- *Qual versão do Commerce você usa?* - Selecione o `currency` em que seu armazenamento opera.

- *Sua loja está baseada na União Europeia?* - Se você responder `Yes` a esta pergunta, a Adobe hospedará sua Data Warehouse e todos os seus dados na União Europeia, em conformidade com o GDPR.

## Configurações do banco de dados

- `Database name` - Qual é o *nome do [!DNL MySQL] banco de dados* onde estão seus dados transacionais do Commerce?

- `Table prefix (optional)` - As tabelas contidas no seu banco de dados do Commerce são precedidas de qualquer item (por exemplo, `store_`)? Normalmente, não é o caso, mas é uma personalização que pode ser feita.
