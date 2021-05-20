---
title: 使用Adobe移动分析跟踪应用程序性能
seo-title: 使用Adobe移动分析跟踪应用程序性能
description: 通过AdobeMobile Services，您可以通过跟踪移动设备应用程序的使用情况、应用程序崩溃情况、设备详细信息以及许多其他关键量度，来洞察用户如何使用您的移动设备应用程序。 请阅读本页以了解更多信息。
seo-description: 通过AdobeMobile Services，您可以通过跟踪移动设备应用程序的使用情况、应用程序崩溃情况、设备详细信息以及许多其他关键量度，来洞察用户如何使用您的移动设备应用程序。 请阅读本页以了解更多信息。
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---


# 使用AdobeMobile Analytics{#track-app-performance-with-adobe-mobile-analytics}跟踪应用程序性能

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

您希望提高客户转化率和忠诚度。

您希望为客户提供相关且引人入胜的体验。

您的AEM Mobile应用程序对您的营销活动有何作用？

如何优化移动应用程序以为用户提供最佳体验？

通过AdobeMobile Services，您可以通过跟踪移动设备应用程序的使用情况、应用程序崩溃情况、设备详细信息以及许多其他关键量度，来洞察用户如何使用您的移动设备应用程序。

Adobe Experience Manager Mobile可直接从AEM Mobile应用程序功能板中了解移动分析的详细信息。 功能板中的&#x200B;**移动量度拼贴**&#x200B;为移动应用程序提供了实时分析，使开发人员、作者和管理员能够快速了解移动应用程序的运行状况。 在封面下方，为Analytics提供支持的是[AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK。 AdobeMobile Analytics SDK可以本地或通过PhoneGap桥插件插入您的应用程序中进行Web查看。 量度会收集并缓存在设备上，直到连接设备为止，在该设备上，数据会被推送到AdobeMobile Services Cloud以便进行报告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **为移动渠道收集数据**  — 在所有主要操作系统上为您的移动设备网站和应用程序收集全面的数据。
1. **移动设备参与度分析**  — 了解移动设备应用程序、网站或视频中的用户参与度，包括消费者启动渠道的频率、是否从渠道进行购买等。
1. **移动设备应用程序功能板和报表**  — 获取使用情况报表，其中包含应用程序的生命周期量度和应用商店量度 — 查看用户趋势、启动次数、平均会话时长、保留时长和崩溃次数。
1. **移动设备促销活动分析**  — 量化特定于移动设备的促销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析**  — 通过GPS位置或目标点，查找应用程序用户在何处启动并与您的移动体验进行交互。
1. **路径分析**  — 查看用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素吸引用户，哪些元素会导致用户流失。

此部分介绍[AEM开发人员](#developers)随后如何了解如何通过分析跟踪来设计AEM Mobile应用程序。

最后， [AEM管理员](#administrators)学习：

* 创建云服务以AdobeMobile Services
* 创建移动服务配置并关联报表包
* 将移动服务配置与移动设备应用程序关联
* 通过AEM Apps Command Center查看量度
* 将AMS SDK配置分配给您的移动设备应用程序

## 对于开发人员 — 将Analytics集成到您的应用程序{#for-developers-integrate-analytics-into-your-app}

**先决条件：** AEM管理员需要配置AdobeMobile Services云配置， [如下所述](#amscloudserviceconfig)。

开发人员负责根据需要将分析添加到AEM Mobile应用程序](/help/mobile/phonegap-add-analytics-to-apps.md)，以跟踪、报告和了解您的用户如何与您的移动设备应用程序内容交互，以及测量关键生命周期量度，如启动次数、应用程序内时间和崩溃率。[

## 对于管理员 — 配置AdobeMobile ServicesCloud Service{#for-administrators-configure-the-adobe-mobile-services-cloud-service}

为了利用Mobile ServicesAdobe，您需要使用Adobe Analytics帐户信息配置AEM Mobile ServicesCloud Service。 应用程序命令中心提供了一个&#x200B;**分析量度**&#x200B;拼贴，您可以在其中创建云服务并将其与移动设备应用程序关联。

首先，单击分析量度拼贴中的齿轮图标，将云服务配置到您的移动设备应用程序。

![chlimage_1-125](assets/chlimage_1-125.png)

单击分析量度拼贴中的齿轮图标将打开“配置Mobile Services Analytics”模式对话框。 从“选择Mobile Service配置”下拉菜单中选择您的配置。 如果需要创建新配置，请单击扳手按钮。

要创建AdobeMobile Service云服务，需要执行两个步骤：连接到服务并选择要分配给配置的报表包。

要开始，请单击功能板中“管理Cloud Services”拼贴上的“+”按钮。

![chlimage_1-126](assets/chlimage_1-126.png)

单击“**+**”按钮时，将显示&#x200B;**添加Cloud Service**&#x200B;向导。

![chlimage_1-127](assets/chlimage_1-127.png)

通过填写必填字段来选择或创建新的Mobile Service配置，如下所示。 AEM管理员需要此信息才能成功创建与AdobeMobile Services的连接。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帐户设置后，系统将提示您选择应用程序。 这样做会将AdobeMobile Service分析报表关联到该应用程序。

选择所需的Mobile服务，然后单击“更新”以分配Mobile服务配置并关闭对话框。

现在，您已将移动服务配置关联到AEM Mobile应用程序，此拼贴将开始获取量度数据并开始报告。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK配置文件{#adobe-mobile-services-sdk-config-file}

此时，您的移动设备应用程序已与云服务关联，但移动设备应用程序尚不知道如何将收集的移动量度传回Adobe Analytics。 要将移动设备应用程序连接到Adobe Analytics，需要将AdobeMobile Services SDK配置文件添加到Adobe Experience Manager。

在分析量度拼贴中，单击箭头图标以显示下载/上传AMS SDK配置菜单条目。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是从AdobeMobile Services获取SDK配置，单击“下载AMS SDK配置”会将您重定向到AdobeMobile Services网站，您可以从中下载配置文件。 获取ADBMobileConfig.json文件后，单击“上传AMS SDK配置”以将配置文件上传到AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

单击“上传AdobeMobile Services应用程序配置”按钮，浏览ADBMobileConfig.json文件，然后单击“上传”。

现在，移动设备应用程序可以访问ADBMobileConfig.json文件，并且它已了解如何传回Adobe Analytics并开始报告有助于推动应用程序取得成功的重要量度值。

## 接下来是什么？{#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序的内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用AdobeMobile Analytics跟踪我的应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供个性化的应用程序体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)