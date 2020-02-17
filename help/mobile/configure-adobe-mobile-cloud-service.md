---
title: 配置Adobe Mobile Services Cloud服务
seo-title: 配置Adobe Mobile Services Cloud服务
description: 可查看本页以配置Adobe Mobile Services Cloud服务。
seo-description: 可查看本页以配置Adobe Mobile Services Cloud服务。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置Adobe Mobile Services Cloud服务 {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

命 **令中心的Mobile Metrics Tile** （移动量度拼贴）为您的移动应用程序提供实时分析。

Adobe [Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可通过PhoneGap插件提供。 在设备连接之前，会在设备上收集和缓存度量，然后将数据推送到Adobe Mobile Services cloud进行报告和分析。

Adobe Mobile Analytics SDK提供以下功能：

1. **针对移动渠道的数据收集** -在所有主要操作系统上为您的移动网站和应用程序收集全面的数据。
1. **移动互动分析** -了解移动App、网站或视频中的用户互动，包括消费者启动渠道的频率、是否从渠道购买等。
1. **移动应用仪表板和报告** -获取包含应用程序生命周期指标和应用商店指标的使用情况报告— 查看用户趋势、启动次数、平均会话长度、保留时长和崩溃情况。
1. **移动营销活动分析** -量化特定于移动的营销活动（如SMS、移动搜索广告、移动展示广告和二维码）的有效性。
1. **地理位置分析** -根据GPS定位或兴趣点，查找您的App用户启动您的移动体验并与之交互的位置。
1. **路径分析** -查看用户如何在您的应用程序中导航以确定哪些屏幕和UI元素是吸引用户的，哪些屏幕和UI元素会导致用户流失。

>[!CAUTION]
>
>仅 **** 在您配置了云服务后，功能板中才会显示分析指标拼贴。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics拼贴

## 配置云服务 {#configuring-the-cloud-service}

为了利用Adobe Mobile Services Analytics，您需要使用Adobe Analytics帐户信息配置AEM Mobile Analytics云服务。

1. 单击右上角的图标，从应用程序功能板的“管理云服务”拼贴中 **添加或编辑云服务** 。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此时将显示 **添加或编辑云服务** 。 选择 **Adobe Mobile Services** ，然后单 **击下一步**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从 **Mobile Services中选择现有配** 置 **，或选择“** 创建配置”以创建新配置。

   对于新配置，输入 **Mobile services属性，然**&#x200B;后单击&#x200B;**“验证”。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果验证了凭据，则“验 **证** ”按钮将变 **为“验证”**。 您可以从“选择移动应用程序服务” **中选择移动服务应用程序**。

   单击 **提交** ，以设置配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在仪表板中查看相同的配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您可以在应用程序功能板中 **查看分析指标** “拼贴”。

   ![chlimage_1-28](assets/chlimage_1-28.png)

