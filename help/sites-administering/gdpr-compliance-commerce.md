---
title: AEM Commerce - GDPR准备工作
seo-title: AEM Commerce - GDPR Readiness
description: “AEM Commerce - GDPR准备工作”
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# AEM Commerce - GDPR准备工作{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但所涵盖的详细信息适用于所有数据保护和隐私法规，例如GDPR和CCPA。

欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。 请参阅 [Adobe隐私中心的GDPR页面](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>参见 [AEM GDPR就绪](/help/managing/data-protection-and-privacy.md) 了解更多详细信息。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

通过Adobe现成的Commerce集成，AEM成为体验层，使用服务并将数据发送回以Headless模式运行的客户Commerce平台。

对于某些商业平台，Adobe存储用户档案信息( `/home/users`)和商务令牌（登录到Commerce平台）的AEM。 对于这些用例，请阅读 [处理AEM平台的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求 {#handling-gdpr-requests-for-aem-commerce}

对于SalesforceCommerce Cloud集成，AEM Commerce不会存储任何GDPR相关信息。 将请求转发到 [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

对于hybris和HCL WebSphere® Commerce的集成，在AEM中有一些数据。 使用 [AEM平台GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 并思考以下问题：

1. **我的数据存储/使用位置** 缓存的用户配置文件信息，例如名称、商业用户标识符、令牌、密码和地址数据，如AEM中所示。
1. **我应将覆盖的GDPR数据共享给谁？** AEM Commerce中GDPR相关数据的任何更新都不会存储（上述相关配置文件信息除外），而是代理回Commerce平台。
1. **如何删除我的用户数据**？ 删除AEM中的用户配置文件并调用商业平台上的用户删除操作。

>[!NOTE]
>
>请查看 [hybris wiki](https://wiki.hybris.com/) 或 [HCL WebSphere® Commerce文档](https://help.hcltechsw.com/commerce/index.html)（如有必要）。
