---
title: 配置AdobeMobile ServicesCloud Service
description: 请按照本页上的说明配置您的AdobeMobile ServicesCloud Service。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 配置AdobeMobile ServicesCloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

此 **移动量度图块** 位于命令中心上，为您的移动应用程序提供实时分析。

此 [Adobe移动分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可通过PhoneGap插件使用。 收集量度并将其缓存在设备上，直到设备连接为止，届时，会将数据推送到AdobeMobile Services云以供生成报表和分析。

AdobeMobile Analytics SDK提供了以下功能：

1. **为移动渠道收集数据**  — 收集您在所有主要操作系统上的移动网站和应用程序的全面数据。
1. **移动参与分析**  — 了解用户在移动应用程序、网站或视频中的参与情况，包括消费者启动渠道的频率、他们是否从中购买等。
1. **移动应用程序功能板和报表**  — 获取包含应用程序和应用商店量度的生命周期量度的使用情况报表 — 请参阅用户、启动次数、平均会话时长、保留时长和崩溃次数趋势。
1. **移动营销活动分析**  — 量化特定于移动设备的促销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析**  — 通过GPS位置或目标点，查找应用程序用户启动的位置并与移动体验交互。
1. **路径分析**  — 了解用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素吸引用户以及导致用户流失。

>[!CAUTION]
>
>此 **分析量度** 仅当您配置了云服务时，图块才会显示在仪表板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics图块

## 配置Cloud Service {#configuring-the-cloud-service}

要利用AdobeMobile Services Analytics，您需要使用Adobe Analytics帐户信息配置AEM Mobile Analytics Cloud服务。

1. 单击右上角的图标以添加或编辑中的Cloud Service **管理Cloud Service** 从应用程序仪表板中拼贴。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此 **添加或编辑Cloud Service** 屏幕显示。 选择 **Adobe移动服务** 并单击 **下一个**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从中选择现有配置 **移动服务** 或选择 **创建配置** 创建一个。

   对于新配置，输入 **Mobile Services属性**&#x200B;并单击&#x200B;**验证。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果认证得到验证， **验证** 按钮更改为 **已验证**. 您可以从中选择移动服务应用程序 **选择移动应用程序服务**.

   单击 **提交** 用于设置您的配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在功能板中查看该配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您可以查看 **分析量度** 在应用程序仪表板中平铺。

   ![chlimage_1-28](assets/chlimage_1-28.png)
