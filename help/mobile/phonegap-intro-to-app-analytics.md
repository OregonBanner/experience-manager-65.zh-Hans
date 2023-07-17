---
title: 通过AdobeMobile Analytics跟踪应用程序性能
description: 借助AdobeMobile Services，您可以通过跟踪移动应用程序的使用情况、应用程序崩溃情况、设备详细信息以及其他诸多关键量度，深入了解用户如何使用移动应用程序。 关注此页面以了解更多信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# 通过AdobeMobile Analytics跟踪应用程序性能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

您希望提高客户转化率和忠诚度。

您希望向客户提供相关且富有吸引力的体验。

您的AEM Mobile应用程序对您的营销活动有何作用？

如何优化移动应用程序以便为用户提供最佳体验？

借助AdobeMobile Services，您可以通过跟踪移动应用程序的使用情况、应用程序崩溃情况、设备详细信息以及其他诸多关键量度，深入了解用户如何使用移动应用程序。

Adobe Experience Manager Mobile可直接从AEM Mobile应用程序仪表板中一窥您的移动分析的详细信息。 此 **移动量度图块** 仪表板中的仪表板为您的移动应用程序提供Real-Time Analytics，允许开发人员、作者和管理员快速了解您的移动应用程序的运行状况。 在封面下，为分析提供支持的 [Adobe移动分析](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK。 AdobeMobile Analytics SDK可以本机插入您的应用程序，也可以通过用于Web视图的PhoneGap Bridge插件插入。 在设备上收集并缓存量度，直到设备连接为止，届时，数据将推送到AdobeMobile Services云以供报告和分析。

AdobeMobile Analytics SDK提供以下功能：

1. **为移动渠道收集数据**  — 收集您的移动网站和所有主要操作系统上的应用程序的全面数据。
1. **移动参与分析**  — 了解用户在移动应用程序、网站或视频中的参与情况，包括消费者启动渠道的频率、他们是否从中购买等。
1. **移动应用程序功能板和报表**  — 获取包含应用程序生命周期量度和应用商店量度的使用情况报表 — 请参阅用户、启动次数、平均会话时长、保留时长和崩溃次数趋势。
1. **移动营销活动分析**  — 量化特定于移动设备的促销活动（如短信、移动搜索广告、移动显示广告和二维码）的有效性。
1. **地理位置分析**  — 通过GPS位置或目标点，查找您的应用程序用户启动位置并与您的移动体验交互。
1. **路径分析**  — 了解用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素吸引用户以及哪些元素导致用户流失。

此部分介绍如何 [AEM开发人员](#developers) 然后，可以了解如何通过Analytics跟踪来检测AEM Mobile应用程序。

最后， [AEM管理员](#administrators) 了解：

* 创建云服务以Adobe移动服务
* 创建移动服务配置并关联报表包
* 将移动服务配置关联到移动应用程序
* 通过AEM应用程序命令中心查看指标
* 将AMS SDK配置分配给您的移动应用程序

## 对于开发人员 — 将Analytics集成到您的应用程序中 {#for-developers-integrate-analytics-into-your-app}

**先决条件：** AEM管理员必须配置AdobeMobile Services云配置， [如下所述](#amscloudserviceconfig).

开发人员负责 [将analytics添加到AEM Mobile应用程序](/help/mobile/phonegap-add-analytics-to-apps.md) 跟踪、报告和了解用户如何参与移动应用程序内容以及衡量关键生命周期量度（如启动次数、应用程序逗留时间和崩溃率）所必需的。

## 对于管理员 — 配置AdobeMobile ServicesCloud Service {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

要使用AdobeMobile Services，您必须使用Adobe Analytics帐户信息配置AEMAdobeMobile ServicesCloud Service。 应用程序命令中心提供 **分析量度** 可在其中创建云服务并将其与移动应用程序关联的图块。

通过单击分析量度图块上的齿轮图标，开始为移动设备应用程序配置云服务。

![chlimage_1-125](assets/chlimage_1-125.png)

单击分析量度拼贴中的齿轮图标可打开“配置Mobile Services Analytics”模式对话框。 从“选择移动服务配置”下拉列表中选择您的配置。 如果必须创建配置，请单击扳手按钮。

要创建AdobeMobile Service云服务，需要执行两个步骤：连接到服务和选择要分配给配置的报表包。

要开始，请单击功能板中“管理Cloud Services”拼贴上的“+”按钮。

![chlimage_1-126](assets/chlimage_1-126.png)

单击“**+**&#39;按钮， **添加Cloud Service** 将显示向导。

![chlimage_1-127](assets/chlimage_1-127.png)

通过填写以下必填字段来选择或创建新的移动服务配置。 AEM管理员需要此信息才能成功创建与AdobeMobile Services的连接。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帐户设置后，系统会提示您选择应用程序。 这样做会将Adobe Mobile Service Analytics报表连接到该应用程序。

选择所需的移动服务，然后单击“更新”以分配移动服务配置并关闭对话框。

现在，您已将Mobile Service配置关联到AEM Mobile应用程序，磁贴将开始获取量度数据并开始报告。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK配置文件 {#adobe-mobile-services-sdk-config-file}

此时，您的移动应用程序已与云服务关联，但移动应用程序还不知道如何将收集的移动量度传回Adobe Analytics。 要将移动设备应用程序连接到Adobe Analytics，必须将AdobeMobile Services SDK配置文件添加到Adobe Experience Manager。

在分析量度图块中，单击箭头图标以显示下载/上传AMS SDK配置菜单项。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是从AdobeMobile Services获取SDK配置。 单击“下载AMS SDK配置”可重定向到AdobeMobile Services网站，您可以从网站下载配置文件。 获取ADBMobileConfig.json文件后，单击“上传AMS SDK配置”以将配置文件上传到AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

单击“上传AdobeMobile Services应用程序配置”按钮并浏览ADBMobileConfig.json文件，然后单击“上传”。

现在，移动设备应用程序已经有权访问ADBMobileConfig.json文件，并且已经了解如何与Adobe Analytics通信并开始报告有助于推动应用程序取得成功的重要量度值。

## 后续内容? {#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe移动分析跟踪我的应用程序的性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供个性化的应用程序体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)
