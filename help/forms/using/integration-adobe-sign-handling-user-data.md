---
title: 与Adobe Sign集成 |处理用户数据
seo-title: Integration with Adobe Sign | Handling user data
description: 与Adobe Sign集成 |处理用户数据
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 与Adobe Sign集成 |处理用户数据 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 集成[!DNL  Adobe Sign] 启用自适应表单中的电子签名工作流，以处理法律、销售、工资单、人力资源管理工作流的表单或协议。 它允许单用户和多用户签名、顺序和同步签名工作流、以匿名或登录用户身份签名表单，以及多种验证用户的方法。

当签名者或多个签名者签名并提交自适应表单时， [!DNL Adobe Sign] 生成包含有关签名者信息的协议。

有关详情，请参阅 [!DNL AEM Forms] 与集成 [!DNL Adobe Sign]，请参见 [在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md).

## 用户数据和数据存储 {#data}

[!DNL Adobe Sign] 启用的自适应表单包含有关签名者的信息，并且可以包含由该自适应表单收集的其他用户数据。 此 [!DNL Adobe Sign] 服务使用协议中的签名保存用户数据。 协议保存于 [!DNL Adobe Sign] 服务器配置于 [!DNL AEM Forms] 云服务。 此外，如果自适应表单配置为使用Forms Portal提交操作，则协议数据与表单数据一起保存在表单门户数据存储中。

## 访问和删除用户数据 {#access-and-delete-user-data}

用户数据在协议中收集，但未保存在任何服务表中。 [!DNL Adobe Sign] 使管理员能够自行选择管理他们在服务中控制的数据。 隐私管理员 [!DNL Adobe Sign] 服务可以根据请求者的电子邮件地址列出或删除协议。

[!DNL Adobe Sign] 提供一个Web应用程序，允许按参与者搜索协议，并在需要时删除协议。 有关更多信息，请参阅 [Adobe Sign — 功能：删除用户信息](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

配置为使用Forms Portal提交操作的自适应表单的协议数据也保存在表单门户数据存储中。 要访问和删除表单门户数据存储中的数据，请参阅 [Forms门户 |处理用户数据](/help/forms/using/forms-portal-handling-user-data.md).
