---
title: 在AEM中开发移动应用程序
seo-title: 在AEM中开发移动应用程序
description: 请阅读本页，以开始使用Adobe PhoneGap Enterprise在AEM中开发移动应用程序。
seo-description: 请阅读本页，以开始使用Adobe PhoneGap Enterprise在AEM中开发移动应用程序。
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# 在AEM {#developing-mobile-applications-in-aem}中开发移动应用程序

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM利用Adobe PhoneGap和Adobe发布解决方案，允许您创建和管理内容丰富且基于实用工具的跨平台移动应用程序：

* 在一个位置管理您公司的所有移动设备应用程序。
* 在开发和暂存环境中查看应用程序，无需复杂的配置配置文件，也无需额外努力来构建和上传应用程序以进行共享。
* 使用AEM创作环境为您的应用程序创建和管理富内容。
* 将HTML5与Adobe PhoneGap结合使用，以通过设备原生功能创建丰富的体验。
* 通过Cordova WebViews将HTML5 Webview引入新的或预先存在的&#x200B;**native**&#x200B;应用程序。
* 在所有交付渠道（包括Web、移动Web、移动应用程序和打印）中创建、组织和共享丰富的多媒体内容。

AEM与Adobe **[PhoneGap Build服务](https://build.phonegap.com/)**&#x200B;集成，以简化应用程序构建和部署过程。

**Adobe** ContentSyncenal让用户能够轻松地将页面和内容更新通过空中(OTA)下载到其设备，而无需重新安装应用程序或从应用商店、Google Play或其他应用程序源下载。

**Adobe** Analytics完全集成到AEM应用程序中，并允许详细跟踪分发、地理位置、操作系统、设备、点击流、iBeacon跟踪等。

## 创建应用程序{#creating-apps}

开发人员可以使用[AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)以及[https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)中的其他资源，通过PhoneGap引导AEM应用程序，包括运行Cordova Webviews的引用本机应用程序。

Starter Kit Git存储库的自述文件包含有关使用Starter Kit的教程：

* 自定义品牌策略
* Maven构建和部署目标示例
* 源代码管理存储库配置
* 安装和部署到本地或远程AEM实例中
* 从AEM卸载

>[!NOTE]
>
>其他引用实施源（包括实验室）可在GitHub [此处](https://github.com/adobe-marketing-cloud-apps)和“kitchen-sink”源[此处](https://github.com/blefebvre/aem-phonegap-kitchen-sink)找到。

## 针对IOS 9和HTTP主机{#developing-for-ios-and-http-hosts}进行开发

iOS开发人员应当注意到在iOS 9上运行的Cordova应用程序存在一个打开的问题。 此问题会阻止向不安全的主机发出请求(例如&#x200B;*http://localhost:4502*)。 此问题将通过即将发布的cordova-ios（由Cordova CLI使用）来解决，但与此同时，有两种解决方法可用：

1. 作为即时的解决方法，您仍然可以使用任何iOS 8模拟器，而不会出现任何问题。
1. 如果您必须使用iOS 9，则可以手动编辑您的apps -Info.plist（在“&lt;应用程序根>/platforms/ios/&lt;应用程序名称>/&lt;应用程序名称>-Info.plist”文件中运行`cordova platform add ios`后找到）以包含以下属性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>有关“App Transport Security”的更多详细信息，请参阅[Apple iOS9预发行文档](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)和此[堆栈溢出讨论](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)的以下部分。

## 在AEM {#developing-mobile-applications-in-aem-1}中开发移动应用程序

* [启动AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [构建移动设备应用程序](/help/mobile/building-app-mobile-phonegap.md)
* [构建应用程序](/help/mobile/phonegap-structure-an-app.md)
* [使用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md)
* [单页应用程序](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI开发应用程序](/help/mobile/phonegap-apps-pg-cli.md)
* [访问设备功能](/help/mobile/phonegap-access-device-features.md)
* [使用Adobe移动分析跟踪应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [将Adobe Analytics添加到移动应用程序](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推送通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile内容个性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [应用的解剖学](/help/mobile/phonegap-apps-arch.md)
* [您的混合应用程序是否已准备就绪，可用于AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM创作Adobe PhoneGap企业版](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
