---
title: 访问设备功能
seo-title: Access Device Features
description: 请阅读本页以了解有关构建访问设备功能的AEM组件的信息。 AEM PhoneGap Kitchen Sink Github存储库为开发人员提供了一个功能强大的AEM应用程序，该应用程序展示了许多核心Cordova API的使用。
seo-description: Follow this page to learn about building AEM components that access device features. The AEM PhoneGap Kitchen Sink Github repository provides developers with a functional AEM app that illustrates the use of a number of core Cordova APIs.
uuid: 1996f017-21d3-4d90-9f55-95c626bc4c60
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 0019e367-8edc-4a23-bfa4-5beda266ace6
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# 访问设备功能{#access-device-features}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

## 构建访问设备功能的AEM组件 {#building-aem-components-that-access-device-features}

的 [AEM PhoneGap Kitchen Sink](https://github.com/blefebvre/aem-phonegap-kitchen-sink) Github存储库为开发人员提供了一个功能强大的AEM应用程序，该应用程序展示了许多核心Cordova API的用法。 当通过PhoneGap CLI在iOS或Android上运行时，应用程序会打开到以下页面，其中包含一个指向其演示的每个设备API的链接：

![chlimage_1-107](assets/chlimage_1-107.png)

每个设备API组件的源代码是 [在Github上提供](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

有关每个API的用法的更多详细信息，我建议您查看 [Cordova插件文档](https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html).

## 后续步骤 {#the-next-steps}

请参阅 [使用Adobe移动分析跟踪应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md).
