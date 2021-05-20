---
title: 将Adobe Analytics添加到移动应用程序
seo-title: 将Adobe Analytics添加到移动应用程序
description: 请阅读本页，了解如何通过与AEM Mobile Services集成，在Analytics应用程序中使用Mobile App Analytics。
seo-description: 请阅读本页，了解如何通过与AEM Mobile Services集成，在Analytics应用程序中使用Mobile App Analytics。
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 将Adobe Analytics添加到移动应用程序{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

想要为您的移动应用程序用户构建引人入胜的相关体验？ 如果您没有使用Mobile Services SDK来监控和测量应用程序生命周期和使用情况，那么您的决策依据是什么？ 您最忠诚的客户在哪里？ 如何确保保持相关性并优化转化？

您的用户是否访问了所有内容？ 他们会放弃应用吗？如果是，会在哪里？ 他们在应用程序中停留的频率是多久？他们回来使用该应用程序的频率是多久？ 您可以引入哪些更改，然后测量这些更改会提高保留率？ 那么崩溃率呢，您的应用程序是否会对用户造成崩溃？

通过与[Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html)集成，在AEM应用程序中利用[Mobile App Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html)Adobe。

利用AEM应用程序，可跟踪、报告和了解用户如何与您的移动设备应用程序和内容交互，以及如何测量关键生命周期量度，如启动次数、应用程序内时间和崩溃率。

本节介绍AEM *Developers*&#x200B;如何：

* 将Mobile Analytics集成到移动设备应用程序中
* 使用Bloodhound测试分析跟踪

## 先决条件 {#prerequisties}

AEM Mobile需要Adobe Analytics帐户才能收集和报告应用程序中的跟踪数据。 作为配置的一部分， AEM *Administrator*&#x200B;首先需要：

* 在Mobile Services中设置Adobe Analytics帐户并为您的应用程序创建报表包。
* 在Adobe Experience Manager(AEM)中配置AMSCloud Service。

## 对于开发人员 — 将Mobile Analytics集成到您的应用程序{#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以提取配置文件{#configure-contentsync-to-pull-in-configuration-file}

设置Analytics帐户后，您将需要创建内容同步配置，以将内容提取到您的移动设备应用程序中。

有关其他详细信息，请参阅配置内容同步内容。 配置将需要指示内容同步将ADBMobileConfig放入/www目录中。 例如，在Geometrixx Outdoors应用程序中，内容同步配置位于：*/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*。 还有开发配置；但是，它与Geometrixx Outdoors中的非开发配置相同。

有关如何从Mobile Application AEM应用程序功能板下载ADBMobileConfig的更多详细信息，请参阅Analytics - Mobile Services -AdobeMobile Services SDK配置文件。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每个平台都要求将ADBMobileConfig复制到特定位置。

如果使用PhoneGap CLI进行构建，则可以使用cordova构建挂接脚本来完成此操作。 可在Geometrixx Outdoors应用程序中查看此内容：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js。*

对于iOS，需要将文件复制到Xcode项目的&#x200B;**Resources**&#x200B;目录(例如， &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;)。 如果针对Android定位了应用程序，则复制到的路径为“platforms/android/assets/ADBMobileConfig.json”。 有关在PhoneGap CLI构建期间使用挂钩的更多详细信息，请参阅[Cordova/PhoneGap项目需要的三个挂钩](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。

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

### 在应用程序{#add-the-ams-plugin-in-the-app}中添加AMS插件

AdobeMobile Services(AMS)插件需要作为应用程序的一部分包含，才能让应用程序收集数据。 通过将插件作为功能包含在应用程序config.xml中，另一个Cordova挂接可用于在PhoneGap构建过程中自动添加插件。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors应用程序config.xml位于&#x200B;*/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*。 以上示例通过在插件URL后添加“#”和标记值，请求使用插件的特定版本。 这是一种良好的做法，可确保在内部版本期间添加未经测试的插件时，不会出现意料之外的问题。

执行这些步骤后，您的应用程序将被启用以报告由Adobe Analytics提供的所有生命周期量度。 这包括启动次数、崩溃次数和安装次数等数据。 如果这是您唯一关心的数据，那么您就完成了。 如果要收集自定义数据，则需要设置代码。

### 设置代码以进行完整的应用程序跟踪{#instrument-your-code-for-full-app-tracking}

[AMS Phonegap Plugin API中提供了多个跟踪API。](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

这些功能允许您跟踪状态和操作，例如用户在应用程序中导航到的页面位置（最常使用的控件）。 使用应用程序进行跟踪的最简单方法是利用AMS插件提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

要获取参考，您可以查看Geometrixx Outdoors应用程序中的代码。 在Geometrixx Outdoors应用程序中，使用ADB.trackState()方法跟踪所有页面导航。 有关更多详细信息，请参阅/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的源代码

通过使用这些方法调用检测源代码，您可以针对应用程序收集完整量度。

#### 连接到AMS {#properties-for-connecting-to-ams}的属性

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl公开了以下用于连接到AMS的属性：

| **标签** | **描述** | **默认** |
|---|---|---|
| API端点 | AdobeMobile Services HTTP API的基本URL | https://api.omniture.com |
| 配置端点 | 用于检索给定报表包ID的ADB移动配置的URL | /ams/1.0/app/config/ |
| Mobile Service应用程序 | 获取用户公司中的应用程序列表 | /ams/1.0/apps |
