---
title: 配置AdobeMobile ServicesCloud Service
seo-title: 配置AdobeMobile ServicesCloud Service
description: 请按照本页配置您的AdobeMobile ServicesCloud Service。
seo-description: 请按照本页配置您的AdobeMobile ServicesCloud Service。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 配置AdobeMobile ServicesCloud Service{#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

命令中心的&#x200B;**移动量度拼贴**&#x200B;为移动应用程序提供实时分析。

[AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可通过PhoneGap插件使用。 量度会收集并缓存在设备上，直到连接设备为止，此时数据会推送到AdobeMobile Services Cloud以进行报告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **为移动渠道收集数据**  — 在所有主要操作系统上为您的移动设备网站和应用程序收集全面的数据。
1. **移动设备参与度分析**  — 了解移动设备应用程序、网站或视频中的用户参与度，包括消费者启动渠道的频率、是否从渠道进行购买等。
1. **移动设备应用程序功能板和报表**  — 获取使用情况报表，其中包含应用程序的生命周期量度和应用商店量度 — 查看用户趋势、启动次数、平均会话时长、保留时长和崩溃次数。
1. **移动设备促销活动分析**  — 量化特定于移动设备的促销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析**  — 通过GPS位置或目标点，查找应用程序用户在何处启动并与您的移动体验进行交互。
1. **路径分析**  — 查看用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素吸引用户，哪些元素会导致用户流失。

>[!CAUTION]
>
>仅当您配置了云服务时，功能板中才会显示&#x200B;**分析量度**&#x200B;拼贴。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM命令中心量度拼贴

## 配置Cloud Service{#configuring-the-cloud-service}

要利用Mobile Services AnalyticsAdobe，您需要使用AEM Mobile Analytics Cloud帐户信息配置Adobe Analytics Service 。

1. 单击右上方的图标，从应用程序功能板的&#x200B;**管理Cloud Services**&#x200B;拼贴中添加或编辑Cloud Services。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此时会显示&#x200B;**添加或编辑Cloud Services**&#x200B;屏幕。 选择&#x200B;**AdobeMobile Services**&#x200B;并单击&#x200B;**下一步**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从&#x200B;**Mobile Services**&#x200B;中选择现有配置，或选择&#x200B;**创建配置**&#x200B;以创建新配置。

   对于新配置，请输入&#x200B;**Mobile Services属性**&#x200B;并单击&#x200B;**验证。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果凭据已验证，则&#x200B;**Verify**&#x200B;按钮将变为&#x200B;**Verified**。 您可以从&#x200B;**选择移动设备应用程序服务**&#x200B;中选择移动设备服务应用程序。

   单击&#x200B;**Submit**&#x200B;以设置配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在功能板中查看相同的配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您便可以在应用程序功能板中查看&#x200B;**分析量度**&#x200B;拼贴。

   ![chlimage_1-28](assets/chlimage_1-28.png)
