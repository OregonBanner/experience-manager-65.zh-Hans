---
title: 将Adobe Analytics添加到您的移动应用程序
description: 关注此页面，了解如何通过与Analytics Mobile Services集成，在Adobe Experience Manager应用程序中使用移动应用程序Adobe。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# 将Adobe Analytics添加到您的移动应用程序{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

想要为您的移动应用程序用户打造引人入胜的相关体验？ 如果您没有使用AdobeMobile Services SDK来监控和衡量应用程序的生命周期和使用情况，那么您的决策依据是什么？ 您最忠诚的客户在哪里？ 如何保证您保持相关状态并优化转化？

您的用户是否正在访问所有内容？ 他们是否在放弃该应用程序，如果是，在哪里放弃？ 他们多久留在应用程序中，多久回访一次以使用应用程序？ 您可以引入哪些更改，然后衡量这些更改是否提高了客户保留率？ 崩溃率如何？您的应用程序是否为用户而崩溃？

充分利用 [移动应用程序分析](https://business.adobe.com/products/analytics/mobile-marketing.html) 通过与集成，在您的Adobe Experience Manager (AEM)应用程序中 [Adobe移动服务](https://business.adobe.com/products/campaign/mobile-marketing.html).

检测您的AEM应用程序，以跟踪、报告和了解用户如何参与您的移动设备应用程序和内容，并测量关键生命周期量度，例如启动次数、应用程序逗留时间和崩溃率。

本节介绍AEM的工作原理 *开发人员* 可以：

* 将Mobile Analytics集成到移动应用程序
* 使用Bloodhound测试您的分析跟踪

## 前提条件 {#prerequisties}

AEM Mobile需要使用Adobe Analytics帐户来收集和报告应用程序中的跟踪数据。 作为配置的一部分，AEM *管理员* 必须首先：

* 在Mobile Services中设置Adobe Analytics帐户，并为您的应用程序创建报表包。
* 在Adobe Experience Manager (AEM)中配置AMSCloud Service。

## 对于开发人员 — 将移动分析集成到您的应用程序中 {#for-developers-integrate-mobile-analytics-into-your-app}

### 配置ContentSync以提取配置文件 {#configure-contentsync-to-pull-in-configuration-file}

设置Analytics帐户后，创建内容同步配置以将内容拉入您的移动应用程序。

有关其他详细信息，请参阅配置内容同步内容。 配置将需要指示内容同步将ADBMobileConfig放入/www目录。 例如，在Geometrixx Outdoors应用程序中，Content Sync配置位于： */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-config/ams-ADBMobileConfig*. 此外，还有一个用于开发的配置；但是，它与Geometrixx Outdoors中的非开发配置相同。

有关如何从移动设备应用程序AEM应用程序仪表板下载ADBMobileConfig的详细信息，请参阅Analytics - Mobile Services -AdobeMobile Services SDK配置文件。

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

如果使用PhoneGap CLI进行构建，则可以使用cordova构建挂接脚本来完成此操作。 您可以在Geometrixx Outdoors应用程序中看到以下内容：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

对于iOS，该文件需要复制到Xcode项目的 **资源** 目录(例如“platforms/ios/Geometrixx/Resources/ADBMobileConfig.json”)。 如果应用程序针对Android™，则要复制到的路径为“platforms/android/assets/ADBMobileConfig.json”。 有关在PhoneGap CLI构建期间使用挂接的详细信息，请参阅 [三个挂接Cordova/PhoneGap项目需求](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

对于要收集数据的应用程序，需要将AdobeMobile Services (AMS)插件作为应用程序的一部分包含在内。 通过将插件作为功能包含在应用程序的config.xml中，可以使用另一个Cordova挂接在PhoneGap Build过程中自动添加插件。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors应用程序config.xml位于 */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content/phonegap/www/config.xml*. 上述示例请求使用特定版本的插件，方法是在插件URL后添加“#”，然后添加标记值。 这是要遵循的一个良好实践，以确保不会出现因在构建期间添加未经测试的插件而导致的意外问题。

执行这些步骤后，您的应用程序将能够报告Adobe Analytics提供的所有生命周期量度。 这包括启动次数、崩溃次数和安装次数等数据。 如果这是您关心的唯一数据，则表示您已完成。 如果要收集自定义数据，则必须检测代码。

### 检测代码以进行完整的应用程序跟踪 {#instrument-your-code-for-full-app-tracking}

中提供了多个跟踪API [AMS Phonegap插件API。](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

这些功能允许您跟踪状态和操作，如用户在应用程序中导航到的页面，以及最常使用的控件。 检测应用程序以进行跟踪的最简单方法是使用AMS插件提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

有关参考，请查看Geometrixx Outdoors应用程序中的代码。 在Geometrixx Outdoors应用程序中，使用ADB.trackState()方法跟踪所有页面导航。 有关更多详细信息，请参阅/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的源代码

通过使用此方法调用检测源代码，您可以收集应用程序的完整量度。

#### 用于连接到AMS的属性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp*&#x200B;我公开以下属性以用于连接到AMS：

| **标签** | **描述** | **默认** |
|---|---|---|
| API端点 | AdobeMobile Services HTTP API的基本URL | https://api.omniture.com |
| 配置端点 | 用于检索给定报表包ID的ADB移动设备配置的URL | /ams/1.0/app/config/ |
| Mobile Service应用程序 | 获取用户公司内的应用程序列表 | /ams/1.0/apps |
