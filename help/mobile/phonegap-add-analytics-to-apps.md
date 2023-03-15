---
title: 将Adobe Analytics添加到您的移动应用程序
seo-title: Add Adobe Analytics to your Mobile Application
description: 关注此页面，了解如何通过与Analytics Mobile Services集成，在AEM应用程序中使用移动应用程序Adobe。
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 将Adobe Analytics添加到您的移动应用程序{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

想要为您的移动应用程序用户打造引人入胜的相关体验？ 如果您没有使用AdobeMobile Services SDK来监控和衡量应用程序的生命周期和使用情况，那么您的决策依据是什么？ 您最忠诚的客户在哪里？ 如何确保保持相关度并优化转化？

您的用户是否正在访问所有内容？ 他们是否正在放弃该应用，如果是，在哪里放弃？ 他们多长时间留在应用程序中，多长时间返回使用应用程序？ 您可以引入哪些更改，然后衡量这些更改是否会增加维系率？ 崩溃率怎么样，您的应用程序是否为用户而崩溃？

充分利用 [移动应用程序分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) 通过与集成，在您的AEM应用程序中 [Adobe移动服务](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

检测您的AEM应用程序，以跟踪、报告和了解用户如何参与移动应用程序和内容，并衡量关键生命周期量度，例如启动次数、应用程序逗留时间和崩溃率。

此部分介绍AEM的工作原理 *开发人员* 可以：

* 将Mobile Analytics集成到移动应用程序
* 使用Bloodhound测试您的分析跟踪

## 先决条件 {#prerequisties}

AEM Mobile需要Adobe Analytics帐户才能在您的应用程序中收集和报告跟踪数据。 作为配置的一部分，AEM *管理员* 将首先需要：

* 在Mobile Services中设置Adobe Analytics帐户，并为您的应用程序创建报表包。
* 在Adobe Experience Manager (AEM)中配置AMSCloud Service。

## 对于开发人员 — 将Mobile Analytics集成到您的应用程序中 {#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以提取配置文件 {#configure-contentsync-to-pull-in-configuration-file}

设置Analytics帐户后，您将需要创建内容同步配置以将内容拉入您的移动应用程序。

有关其他详细信息，请参阅配置内容同步内容。 该配置将需要指示内容同步将ADBMobileConfig放入/www目录。 例如，在Geometrixx Outdoors应用程序中，Content Sync配置位于： */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-config/ams-ADBMobileConfig*. 此外，还有一个用于开发的配置；但是，对于Geometrixx Outdoors，它与非开发配置相同。

有关如何从移动应用程序AEM应用程序仪表板下载ADBMobileConfig的详细信息，请参阅Analytics - Mobile Services -AdobeMobile Services SDK配置文件。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每个平台都需要将ADBMobileConfig复制到特定位置。

如果使用PhoneGap CLI进行构建，则可以使用cordova构建挂接脚本来完成此操作。 这可以在Geometrixx Outdoors应用程序中查看，网址为：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

对于iOS，该文件需要复制到Xcode项目的 **资源** 目录(例如 &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;)。 如果应用程序面向Android，则要复制到其中的路径为“platforms/android/assets/ADBMobileConfig.json”。 有关在PhoneGap CLI构建期间使用挂接的详细信息，请参阅 [三个挂接您的Cordova/PhoneGap项目需求](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### 在应用程序中添加AMS插件 {#add-the-ams-plugin-in-the-app}

对于要收集数据的应用程序，需要将AdobeMobile Services (AMS)插件包含在应用程序中。 通过将插件作为功能包含在应用程序的config.xml中，另一个Cordova挂接可用于在PhoneGap Build过程中自动添加插件。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors应用程序config.xml位于 */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content/phonegap/www/config.xml*. 上述示例要求使用特定版本的插件，方法是在插件URL后添加“#”，然后添加标记值。 这是要遵循的良好实践，以确保在构建期间添加未经测试的插件时不会出现意外问题。

执行这些步骤后，您的应用程序将能够报告Adobe Analytics提供的所有生命周期量度。 这包括启动次数、崩溃次数和安装次数等数据。 如果这是您关心的唯一数据，则表示您已完成。 如果要收集自定义数据，则需要检测代码。

### 检测代码以进行完整的应用程序跟踪 {#instrument-your-code-for-full-app-tracking}

中提供了多个跟踪API [AMS Phonegap插件API。](https://experienceleague.adobe.com/docs/mobile-services/ios/phonegap-ios/phonegap-methods.html)

这些功能允许您跟踪状态和操作，例如用户在应用程序中导航到的页面位置，以及最常使用哪些控件。 检测应用程序以进行跟踪的最简单方法是使用AMS插件提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

有关参考，您可以查看Geometrixx Outdoors应用程序中的代码。 在Geometrixx Outdoors应用程序中，使用ADB.trackState()方法跟踪所有页面导航。 有关更多详细信息，请查看/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的源代码

通过使用这些方法调用检测源代码，您可以收集应用程序的完整量度。

#### 用于连接到AMS的属性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp*&#x200B;我公开以下用于连接到AMS的属性：

| **标签** | **描述** | **默认** |
|---|---|---|
| API端点 | AdobeMobile Services HTTP API的基本URL | https://api.omniture.com |
| 配置端点 | 用于检索给定报表包ID的ADB移动配置的URL | /ams/1.0/app/config/ |
| Mobile Service应用程序 | 获取用户公司内的应用程序列表 | /ams/1.0/apps |
