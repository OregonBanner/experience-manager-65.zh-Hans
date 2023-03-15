---
title: AEM Commerce - GDPR准备工作
seo-title: AEM Commerce - GDPR Readiness
description: “AEM Commerce - GDPR准备工作”
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# AEM Commerce - GDPR准备工作{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但所涵盖的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等。

欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。 欲知更多信息，请参见 [Adobe隐私中心的GDPR页面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>参见 [AEM GDPR就绪](/help/managing/data-protection-and-privacy.md) 了解更多详细信息。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在我们开箱即用的Commerce集成中，AEM是体验层，使用服务并将数据发送回以Headless模式运行的客户商务平台。

对于某些商业平台，我们存储个人资料信息( `/home/users`)和Commerce令牌（用于登录到Commerce平台）的AEM。 对于这些用例，请阅读 [处理AEM平台的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求 {#handling-gdpr-requests-for-aem-commerce}

对于SalesforcesCommerce Cloud集成，AEM Commerce不会存储任何GDPR相关信息。 您应将请求转发至 [Salesforce Cloud](https://documentation.demandware.com/).

对于hybris和IBM WebSphere的集成，AEM中提供了一些数据。 您应使用 [AEM平台GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 并思考以下问题：

1. **我的数据存储/使用位置** 缓存的用户配置文件信息（如名称、商业用户标识符、令牌、密码、地址数据等）将显示自AEM。
1. **我应将覆盖的GDPR数据共享给谁？** AEM Commerce中GDPR相关数据的任何更新不会存储（上面提到的相关配置文件信息除外），而是通过代理传回Commerce平台。
1. **如何删除我的用户数据**？ 删除AEM中的用户配置文件并调用商业平台上的用户删除操作。

>[!NOTE]
>
>请查看 [hybris wiki](https://wiki.hybris.com/) 或 [Websphere Commerce文档](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) 如果需要。
