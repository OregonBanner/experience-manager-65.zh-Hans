---
title: 配置AdobeMobile ServicesCloud Service
seo-title: Configure your Adobe Mobile Services Cloud Service
description: 请按照本页配置您的AdobeMobile ServicesCloud Service。
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
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
source-wordcount: '450'
ht-degree: 0%

---

# 配置AdobeMobile ServicesCloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

的 **移动量度拼贴** 命令中心为您的移动应用程序提供实时分析。

的 [AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK通过PhoneGap插件提供。 量度会收集并缓存在设备上，直到连接设备为止，此时数据会推送到AdobeMobile Services Cloud以进行报告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **为移动渠道收集数据**  — 收集所有主要操作系统上移动设备网站和应用程序的全面数据。
1. **移动参与度分析**  — 了解移动设备应用程序、网站或视频中的用户参与度，包括消费者启动渠道的频率、是否从渠道购买等。
1. **移动设备应用程序功能板和报表**  — 获取使用情况报表，其中包含应用程序的生命周期量度和应用商店量度 — 查看用户趋势、启动次数、平均会话时长、保留时长和崩溃次数。
1. **移动设备促销活动分析**  — 量化特定于移动设备的促销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析**  — 按GPS位置或目标点查找应用程序用户在何处启动并与移动体验进行交互。
1. **路径分析**  — 了解用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素吸引用户以及哪些元素会导致用户流失。

>[!CAUTION]
>
>的 **分析量度** 仅当您配置了云服务时，功能板中才会显示拼贴。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM命令中心量度拼贴

## 配置Cloud Service {#configuring-the-cloud-service}

要利用Mobile Services AnalyticsAdobe，您需要使用AEM Mobile Analytics Cloud帐户信息配置Adobe Analytics Service 。

1. 单击右上方的图标，以在 **管理Cloud Services** 图块。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 的 **添加或编辑Cloud Services** 屏幕。 选择 **AdobeMobile Services** 单击 **下一个**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从 **Mobile Services** 或选择 **创建配置** 来创建新受众。

   对于新配置，请输入 **Mobile Services属性**&#x200B;单击&#x200B;**验证。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果凭据已验证，则 **验证** 按钮更改为 **已验证**. 您可以从 **选择移动设备应用程序服务**.

   单击 **提交** ，以设置配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在功能板中查看相同的配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您可以查看 **分析量度** 在应用程序功能板中拼贴。

   ![chlimage_1-28](assets/chlimage_1-28.png)
