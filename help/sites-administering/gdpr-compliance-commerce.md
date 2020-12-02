---
title: AEM商务- GDPR就绪性
seo-title: AEM商务- GDPR就绪性
description: 'null'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# AEM Commerce - GDPR Readiness{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下各节中用作示例，但涵盖的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等。

欧洲合并的《数据隐私权一般数据保护规定》自2018年5月起生效。 有关详细信息，请参阅Adobe隐私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[GDPR页面。

>[!NOTE]
>
>有关更多详细信息，请参阅[AEM GDPR Readiness](/help/managing/data-protection-and-privacy.md)。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在我们现成的商务集成中，AEM是体验层，它消费服务，将数据发送回以无外设模式运行的客户商务平台。

对于某些商务平台，我们将用户档案信息(`/home/users`)和商务令牌（登录到商务平台）存储在AEM中。 对于这些用例，请阅读[处理AEM Platform的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求{#handling-gdpr-requests-for-aem-commerce}

对于SalesforcesCommerce Cloud集成，AEM Commerce不存储任何GDPR相关信息。 您应将请求转发到[Salesforce云](https://documentation.demandware.com/)。

对于hybris和IBM WebSphere集成，AEM中有一些数据。 您应使用[AEM Platform GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)并考虑以下问题：

1. **我的数据存储／使用位置？** 缓存的用户用户档案信息（如名称、商务用户标识符、令牌、密码、地址数据等）从AEM中显示。
1. **我应与谁共享涵盖的GDPR数据？** AEM Commerce中对GDPR相关数据的任何更新均不会存储(相关用户档案信息除外，如上所述)，而是被代理回商务平台。
1. **如何删除我的用户数据**?删除AEM中的用户用户档案，并调用商务平台上的用户删除。

>[!NOTE]
>
>如果需要，请查看[hybris wiki](https://wiki.hybris.com/)或[Websphere Commerce documentation](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)。

