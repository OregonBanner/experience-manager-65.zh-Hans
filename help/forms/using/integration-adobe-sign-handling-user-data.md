---
title: 与Adobe Sign集成 |处理用户数据
seo-title: 与Adobe Sign集成 |处理用户数据
description: 与Adobe Sign集成 |处理用户数据
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 与Adobe Sign集成 |处理用户数据 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 与集[!DNL  Adobe Sign] 成，以在自适应表单中启用电子签名工作流，以处理法律、销售、工资单、人力资源管理工作流的表单或协议。它允许单次和多用户签名、顺序和同时的签名工作流、以匿名或已登录用户身份对表单进行签名，以及通过多种方法来验证用户。

当签名者或多个签名者签名并提交自适应表单时，将生成一个[!DNL Adobe Sign]协议，其中包含有关签名者的信息。

有关[!DNL AEM Forms]与[!DNL Adobe Sign]集成的更多信息，请参阅[在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 用户数据和数据存储 {#data}

[!DNL Adobe Sign] 启用的自适应表单包括关于签名者的信息，并且可以包括由自适应表单收集的其他用户数据。[!DNL Adobe Sign]服务保存协议中具有签名的用户数据。 协议保存在[!DNL AEM Forms]云服务中配置的[!DNL Adobe Sign]服务器上。 此外，如果自适应表单配置为使用Forms Portal提交操作，则协议数据会与表单数据一起保存在表单门户数据存储中。

## 访问和删除用户数据 {#access-and-delete-user-data}

用户数据在协议中收集，但未保存在任何服务表中。 [!DNL Adobe Sign] 允许管理员在管理其控制的服务数据时，自行做出选择。[!DNL Adobe Sign]服务的隐私管理员可以根据请求者的电子邮件地址列出或删除协议。

[!DNL Adobe Sign] 提供了一个web应用程序，允许参与者搜索协议，并在必要时删除协议。有关更多信息，请参阅[Adobe Sign — 功能：删除用户信息](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

配置为使用Forms Portal提交操作的自适应表单的协议数据也会保存在Forms Portal数据存储中。 要访问和删除表单门户数据存储中的数据，请参阅[Forms门户 |处理用户数据](/help/forms/using/forms-portal-handling-user-data.md)。
