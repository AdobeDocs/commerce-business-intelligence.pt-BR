---
title: Diferenças entre o SQL e o Data Warehouse Manager
description: Saiba mais sobre as diferenças entre o SQL e o Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Diferenças entre o SQL e o Data Warehouse Manager

Há duas diferenças principais entre as colunas criadas na variável [Report Builder SQL](../dev-reports/sql-rpt-bldr.md) e os criados usando o [Gerenciador de Datas Warehouse](../data-warehouse-mgr/creating-calculated-columns.md): uma é a dependência em ciclos de atualização, a outra é como as colunas são salvas em sua conta.

## Colunas na `SQL Report Builder`

As colunas não dependem dos ciclos de atualização, portanto, não é mais necessário aguardar a conclusão de um para iterar na coluna. Se você cometer um erro, são necessários apenas alguns pressionamentos de tecla para corrigi-lo; não é mais necessário aguardar duas atualizações para que você possa voltar ao trabalho.

>[!IMPORTANT]
>
>As colunas criadas usando o editor SQL não são salvas em sua Data Warehouse. Você sempre tem acesso à consulta que contém a coluna , mas se quiser usar a coluna em mais de um relatório, é necessário recriá-la na consulta para cada relatório. Isso significa que as colunas criadas usando o editor SQL não podem ser usadas no `Report Builder`.

## Colunas no Gerenciador de Data Warehouse

As colunas dependem dos ciclos de atualização, portanto, um ciclo completo deve ser concluído antes de serem editadas. Essas colunas são salvas no Gerenciador de Datas Warehouse e podem ser usadas no `Report Builder` ou `SQL Report Builder`.
