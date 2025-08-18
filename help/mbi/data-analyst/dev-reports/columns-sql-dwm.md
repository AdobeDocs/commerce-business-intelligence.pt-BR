---
title: Diferenças entre o SQL e o Data Warehouse Manager
description: Saiba mais sobre as diferenças entre o SQL e o Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Diferenças entre [!DNL SQL] e [!DNL Data Warehouse Manager]

Há duas diferenças principais entre as colunas criadas em [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) e as criadas com o [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Uma é a dependência dos ciclos de atualização e a outra é como as colunas são salvas em sua conta.

## Colunas na [!DNL SQL Report Builder]

As colunas não dependem dos ciclos de atualização, portanto, não é mais necessário aguardar a conclusão de uma para poder iterar na coluna. Se você cometer um erro, basta pressionar algumas teclas para corrigi-lo - não é mais necessário esperar duas atualizações serem concluídas antes que você possa voltar ao trabalho.

>[!IMPORTANT]
>
>As colunas criadas usando o editor [!DNL SQL] não são salvas na Data Warehouse. Você sempre tem acesso à consulta contendo a coluna, mas se quiser usar a coluna em mais de um relatório, será necessário recriá-la na consulta para cada relatório. Isso significa que as colunas criadas usando o editor [!DNL SQL] não podem ser usadas no [!DNL Report Builder] tradicional.

## Colunas no Data Warehouse Manager

As colunas dependem dos ciclos de atualização, portanto, um ciclo completo deve ser concluído antes de serem editadas. Essas colunas são salvas no Gerenciador do Data Warehouse e podem ser usadas no [!DNL Report Builder] ou [!DNL SQL Report Builder] tradicional.
