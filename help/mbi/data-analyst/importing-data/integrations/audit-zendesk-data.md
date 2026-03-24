---
title: Auditoria de dados do Zendesk
description: Saiba mais sobre as etapas para exportar seus dados do Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# Auditoria de dados do Zendesk

Encontrou algo estranho em seus [[!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)? Para apontar o problema, você precisa explorar seus dados. Isso pode ser feito exportando os dados do [!DNL Zendesk] para um arquivo baixável.

## Ativação da exportação de dados

A exportação de dados não está habilitada para todas as contas do [!DNL Zendesk]. Para ativar esse recurso, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR), mencionando o nome de subdomínio [!DNL Zendesk].

>[!NOTE]
>
>Apenas os planos `Enterprise` e `Plus` têm acesso a este recurso no momento.

Após habilitar a exportação de dados, somente administradores em um domínio de email específico poderão exportar dados da sua conta do [!DNL Zendesk]. Normalmente, esse domínio de email é o mesmo domínio de email que o seu [!DNL Zendesk]. O domínio de email do proprietário da conta é usado como padrão, mas você pode alterar o domínio, se necessário.

## Exportar para um arquivo baixável

1. Clique no ícone Admin (logotipo da engrenagem) na barra lateral e escolha **[!UICONTROL Manage** > **Reports]**.
1. Clique na guia **[!UICONTROL Export]**.
1. Clique em **[!UICONTROL Request file]** ao lado de Exportação de XML Completo, como visto na imagem abaixo.

   Nesse ponto, uma criação é iniciada; você é notificado por email quando ela é concluída.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Clique no link em sua notificação por email para baixar um arquivo zip que contém o relatório.

   Esse link de download é válido por pelo menos três dias.

Esse processo cria um arquivo XML contendo todas as informações armazenadas na conta atual do [!DNL Zendesk], incluindo dados de tíquete (com comentários), dados de usuário e dados de conta. Neste ponto, você pode [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) (certifique-se de anexar este arquivo!) para examinar seus dados mais detalhadamente. Se o arquivo for muito grande, compartilhe-o com a equipe [!DNL Commerce Intelligence] via [!DNL Dropbox] ou [!DNL Google Drive].

Para obter mais informações sobre [!DNL Zendesk] exportações de arquivos, consulte a [[!DNL Zendesk] documentação de exportação](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file) oficial.
