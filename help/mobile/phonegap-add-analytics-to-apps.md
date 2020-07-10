---
title: 将AdobeAnalytics添加到您的移动应用程序
seo-title: 将AdobeAnalytics添加到您的移动应用程序
description: 可查看本页，了解如何通过与Adobe Mobile Services集成在AEM应用程序中使用移动应用程序Analytics。
seo-description: 可查看本页，了解如何通过与Adobe Mobile Services集成在AEM应用程序中使用移动应用程序Analytics。
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# 将AdobeAnalytics添加到您的移动应用程序{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

想要为您的移动应用程序用户构建引人入胜的相关体验？ 如果您不使用Adobe Mobile Services SDK来监视和衡量应用程序生命周期和使用情况，则您的决策依据是什么？ 您最忠诚的客户在哪里？ 您如何保证保持相关性并优化转化率？

您的用户是否访问所有内容？ 他们是否会放弃这款应用，如果是，会在哪里？ 他们在应用程序中停留的频率是多少？他们回来使用该应用的频率是多少？ 您可以引入哪些更改，然后衡量这些更改可以提高保留率？ 崩溃率如何？您的应用程序是否会对用户造成崩溃？

通过与Adobe Mobile [Services集成](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) ，在AEM应用程序中充分利 [用Mobile App](https://www.adobe.com/marketing-cloud/mobile-marketing.html)Analytics。

利用AEM Apps跟踪、报告和了解用户如何与您的移动App和内容互动，并衡量关键生命周期指标，如启动次数、应用程序停留时间和崩溃率。

本节介绍AEM开发人 *员如何* :

* 将移动Analytics集成到您的移动应用程序中
* 使用Bloodhound测试分析跟踪

## 先决条件 {#prerequisties}

AEM Mobile需要AdobeAnalytics帐户来收集和报告应用程序中的跟踪数据。 作为配置的一部分， *AEM* Administrator首先需要：

* 在Mobile Services中设置AdobeAnalytics帐户并为应用程序创建报表包。
* 在Adobe Experience Manager(AEM)中配置AMSCloud Service。

## 对于开发人员——将Mobile Analytics集成到您的应用程序中 {#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以拉入配置文件 {#configure-contentsync-to-pull-in-configuration-file}

设置Analytics帐户后，您需要创建内容同步配置以将内容拉入您的移动应用程序。

有关其他详细信息，请参阅配置内容同步内容。 配置需要指示内容同步将ADBMobileConfig放入/www目录。 例如，在Geometrixx Outdoors应用程序中，内容同步配置位于： */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*。 还有一种发展配置； 但是，在Geometrixx Outdoors的情况下，它与非开发配置相同。

有关如何从您的Mobile Application AEM Apps仪表板下载ADBMobileConfig的更多详细信息，请参阅Analytics- Mobile Services - Adobe Mobile Services SDK配置文件。

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

如果使用PhoneGap CLI进行构建，则可以使用cordova构建挂接脚本完成此操作。 这可在Geometrixx Outdoors应用程序中查看，网址为：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js。*

对于iOS，需要将文件复制到XCode项目的“资 **源** ”目录(如 “platforms/ios/Geometrixx/Resources/ADBMobileConfig.json”)。 如果应用程序针对Android，则要复制到的路径为“platforms/android/assets/ADBMobileConfig.json”。 有关在PhoneGap CLI构建过程中使用挂钩的更多详细信息， [请参阅Cordova/PhoneGap项目需要的“三个挂钩”](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。

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

要使应用程序收集数据，Adobe Mobile Services(AMS)插件需要作为应用程序的一部分包含在其中。 通过将插件作为功能包含在应用程序的config.xml中，可以在PhoneGap构建过程中使用另一个Cordova挂接自动添加插件。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors App config.xml位 *于/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*。 上面的示例通过在插件URL后添加“#”和标记值来请求要使用的插件的特定版本。 这是确保在构建过程中添加未经测试的插件时不会出现意外问题的最佳实践。

执行这些步骤后，您的应用程序将能够报告AdobeAnalytics提供的所有生命周期指标。 这包括启动、崩溃和安装等数据。 如果这是您关心的唯一数据，那么您就完成了。 如果要收集自定义数据，则需要指导您进行编码。

### 对代码进行全面的应用程序跟踪 {#instrument-your-code-for-full-app-tracking}

AMS Phonegap插件API中提 [供了多个跟踪API。](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

这些选项将允许您跟踪状态和操作，如用户在应用程序中导航到的页面的位置，这些控件的使用率最高。 使用AMS插件提供的AnalyticsAPI，最轻松地指导您的应用程序进行跟踪。

* ADB.trackState()
* ADB.trackAction()

要获得参考，您可以查看Geometrixx Outdoors应用程序中的代码。 在Geometrixx Outdoors应用程序中，使用ADB.trackState()方法跟踪所有页面导航。 有关更多详细信息，请查看/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的源代码

通过使用这些方法调用检测源代码，您可以针对应用程序收集完整指标。

#### 连接到AMS的属性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl公开以下用于连接到AMS的属性：

| **标签** | **描述** | **默认** |
|---|---|---|
| API端点 | Adobe Mobile Services HTTP API的基本URL | https://api.omniture.com |
| 配置端点 | 用于检索给定报告包ID的ADB移动配置的URL | /ams/1.0/app/config/ |
| 移动服务应用程序 | 在用户列表中获取应用程序公司 | /ams/1.0/apps |

