---
title: 在AEM中开发Mobile应用程序
seo-title: 在AEM中开发Mobile应用程序
description: 可查看本页，以开始使用Adobe phoneGap Enterprise在AEM中开发移动应用程序。
seo-description: 可查看本页，以开始使用Adobe phoneGap Enterprise在AEM中开发移动应用程序。
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在AEM中开发Mobile应用程序 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM利用Adobe phoneGap和Adobe Publishing Solutions，使您能够创建和管理内容丰富的和基于实用程序的跨平台移动应用程序：

* 在一个位置管理所有公司的移动应用程序。
* 在开发和暂存环境中审核应用程序，而无需复杂的配置文件以及构建和上传用于共享的应用程序所需的额外工作。
* 使用AEM创作环境为您的应用程序创建和管理丰富内容。
* 将HTML5与Adobe phoneGap结合使用，以利用设备本机功能创建丰富的体验。
* 通过Cordova webViews将HTML5 web视图引入新的或预先存 **在的本** 机应用程序。
* 跨所有交付渠道（包括Web、移动Web、移动App和印刷）创建、策划和共享丰富的多媒体内容。

AEM与Adobe **[PhoneGap build服务集成](https://build.phonegap.com/)**，可简化应用程序构建和部署过程。

**Adobe contentSync使用户能够轻松地将Over-the-Air(OTA)页面和内容更新下载到其设备，而无需重新安装应用程序或从appStore、Google Play或其他应用程序源下载。**

**Adobe Analytics已完全集成到AEM应用程序中** ，允许详细跟踪分发、地理位置、操作系统、设备、点击流、iBeacon跟踪等。

## 创建应用程序 {#creating-apps}

开发人员可以使用 [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) ，以及https://github.com/adobe-marketing-cloud-apps中的其他资源，使用 [](https://github.com/adobe-marketing-cloud-apps) PhoneGap引导AEM应用程序，包括运行Cordova Webview的参考本机应用程序。

Starter Kit Git存储库的自述文件包含有关使用启动工具包的教程：

* 自定义品牌
* 制作构建和部署目标示例
* 源控制存储库配置
* 安装并部署到本地或远程AEM实例
* 从AEM卸载

>[!NOTE]
>
>GitHub和“厨房——水槽”源上 [可找到其他参考实施源](https://github.com/adobe-marketing-cloud-apps) ，包括实验室 [](https://github.com/blefebvre/aem-phonegap-kitchen-sink)。

## 为IOS 9和HTTP主机进行开发 {#developing-for-ios-and-http-hosts}

IOS开发人员应注意到在iOS 9上运行的Cordova应用程序存在一个未解决的问题。 此问题会阻止向不安全的主机(如http://localhost:4502 **)发出请求。 此问题将在即将发布的cordova-ios版本（由Cordova CLI使用）中得到解决，但同时有两种解决办法：

1. 作为立即的解决方法，您仍可以无问题地使用任何iOS 8模拟器。
1. 如果必须使用iOS 9，则可以手动编辑您的应用程序-Info.plist（在“&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist”文件中运行后找到），以包含以下属性： `cordova platform add ios`

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>有关“App Transport Security”的详细信息，请参阅 [Apple的iOS9预发行文档的下一节](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) ，以及此“堆栈溢 [出”讨论](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)。

## 在AEM中开发Mobile应用程序 {#developing-mobile-applications-in-aem-1}

* [启动AEM phoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [构建移动应用程序](/help/mobile/building-app-mobile-phonegap.md)
* [构建应用程序](/help/mobile/phonegap-structure-an-app.md)
* [使用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md)
* [单页应用程序](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI开发应用程序](/help/mobile/phonegap-apps-pg-cli.md)
* [访问设备功能](/help/mobile/phonegap-access-device-features.md)
* [使用Adobe Mobile Analytics跟踪应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [将Adobe Analytics添加到您的移动应用程序](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推送通知](/help/mobile/phonegap-push-notifications.md)
* [AEM mobile内容个性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [应用程序剖析](/help/mobile/phonegap-apps-arch.md)
* [您的混合应用程序是否已准备好用于AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行创作](/help/mobile/phonegap.md)
* [通过AEM管理Adobe phoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
