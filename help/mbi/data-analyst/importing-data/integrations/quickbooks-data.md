---
title: Dados esperados do QuickBooks
description: Saiba como rastrear facilmente campos de dados relevantes para análise.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Dados [!DNL QuickBooks] esperados

Depois de [conectar sua [!DNL QuickBooks] conta](../../../data-analyst/importing-data/integrations/quickbooks.md), você poderá usar o [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise. As tabelas a seguir são criadas no Data Warehouse:

Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

## Entidades de Transação {#transactionentities}

| **Nome da Tabela** | **Descrição** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | A tabela `bills` contém informações sobre transações de AP ou uma solicitação de pagamento de terceiros. Os atributos incluem tipo de moeda, taxa de câmbio, valor total, data de vencimento, saldo e muito mais. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` entidades são a transação final de pagamento de contas recebidas de um fornecedor. Essa tabela inclui informações do fornecedor, tipo de pagamento, valor total, data da transação e muito mais. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | A tabela `creditmemos` registra transações que são reembolsos ou créditos de pagamentos completos e parciais. Alguns atributos incluem o nome do cliente, as informações de faturamento e envio do cliente, o valor e a data. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` inclui depósitos diretos e pagamentos de clientes movidos para a Conta de Ativos depois de serem mantidos na conta `Undeposited Funds`. Os atributos incluem o valor, a ID do depósito e a data. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` são transações fornecidas a clientes que incluem preços propostos para um bem ou serviço. Esta tabela registra o valor, as informações de desconto, as informações do cliente e a data. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` são formulários de vendas que um cliente paga mais tarde. A tabela de faturas registra quaisquer informações de depósito, data, itens de linha, informações de imposto e informações do cliente. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | A tabela `journalentries` registra informações de conta de AR e AP, incluindo ID de entrada de diário, data de transação e informações de item de linha. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Um registro `payment` inclui atributos como ID de pagamento, valores aplicados e não aplicados, data da transação, tipo de transação e status de processamento. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | A tabela `purchases` representa suas despesas e inclui a ID de compra, o tipo de pagamento, o valor e qualquer informação de item de linha. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | A tabela `purchaseorders` contém solicitações de mercadorias enviadas para fornecedores. Essa tabela inclui informações do fornecedor, ID da ordem de compra, data da transação, informações de item de linha, valor total e informações da conta AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | A tabela `refundreceipts` registra os reembolsos concedidos aos clientes. Os atributos incluem o ID do recebimento da restituição, informações sobre o item de linha, quantia total, informações sobre o cliente e saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | A tabela `salesreceipts` registra informações nos recibos de venda fornecidos aos clientes, incluindo a ID do recibo de venda, informações de item de linha, valor total, informações do cliente, data da transação e quaisquer depósitos. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | A tabela `timeactivities` contém registros de tempo para fornecedores e/ou funcionários e inclui a ID da atividade de tempo, informações de funcionário/fornecedor, tempo registrado, descrição da atividade e data registrada. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | A tabela `transfers` registra informações sobre fundos movidos entre contas. Os atributos incluem a ID de transferência, o valor, as informações de conta e a data. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Os créditos do fornecedor são transações de AP que são reembolsos ou créditos concedidos aos fornecedores. A tabela `vendorcredits` inclui a ID de crédito do fornecedor, informações de item de linha, informações do fornecedor, conta AP, valor total e data. |

{style="table-layout:auto"}

## Entidades da Lista de Nomes {#namelistentities}

| **Nome da Tabela** | **Descrição** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Essa tabela inclui a ID da conta, o nome, o status, o tipo, o saldo, a moeda e o horário de criação. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Esta tabela registra todas as informações relacionadas aos orçamentos da empresa, incluindo a ID do orçamento, o nome, as datas de início e término, o tipo, o status e os detalhes. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | As classes, aplicadas às linhas detalhadas das transações, permitem rastrear segmentos que não estão vinculados a um cliente ou projeto. Esta tabela registra a ID da classe, o nome, a subclasse e o status. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | A tabela `customers` contém todas as informações relacionadas aos seus clientes, incluindo a ID do cliente, nome, endereços de cobrança e de envio, número de telefone e endereço de email. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | A tabela `departments` inclui a ID, o nome e o tipo do departamento (subdepartamento versus departamento de nível superior). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | A tabela `employees` registra informações sobre as pessoas que trabalham na sua empresa. Os atributos incluem a ID do funcionário, o nome, o endereço, o número de telefone e as informações faturáveis, se a empresa estiver habilitada para folha de pagamento. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | A tabela `items` contém detalhes sobre produtos ou serviços que sua empresa vende. Esta tabela inclui a ID do item, o nome, a descrição, o preço unitário, o tipo, as informações de compra, a quantidade em estoque e as informações de conta de receita e ativo. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | A tabela `paymentmethods` registra o método de pagamento recebido para mercadorias e serviços. Ele contém a ID, o tipo e o nome do pagamento. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Esta tabela registra informações sobre agências de impostos, incluindo a ID da agência de impostos, e informações de rastreamento sobre impostos para compras e vendas. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Os códigos de imposto são usados para rastrear o status do imposto (tributável vs. não tributável) de produtos, serviços e clientes. A tabela `taxcodes` inclui a ID do código de imposto, o nome, a descrição, o status, o status tributável, a alíquota do imposto e o grupo de impostos. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | As alíquotas de imposto são usadas para calcular passivos de imposto. Esta tabela inclui a ID da alíquota do imposto, o nome, a descrição, a alíquota, a agência de impostos e muito mais. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Esta entidade representa as condições sob as quais as vendas são feitas. A tabela de termos inclui a ID do termo, o nome, o tipo, o percentual de desconto e os dias de vencimento. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | A tabela de fornecedores contém informações sobre os fornecedores dos quais você compra. Os atributos da tabela incluem ID do fornecedor, nome da empresa, número da conta, saldo da conta, status 1099, endereço de cobrança, número de telefone, endereço de email e endereço da Web. |

{style="table-layout:auto"}

## Relacionados:

* [Conectando [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
