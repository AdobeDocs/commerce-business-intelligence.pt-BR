---
title: Dados esperados do QuickBooks
description: Saiba como rastrear facilmente campos de dados relevantes para análise.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Esperado [!DNL QuickBooks] dados

![](../../../assets/Quickbooks.png)

Depois [você conectou o [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), você pode usar o [Gerenciador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise. As tabelas a seguir são criadas na Data Warehouse:

Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

## Entidades de Transação {#transactionentities}

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | A tabela de faturamentos contém informações sobre transações de AP ou uma solicitação de pagamento de terceiros. Os atributos incluem tipo de moeda, taxa de câmbio, valor total, data de vencimento, saldo e muito mais. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | As entidades BillPayment são a transação final de pagamento de títulos recebidos de um fornecedor. Essa tabela inclui informações do fornecedor, tipo de pagamento, valor total, data da transação e muito mais. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | A tabela de créditos registra transações que são restituições ou créditos de pagamentos completos e parciais. Alguns atributos incluem o nome do cliente, as informações de faturamento e envio do cliente, o valor e a data. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | Os depósitos incluem depósitos diretos e pagamentos de clientes transferidos para a conta de ativos após terem sido detidos na conta de `Undeposited Funds` conta. Os atributos incluem o valor, a ID do depósito e a data. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | As estimativas são transações fornecidas aos clientes que incluem preços propostos para um bem ou serviço. Esta tabela registra o valor, as informações de desconto, as informações do cliente e a data. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | As faturas são formulários de vendas que um cliente paga posteriormente. A tabela de faturas registra quaisquer informações de depósito, data, itens de linha, informações de imposto e informações do cliente. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | A tabela de lançamentos registra informações de conta de AR e AP, incluindo ID de lançamento, data da transação e informações de item de linha. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Um registro de pagamento inclui atributos como ID do pagamento, quantias aplicadas e não-aplicadas, data da transação, tipo de transação e status de processamento. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | A tabela de compras representa suas despesas e inclui a ID de compra, o tipo de pagamento, o valor e qualquer informação de item de linha. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | Ordens de compra são solicitações de mercadorias enviadas aos fornecedores. Essa tabela inclui informações do fornecedor, ID da ordem de compra, data da transação, informações de item de linha, valor total e informações da conta AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | Esta tabela registra os reembolsos concedidos aos clientes. Os atributos incluem o ID do recebimento da restituição, informações sobre o item de linha, quantia total, informações sobre o cliente e saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | A tabela de recebimentos de venda registra informações nos recebimentos de venda fornecidos aos clientes, incluindo ID do recebimento de venda, informações de item de linha, valor total, informações do cliente, data da transação e quaisquer depósitos. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | Atividades de tempo são registros de tempo para fornecedores e/ou funcionários. A tabela de atividades de tempo inclui a ID de atividade de tempo, informações de funcionário/fornecedor, tempo registrado, descrição da atividade e data registrada. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | A tabela de transferências registra informações sobre fundos movidos entre contas. Os atributos incluem a ID de transferência, o valor, as informações de conta e a data. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Os créditos do fornecedor são transações de AP que são reembolsos ou créditos concedidos aos fornecedores. A variável `vendorcredits` A tabela inclui a ID de crédito do fornecedor, as informações de item de linha, as informações do fornecedor, a conta AP, o valor total e a data. |

{style="table-layout:auto"}

## Entidades da Lista de Nomes {#namelistentities}

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Essa tabela inclui a ID da conta, o nome, o status, o tipo, o saldo, a moeda e o horário de criação. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Esta tabela registra todas as informações relacionadas aos orçamentos da empresa, incluindo a ID do orçamento, o nome, as datas de início e término, o tipo, o status e os detalhes. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | As classes, aplicadas às linhas detalhadas das transações, permitem rastrear segmentos que não estão vinculados a um cliente ou projeto. Esta tabela registra a ID da classe, o nome, a subclasse e o status. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | A tabela de clientes contém todas as informações relacionadas aos clientes, incluindo a ID, o nome, os endereços de cobrança e de envio, o número de telefone e o endereço de email do cliente. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | A tabela de departamentos inclui a ID, o nome e o tipo do departamento (departamento secundário versus departamento de nível superior). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | A tabela de funcionários registra informações sobre as pessoas que trabalham na sua empresa. Os atributos incluem a ID do funcionário, o nome, o endereço, o número de telefone e as informações faturáveis, se a empresa estiver habilitada para folha de pagamento. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | A tabela de itens contém detalhes sobre produtos ou serviços que sua empresa vende. Esta tabela inclui a ID do item, o nome, a descrição, o preço unitário, o tipo, as informações de compra, a quantidade em estoque e as informações de conta de receita e ativo. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | A tabela métodos de pagamento registra o método de pagamento recebido para mercadorias e serviços. Ele contém a ID, o tipo e o nome do pagamento. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Esta tabela registra informações sobre agências de impostos, incluindo a ID da agência de impostos, e informações de rastreamento sobre impostos para compras e vendas. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Os códigos de imposto são usados para rastrear o status do imposto (tributável vs. não tributável) de produtos, serviços e clientes. A tabela de códigos de imposto inclui ID do código do imposto, nome, descrição, status, status tributável, alíquota do imposto e grupo de impostos. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | As alíquotas de imposto são usadas para calcular passivos de imposto. Esta tabela inclui a ID da alíquota do imposto, o nome, a descrição, a alíquota, a agência de impostos e muito mais. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Esta entidade representa as condições sob as quais as vendas são feitas. A tabela de termos inclui a ID do termo, o nome, o tipo, o percentual de desconto e os dias de vencimento. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | A tabela de fornecedores contém informações sobre os fornecedores dos quais você compra. Os atributos da tabela incluem ID do fornecedor, nome da empresa, número da conta, saldo da conta, status 1099, endereço de cobrança, número de telefone, endereço de email e endereço da Web. |

{style="table-layout:auto"}

## Relacionados:

* [Conectando [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
