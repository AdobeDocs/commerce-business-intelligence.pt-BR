---
title: Auditoria de dados do Zendesk
description: Saiba mais sobre as etapas para exportar seus dados do Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Auditoria de dados do Zendesk

Encontrou algo estranho em seus [[!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)? Para apontar o problema, você precisa explorar seus dados. Isso pode ser feito exportando os dados do [!DNL Zendesk] para um arquivo baixável.

## Ativação da exportação de dados

A exportação de dados não está habilitada para todas as contas do [!DNL Zendesk]. Para ativar esse recurso, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html), mencionando o nome de subdomínio [!DNL Zendesk].

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

Esse processo cria um arquivo XML contendo todas as informações armazenadas na conta atual do [!DNL Zendesk], incluindo dados de tíquete (com comentários), dados de usuário e dados de conta. Neste ponto, você pode [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (certifique-se de anexar este arquivo!) para examinar seus dados mais detalhadamente. Se o arquivo for muito grande, compartilhe-o com a equipe [!DNL Commerce Intelligence] via [!DNL Dropbox] ou [!DNL Google Drive].

Para obter mais informações sobre [!DNL Zendesk] exportações de arquivos, consulte a [[!DNL Zendesk] documentação de exportação](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file) oficial.
