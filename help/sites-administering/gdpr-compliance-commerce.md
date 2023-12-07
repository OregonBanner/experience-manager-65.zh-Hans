---
title: AEM Commerce - GDPR就绪
description: 了解在AEM Commerce中处理GDPR请求的过程以及如何使用它们。
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - GDPR就绪{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但包含的详细信息适用于所有数据保护和隐私法规；例如GDPR和CCPA。

欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。 请参阅 [Adobe隐私中心的GDPR页面](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>请参阅 [AEM GDPR就绪](/help/managing/data-protection-and-privacy.md) 以了解更多详细信息。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

通过Adobe的开箱即用的Commerce集成，AEM成为体验层，使用服务并将数据发送回以Headless模式运行的客户Commerce平台。

对于某些商业平台，Adobe存储个人资料信息( `/home/users`)和AEM中的商务令牌（登录到commerce平台）。 对于这些用例，请阅读 [处理AEM平台的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求 {#handling-gdpr-requests-for-aem-commerce}

对于SalesforceCommerce Cloud集成，AEM Commerce不会存储任何GDPR相关信息。 将请求转发到 [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

对于hybris和HCL WebSphere® Commerce的集成，在AEM中有一些数据。 使用 [AEM平台GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 并思考以下问题：

1. **我的数据存储/使用位置？** 缓存的用户配置文件信息，例如名称、商业用户标识符、令牌、密码和地址数据，如AEM中所示。
1. **我应当与谁共享包含的GDPR数据？** AEM Commerce中GDPR相关数据的任何更新都不会存储（除了上述相关的用户档案信息之外），而是通过代理传回Commerce平台。
1. **如何删除我的用户数据**？ 在AEM中删除用户配置文件并调用商务平台上的用户删除操作。

>[!NOTE]
>
>请查看 [hybris wiki](https://wiki.hybris.com/) 或 [HCL WebSphere® Commerce文档](https://help.hcltechsw.com/commerce/index.html)（如有必要）。
