---
title: Gerencie as configurações da sua conta
description: Saiba como personalizar as configurações da conta para o Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Personalização das configurações da sua conta

>[!NOTE]
>
>Exige [permissões de administrador.](../../administrator/user-management/user-management.md)

Na conta do [!DNL Commerce Intelligence], você pode personalizar as configurações da conta para a Data Warehouse. Para acessá-las, selecione o nome da sua organização no canto superior direito de qualquer tela e escolha **[!UICONTROL Account Settings]** na lista suspensa.

* **[!UICONTROL Client Name:]** Essa configuração aparece no canto superior direito de todos os painéis e em qualquer outro lugar em sua conta. Se você deseja alterar **[!UICONTROL "Vandelay Industries Co., Ltd]** para apenas **[!UICONTROL "Vandelay]**, este é o local para fazer isso.

* **[!UICONTROL Currency:]** Esta é a *moeda padrão* para todos os valores monetários da sua conta. Sempre que um valor decimal ou de moeda for sincronizado em sua Data Warehouse, essa configuração determinará o símbolo colocado antes desse valor em seus relatórios.

* **[!UICONTROL Blackout Hours:]** Essa configuração garante que, durante as horas selecionadas do dia, sua Data Warehouse não acesse os bancos de dados conectados. Todas as horas são expressas em zero hora e no Horário Padrão do Leste (EST). Por exemplo, se você não quiser que o banco de dados de produção seja acessado entre as horas de EST às 9h e EST às 13h, digite a seguinte matriz de dígitos: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Essa configuração garante que uma atualização de Data Warehouse comece automaticamente na sua conta *durante as horas* especificadas. Assim como com as horas de blecaute, elas também estão no ET. Por exemplo, se você quiser que as atualizações do Data Warehouse comecem automaticamente às **meia-noite** e **meio-dia** EST, digite a seguinte matriz de dígitos: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Essa opção gerencia situações em que um resumo de email é agendado para envio *antes da atualização dos dados em um de seus relatórios*. Se você escolher **Não**, sua conta ignorará o envio do email no horário agendado. Em vez disso, sua conta a envia assim que os dados são atualizados. Se você escolher **[!UICONTROL Yes]**, sua conta enviará o email, incluirá uma mensagem explicando que os dados estão obsoletos e enviará outro email assim que os dados forem atualizados.

* **[!UICONTROL Enable data updates:]** Essa opção garante que as atualizações de dados sejam executadas em sua conta. Se você alterar a configuração para **[!UICONTROL No]**, sincronizações de dados e cálculos de coluna serão interrompidos em sua conta.

>[!NOTE]
>
>Selecione **[!UICONTROL Save Customizations]** depois de fazer quaisquer alterações.
