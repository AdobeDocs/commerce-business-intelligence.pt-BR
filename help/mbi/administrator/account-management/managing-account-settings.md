---
title: Gerencie as configurações da sua conta
description: Saiba como personalizar as configurações da sua conta do Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b6935462-7263-4ced-a703-60de6a5aeb2did: bd989d82-1e15-4534-88db-f1f51dd77ffa
subfeature_v2: id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4e01225a6bd285afbe988b9c24e07e2ea34649fc
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Personalização das configurações da sua conta

>[!NOTE]
>
>Exige [permissões de administrador.](../../administrator/user-management/user-management.md)

Na conta do [!DNL Commerce Intelligence], você pode personalizar as configurações da conta para o Data Warehouse. Para acessá-las, selecione o nome da sua organização no canto superior direito de qualquer tela e escolha **[!UICONTROL Account Settings]** na lista suspensa.

* **[!UICONTROL Client Name:]** Essa configuração aparece no canto superior direito de todos os painéis e em qualquer outro lugar em sua conta. Se você deseja alterar **[!UICONTROL "Vandelay Industries Co., Ltd]** para apenas **[!UICONTROL "Vandelay]**, este é o local para fazer isso.

* **[!UICONTROL Currency:]** Esta é a *moeda padrão* para todos os valores monetários da sua conta. Sempre que um valor decimal ou de moeda for sincronizado no Data Warehouse, essa configuração determinará o símbolo colocado antes desse valor em seus relatórios.

* **[!UICONTROL Blackout Hours:]** Essa configuração garante que, durante as horas selecionadas do dia, a Data Warehouse não acesse os bancos de dados conectados. Todas as horas são expressas em zero hora e no Horário Padrão do Leste (EST). Por exemplo, se você não quiser que o banco de dados de produção seja acessado entre as horas de EST de 9:00 e EST de 1:00 horas, digite a seguinte matriz de dígitos: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Essa configuração garante que uma atualização do Data Warehouse comece automaticamente na sua conta *durante as horas* especificadas. Assim como com as horas de blecaute, elas também estão no ET. Por exemplo, se você quiser que as atualizações do Data Warehouse comecem automaticamente às **meia-noite** e **meio-dia** EST, digite a seguinte matriz de dígitos: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Essa opção gerencia situações em que um resumo de email é agendado para envio *antes da atualização dos dados em um de seus relatórios*. Se você escolher **Não**, sua conta ignorará o envio do email no horário agendado. Em vez disso, sua conta a envia assim que os dados são atualizados. Se você escolher **[!UICONTROL Yes]**, sua conta enviará o email, incluirá uma mensagem explicando que os dados estão obsoletos e enviará outro email assim que os dados forem atualizados.

* **[!UICONTROL Enable data updates:]** Essa opção garante que as atualizações de dados sejam executadas em sua conta. Se você alterar a configuração para **[!UICONTROL No]**, sincronizações de dados e cálculos de coluna serão interrompidos em sua conta.

>[!NOTE]
>
>Selecione **[!UICONTROL Save Customizations]** depois de fazer quaisquer alterações.
