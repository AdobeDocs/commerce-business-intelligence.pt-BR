---
title: Diferenças entre o SQL e o Data Warehouse Manager
description: Saiba mais sobre as diferenças entre o SQL e o Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Diferenças entre o SQL e o Data Warehouse Manager

Há duas diferenças principais entre as colunas criadas no [REPORT BUILDER SQL](../dev-reports/sql-rpt-bldr.md) e as criadas com o uso do [Gerenciador de Data Warehouse](../data-warehouse-mgr/creating-calculated-columns.md). Uma é a dependência dos ciclos de atualização e a outra é como as colunas são salvas em sua conta.

## Colunas na `SQL Report Builder`

As colunas não dependem dos ciclos de atualização, portanto, não é mais necessário aguardar a conclusão de uma para poder iterar na coluna. Se você cometer um erro, basta pressionar algumas teclas para corrigi-lo - não é mais necessário esperar duas atualizações serem concluídas antes que você possa voltar ao trabalho.

>[!IMPORTANT]
>
>As colunas criadas usando o editor SQL não são salvas na Data Warehouse. Você sempre tem acesso à consulta contendo a coluna, mas se quiser usar a coluna em mais de um relatório, será necessário recriá-la na consulta para cada relatório. Isso significa que as colunas criadas usando o editor SQL não podem ser usadas no `Report Builder`.

## Colunas no Gerenciador de Datas Warehouse

As colunas dependem dos ciclos de atualização, portanto, um ciclo completo deve ser concluído antes de serem editadas. Essas colunas são salvas no Gerenciador de Datas Warehouse e podem ser usadas na `Report Builder` ou `SQL Report Builder`.
