---
title: 配置AdobeMobile ServicesCloud Service
seo-title: 配置AdobeMobile ServicesCloud Service
description: 可查看本页以配置AdobeMobile ServicesCloud Service。
seo-description: 可查看本页以配置AdobeMobile ServicesCloud Service。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# 配置AdobeMobile ServicesCloud Service{#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

命令中心上的&#x200B;**移动度量拼贴**&#x200B;为您的移动应用程序提供实时分析。

[Adobe移动分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可通过PhoneGap插件提供。 在设备上收集和缓存度量，直到连接设备，此时数据将推送到AdobeMobile Services Cloud进行报告和分析。

Adobe移动分析SDK提供以下内容：

1. **针对移动渠道的收集** -在所有主要操作系统上为您的移动网站和应用程序收集全面的数据。
1. **移动互动分析** -了解移动应用、网站或视频中的用户互动，包括消费者启动渠道的频率、是否从中购买，等等。
1. **移动App仪表板和报告** -获取包含App生命周期指标和App商店指标的使用情况报告——查看用户趋势、启动情况、平均会话长度、保留期长度和崩溃情况。
1. **移动活动分析** -量化移动特定活动（如短信、移动搜索广告、移动展示广告和二维码）的有效性。
1. **地理位置分析** -按GPS定位或兴趣点查找应用程序用户启动您的移动体验并与之交互的位置。
1. **寻路分析** -了解用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素是吸引用户的，哪些是导致用户放弃的。

>[!CAUTION]
>
>**分析度量**&#x200B;磁贴仅在您已配置云服务时才显示在仪表板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM命令中心度量拼贴

## 配置Cloud Service{#configuring-the-cloud-service}

为了利用AdobeMobile Services Analytics，您需要使用您的Adobe Analytics帐户信息配置AEM MobileAnalytics Cloud服务。

1. 单击右上方的图标以添加或编辑应用程序Cloud Services **管理Cloud Services**&#x200B;拼贴中的仪表板。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 将显示&#x200B;**添加或编辑Cloud Services**&#x200B;屏幕。 选择&#x200B;**AdobeMobile Services**&#x200B;并单击&#x200B;**下一步**。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 从&#x200B;**Mobile Services**&#x200B;中选择现有配置，或选择&#x200B;**创建配置**&#x200B;创建新配置。

   对于新配置，输入&#x200B;**Mobile Services属性**&#x200B;并单击&#x200B;**验证。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果验证了凭据，则&#x200B;**Verify**&#x200B;按钮将变为&#x200B;**Verified**。 您可以从&#x200B;**选择移动应用服务**&#x200B;中选择移动服务。

   单击&#x200B;**Submit**&#x200B;以设置配置。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 设置云配置后，您可以在仪表板中视图相同的配置。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >设置云配置后，您可以在应用程序视图中仪表板&#x200B;**分析指标**&#x200B;拼贴。

   ![chlimage_1-28](assets/chlimage_1-28.png)

