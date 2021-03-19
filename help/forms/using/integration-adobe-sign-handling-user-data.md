---
title: 与Adobe Sign集成 |处理用户数据
seo-title: 与Adobe Sign集成 |处理用户数据
description: 与Adobe Sign集成 |处理用户数据
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 与Adobe Sign集成 |处理用户数据{#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 集[!DNL  Adobe Sign] 成，以在自适应表单中启用电子签名工作流，以处理法律、销售、工资、人力资源管理工作流的表单或协议。它允许单用户和多用户签名、顺序和同时签名工作流、以匿名或登录用户身份对表单进行签名以及多种用户身份验证方式。

当签名者或多个签名者签名并提交自适应表单时，将生成[!DNL Adobe Sign]协议，其中包含有关签名者的信息。

有关[!DNL AEM Forms]与[!DNL Adobe Sign]集成的详细信息，请参阅[在自适应形式中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

## 用户数据和数据存储{#data}

[!DNL Adobe Sign] 已启用的自适应表单包括关于签名者的信息并且可以包括由自适应表单收集的其他用户数据。[!DNL Adobe Sign]服务在协议中保存具有签名的用户数据。 协议保存在[!DNL AEM Forms]云服务中配置的[!DNL Adobe Sign]服务器上。 此外，如果自适应表单配置为使用Forms Portal提交操作，则协议数据将与表单数据一起保存在表单门户数据存储中。

## 访问和删除用户数据{#access-and-delete-user-data}

用户数据在协议中收集，但不保存在任何服务表中。 [!DNL Adobe Sign] 使管理员能够自行选择管理他们在服务中控制的数据。[!DNL Adobe Sign]服务的隐私管理员可以根据申请人的电子邮件地址列表或删除协议。

[!DNL Adobe Sign] 优惠一个Web应用程序，它允许参与者搜索协议，并根据需要删除协议。有关详细信息，请参阅[Adobe Sign — 功能：删除用户信息](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

配置为使用Forms门户提交操作的自适应表单的协议数据也保存在表单门户数据存储中。 要访问和删除表单门户数据存储中的数据，请参阅[Forms门户 |处理用户数据](/help/forms/using/forms-portal-handling-user-data.md)。
