---
title: 使用Adobe移动分析跟踪应用程序性能
seo-title: 使用Adobe移动分析跟踪应用程序性能
description: 通过AdobeMobile Services，您可以通过跟踪使用情况、应用程序崩溃、设备详细信息以及移动应用程序的许多其他关键指标，了解用户如何使用您的移动应用程序。 可查看本页以了解更多信息。
seo-description: 通过AdobeMobile Services，您可以通过跟踪使用情况、应用程序崩溃、设备详细信息以及移动应用程序的许多其他关键指标，了解用户如何使用您的移动应用程序。 可查看本页以了解更多信息。
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---


# 使用AdobeMobile Analytics跟踪应用程序性能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

您希望提高客户转化率和忠诚度。

您希望为客户提供相关且有吸引力的体验。

您的AEM Mobile应用程序对您的营销活动有何作用？

您如何调整移动应用程序以为用户提供最佳体验？

通过AdobeMobile Services，您可以通过跟踪使用情况、应用程序崩溃、设备详细信息以及移动应用程序的许多其他关键指标，了解用户如何使用您的移动应用程序。

Adobe Experience Manager Mobile直接从AEM Mobile应用程序仪表板中了解您的移动分析的详细信息。 该仪表板中的&#x200B;**移动度量标题**&#x200B;为移动应用程序提供实时分析，使开发人员、作者和管理员能够快速了解移动应用程序的运行状况。 [Adobe移动分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK。 AdobeMobile Analytics SDK可以本机插入您的应用程序，也可以通过PhoneGap桥接插件进行Web查看。 在设备上收集和缓存度量，直到连接设备，数据将推送到AdobeMobile Services Cloud进行报告和分析。

Adobe移动分析SDK提供以下内容：

1. **针对移动渠道的收集** -在所有主要操作系统上为您的移动网站和应用程序收集全面的数据。
1. **移动互动分析** -了解移动应用、网站或视频中的用户互动，包括消费者启动渠道的频率、是否从中购买，等等。
1. **移动App仪表板和报告** -获取包含App生命周期指标和App商店指标的使用情况报告——查看用户趋势、启动情况、平均会话长度、保留期长度和崩溃情况。
1. **移动活动分析** -量化移动特定活动（如短信、移动搜索广告、移动展示广告和二维码）的有效性。
1. **地理位置分析** -按GPS定位或兴趣点查找应用程序用户启动您的移动体验并与之交互的位置。
1. **寻路分析** -了解用户如何在您的应用程序中导航，以确定哪些屏幕和UI元素是吸引用户的，哪些是导致用户放弃的。

本节介绍[AEM开发人员](#developers)随后如何学习如何通过分析跟踪来指导AEM Mobile应用程序。

最后，[AEM管理员](#administrators)学习：

* 创建用于Adobe移动服务的云服务
* 创建移动服务配置并关联报表包
* 将移动服务配置关联到移动应用程序
* 视图指标通过AEM Apps命令中心
* 将AMS SDK配置分配给您的移动应用程序

## 对于开发人员——将Analytics集成到您的应用程序{#for-developers-integrate-analytics-into-your-app}

**入门项** 目：AEM管理员需要配置AdobeMobile Services云配置， [如下所述](#amscloudserviceconfig)。

开发人员负责根据需要将分析添加到AEM Mobile应用[，以跟踪、报告和了解用户如何与移动应用内容互动以及衡量关键生命周期指标，如启动、应用程序停留时间和崩溃率。](/help/mobile/phonegap-add-analytics-to-apps.md)

## 对于管理员——配置AdobeMobile ServicesCloud Service{#for-administrators-configure-the-adobe-mobile-services-cloud-service}

为了利用AdobeMobile Services，您需要使用您的Adobe Analytics帐户信息配置AEMAdobeMobile ServicesCloud Service。 应用程序命令中心提供&#x200B;**分析指标**&#x200B;拼贴，您可以在其中创建云服务并将其与移动应用程序关联。

单击“分析指标”拼贴上的齿轮图标，开始将云服务配置到您的移动应用程序。

![chlimage_1-125](assets/chlimage_1-125.png)

单击“分析度量”拼贴中的齿轮图标将打开“配置Mobile Services Analytics”模态对话框。 从“选择Mobile Service Configuration”下拉菜单中选择配置。 如果需要创建新配置，请单击扳手按钮。

要创建AdobeMobile Service云服务，需要执行两个步骤：连接到服务并选择要分配给配置的报告套件。

首先，单击仪表板中“管理Cloud Services”拼贴上的“+”按钮。

![chlimage_1-126](assets/chlimage_1-126.png)

单击“**+**”按钮后，将显示&#x200B;**添加Cloud Service**&#x200B;向导。

![chlimage_1-127](assets/chlimage_1-127.png)

通过填写必填字段来选择或创建新的移动服务配置，如下所示。 您的AEM管理员需要此信息才能成功创建与AdobeMobile Services的连接。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帐户设置后，将提示您选择应用程序。 这样做会将AdobeMobile Service分析报告连接到该应用程序。

选择所需的移动服务，然后单击“更新”以分配移动服务配置并关闭对话框。

现在，您已将移动服务配置关联到AEM Mobile应用程序，磁贴将开始获取度量数据并开始报告。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK配置文件{#adobe-mobile-services-sdk-config-file}

此时，您的移动应用程序与云服务相关联，但移动应用程序尚不知道如何将收集的移动指标传回Adobe Analytics。 要将移动应用程序连接到Adobe Analytics，需要将AdobeMobile Services SDK Config文件添加到Adobe Experience Manager。

在“分析指标”拼贴中，单击箭头图标以显示“下载／上传AMS SDK配置”菜单条目。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是从AdobeMobile Services获取SDK配置，单击“下载AMS SDK配置”将将您重定向到AdobeMobile Services网站，从中下载配置文件。 获取ADBMobileConfig.json文件后，单击“上传AMS SDK配置”以将配置文件上传到AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

单击“上传AdobeMobile Services应用程序配置”按钮并浏览ADBMobileConfig.json文件，然后单击“上传”。

现在，移动应用程序可以访问ADBMobileConfig.json文件，它知道如何与Adobe Analytics进行交流并开始报告这些重要指标值，这些重要指标值将帮助您的应用程序取得成功。

## 下一步是什么？{#what-s-next}

1. [开始我的AEM Mobile应用程序体验](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的应用程序的内容](/help/mobile/phonegap-manage-app-content.md)
1. [构建我的应用程序](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe移动分析跟踪我的应用程序的性能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [通过Adobe Target提供个性化的App体验](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用户发送重要消息](/help/mobile/phonegap-push-notifications.md)