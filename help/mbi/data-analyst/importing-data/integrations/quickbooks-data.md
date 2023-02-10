---
title: Dados de QuickBooks esperados
description: Saiba como rastrear facilmente campos de dados relevantes para análise.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# Esperado [!DNL QuickBooks] dados

![](../../../assets/Quickbooks.png)

Depois [você conectou seu [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), você pode usar o [Gerenciador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise. As tabelas a seguir serão criadas no data warehouse:

Para exibir todos os campos disponíveis para rastreamento, clique nos links na coluna de nome da tabela.

## Entidades de Transação {#transactionentities}

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`bill`](https://developer.intuit.com/docs/api/accounting/Bill) | A tabela de títulos contém informações sobre transações de AP ou uma solicitação de pagamento de terceiros. Os atributos incluem tipo de moeda, taxa de câmbio, valor total, data de vencimento, saldo e muito mais. |
| [`billpayments`](https://developer.intuit.com/docs/api/accounting/BillPayment) | As entidades de Pagamento de Faturamento são a transação final de pagamento de faturas recebidas de um fornecedor. Esta tabela inclui informações sobre o fornecedor, tipo de pagamento, valor total, data da transação e muito mais. |
| [`creditmemos`](https://developer.intuit.com/docs/api/accounting/CreditMemo) | A tabela de avisos de crédito registra as transações que são reembolsos ou créditos de pagamentos totais e parciais. Alguns atributos incluem o nome do cliente, as informações de faturamento e envio do cliente, o valor e a data. |
| [`deposits`](https://developer.intuit.com/docs/api/accounting/Deposit) | Os depósitos incluem os depósitos diretos e os pagamentos de clientes transferidos para a Conta de Ativo depois de serem detidos no `Undeposited Funds` conta. Os atributos incluem a quantidade, a ID do depósito e a data. |
| [`estimates`](https://developer.intuit.com/docs/api/accounting/Estimate) | As estimativas são transações fornecidas a clientes que incluem o preço proposto para um bem ou serviço. Esta tabela registra a quantia, quaisquer informações de desconto, informações do cliente e data. |
| [`invoices`](https://developer.intuit.com/docs/api/accounting/Invoice) | NFFs são formulários de vendas que um cliente paga posteriormente. A tabela de NFFs registra qualquer informação de depósito, data, itens de linha, informações de imposto e informações sobre o cliente. |
| [`journalentries`](https://developer.intuit.com/docs/api/accounting/JournalEntry) | A tabela de lançamentos registra as informações da conta AR e AP, incluindo a ID do lançamento, a data da transação e as informações do item de linha. |
| [`payments`](https://developer.intuit.com/docs/api/accounting/Payment) | Um registro de pagamento inclui atributos como ID de pagamento, quantias aplicadas e não aplicadas, data da transação, tipo de transação e status de processamento. |
| [`purchases`](https://developer.intuit.com/docs/api/accounting/Purchase) | A tabela de compras representa suas despesas e inclui a ID de compra, o tipo de pagamento, a quantia e qualquer informação sobre o item da linha. |
| [`purchaseorders`](https://developer.intuit.com/docs/api/accounting/PurchaseOrder) | As ordens de compra são solicitações de mercadorias enviadas a fornecedores. Esta tabela inclui informações sobre o fornecedor, ID da ordem de compra, data da transação, informações sobre item de linha, valor total e informações sobre a conta AP. |
| [`refundreceipts`](https://developer.intuit.com/docs/api/accounting/RefundReceipt) | Este quadro registra as restituições concedidas aos clientes. Os atributos incluem a ID de recebimento de reembolso, informações de item de linha, valor total, informações sobre o cliente e saldo. |
| [`salesreceipts`](https://developer.intuit.com/docs/api/accounting/SalesReceipt) | A tabela de recebimentos de vendas registra informações nos recebimentos de vendas fornecidos aos clientes, incluindo a ID de recebimento de vendas, informações de item de linha, valor total, informações sobre o cliente, data da transação e quaisquer depósitos. |
| [`timeactivities`](https://developer.intuit.com/docs/api/accounting/TimeActivity) | Atividades de tempo são registros de tempo para fornecedores e/ou funcionários. A tabela de atividades de tempo inclui a ID da atividade de tempo, as informações do funcionário/fornecedor, o registro de tempo, a descrição da atividade e a data registrada. |
| [`transfers`](https://developer.intuit.com/docs/api/accounting/Transfer) | A tabela de transferências registra informações sobre fundos movidos entre contas. Os atributos incluem a ID da transferência, o valor, as informações da conta e a data. |
| [`vendorcredits`](https://developer.intuit.com/docs/api/accounting/VendorCredit) | Créditos de fornecedor são transações de AP que são reembolsos ou créditos dados a fornecedores. O `vendorcredits` inclui a ID de crédito do fornecedor, informações de item de linha, informações do fornecedor, conta AP, valor total e data. |

{style=&quot;table-layout:auto&quot;}

## Nomear entidades da lista {#namelistentities}

| **Nome da tabela** | **Descrição** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/docs/api/accounting/Account) | Esta tabela inclui a ID da conta, o nome, o status, o tipo, o saldo, a moeda e o tempo de criação. |
| [`budgets`](https://developer.intuit.com/docs/api/accounting/Budget) | Essa tabela registra todas as informações relacionadas aos orçamentos da empresa, incluindo a ID do orçamento, o nome, as datas de início e término, o tipo, o status e os detalhes. |
| [`classes`](https://developer.intuit.com/docs/api/accounting/Class) | As classes, aplicadas às linhas de detalhes das transações, permitem rastrear segmentos que não estão vinculados a um cliente ou projeto. Essa tabela registra a ID da classe, o nome, a subclasse e o status. |
| [`customers`](https://developer.intuit.com/docs/api/accounting/Customer) | A tabela de clientes contém todas as informações relacionadas aos clientes, incluindo a ID do cliente, o nome, os endereços de faturamento e envio, o número de telefone e o endereço de email. |
| [`departments`](https://developer.intuit.com/docs/api/accounting/Department) | A tabela de departamentos inclui a ID do departamento, o nome e o tipo (subdepartamento vs departamento de nível superior). |
| [`employees`](https://developer.intuit.com/docs/api/accounting/Employee) | A tabela de funcionários registra as informações sobre as pessoas que trabalham para sua empresa. Os atributos incluem a ID do funcionário, o nome, o endereço, o número de telefone e as informações faturáveis, se a empresa estiver habilitada para a folha de pagamento. |
| [`items`](https://developer.intuit.com/docs/api/accounting/Item) | A tabela de itens contém detalhes sobre produtos ou serviços que sua empresa vende. Esta tabela inclui o item ID, nome, descrição, preço unitário, tipo, informações de compra, quantidade em estoque e informações de conta de receita e ativo. |
| [`paymentmethods`](https://developer.intuit.com/docs/api/accounting/PaymentMethod) | A tabela de métodos de pagamento registra o método de pagamento recebido para bens e serviços. Ele contém a ID do pagamento, o tipo e o nome. |
| [`taxagencies`](https://developer.intuit.com/docs/api/accounting/TaxAgency) | Esta tabela registra informações sobre agências de impostos, incluindo a ID da agência de impostos, e informações de rastreamento sobre impostos para compras e vendas. |
| [`taxcodes`](https://developer.intuit.com/docs/api/accounting/TaxCode) | Os códigos de imposto são usados para rastrear o status de imposto (tributável vs. não tributável) de produtos, serviços e clientes. A tabela de códigos de imposto inclui a ID do código de imposto, o nome, a descrição, o status, o status tributável, a alíquota de imposto e o grupo de impostos. |
| [`taxrates`](https://developer.intuit.com/docs/api/accounting/TaxRate) | As taxas de imposto são usadas para calcular passivos de imposto. Essa tabela inclui a ID da taxa de imposto, o nome, a descrição, a taxa, a agência de impostos e muito mais. |
| [`terms`](https://developer.intuit.com/docs/api/accounting/Term) | Esta entidade representa os termos em que as vendas são efetuadas. A tabela de termos inclui o termo ID, nome, tipo, percentual de desconto e dias de vencimento. |
| [`vendors`](https://developer.intuit.com/docs/api/accounting/Vendor) | A tabela de fornecedores contém informações sobre os fornecedores dos quais você adquiriu. Os atributos da tabela incluem a ID do fornecedor, o nome da empresa, o número da conta, o saldo da conta, o status 1099, o endereço de faturamento, o número de telefone, o endereço de email e o endereço da Web. |

{style=&quot;table-layout:auto&quot;}

## Relacionadas:

* [Conexão [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
