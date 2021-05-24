---
title: AEM Commerce - GDPR就绪
seo-title: AEM Commerce - GDPR就绪
description: “AEM商务 — GDPR就绪”
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# AEM Commerce - GDPR就绪{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR用作以下部分的示例，但相关详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等

欧盟的《数据隐私权通用数据保护条例》已于2018年5月正式生效。 有关更多信息，请参阅Adobe隐私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[GDPR页面。

>[!NOTE]
>
>有关更多详细信息，请参阅[AEM GDPR就绪](/help/managing/data-protection-and-privacy.md)。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在我们开箱即用的商务集成中， AEM是体验层，用于使用服务并将数据发送回以无头模式运行的客户商务平台。

对于某些商务平台，我们在AEM中存储了配置文件信息(`/home/users`)和商务令牌（用于在商务平台中登录）。 对于这些用例，请阅读[处理AEM Platform的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求{#handling-gdpr-requests-for-aem-commerce}

对于SalesforcesCommerce Cloud集成，AEM Commerce不会存储任何与GDPR相关的信息。 您应该将请求转发到[Salesforce Cloud](https://documentation.demandware.com/)。

对于hybris和IBM WebSphere集成，AEM中有一些数据。 您应使用[AEM Platform GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)并考虑以下问题：

1. **我的数据存储/使用在何处？** 从AEM中显示缓存的用户配置文件信息，如名称、商务用户标识符、令牌、密码、地址数据等。
1. **我该与谁共享涵盖的GDPR数据？** AEM Commerce中任何与GDPR相关数据的更新均不会存储（相关用户档案信息除外，如上所述），而是会被代理回商务平台。
1. **如何删除我的用户数据**?在AEM中删除用户配置文件，并在商务平台上调用用户删除。

>[!NOTE]
>
>如果需要，请查看[hybris wiki](https://wiki.hybris.com/)或[Websphere商务文档](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)。
