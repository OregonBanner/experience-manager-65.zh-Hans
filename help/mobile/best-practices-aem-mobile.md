---
title: 最佳实践
seo-title: 最佳实践
description: 请阅读本页以了解最佳实践和准则，这些实践和准则将帮助那些希望构建移动设备应用程序模板和组件的经验丰富的AEM网站开发人员。
seo-description: 请阅读本页以了解最佳实践和准则，这些实践和准则将帮助那些希望构建移动设备应用程序模板和组件的经验丰富的AEM网站开发人员。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# 最佳实践 {#best-practices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

构建AEM Mobile On-demand Services应用程序与直接在Cordova（或PhoneGap）Shell中运行的应用程序不同。 开发人员应该熟悉：

* 开箱即用支持的插件以及特定于AEM Mobile的插件。

>[!NOTE]
>
>要深入了解插件，请参阅以下资源：
>
>* [在AEM Mobile中使用Cordova插件](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用特定于AEM Mobile的启用Cordova的插件](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* 使用插件功能的模板的编写方式应当使其仍可在浏览器中创作，而不应存在插件桥。

   * 例如，请确保在尝试访问插件的API之前等待&#x200B;*deviceready*&#x200B;函数。

## 面向AEM开发人员的准则{#guidelines-for-aem-developers}

以下准则将帮助那些希望构建移动设备应用程序模板和组件的经验丰富的AEM网站开发人员：

**构建AEM站点模板以鼓励重复使用和可扩展性**

* 与单个整体文件相比，需要多个组件脚本文件

   * 提供了许多空的扩展点，如&#x200B;*customheaderlibs.html*&#x200B;和&#x200B;*customfooterlibs.html*，它们允许开发人员在尽可能少复制核心代码的同时更改页面模板
   * 然后，可以通过Sling的&#x200B;*sling:resourceSuperType*&#x200B;机制来扩展和自定义模板

* 与JSP相比，使用Sightly/HTL作为模板语言更好

   * 使用它可以将代码与标记分离，在XSS保护中内置选件，并且具有更为熟悉的语法

**优化设备内性能**

* 文章特定脚本和样式表应使用dps-article contentsync模板包含在文章有效负载中
* 由多篇文章共享的脚本和样式表应通过dps-HTMLResourcescontentsync模板包含在共享资源中
* 请勿引用任何呈现阻塞的外部脚本

>[!NOTE]
>
>您可以在此处](https://developers.google.com/speed/docs/insights/BlockingJS)详细了解有关渲染阻止外部脚本的[。

**与特定于Web的库相比，首选使用特定于应用程序的客户端JS和CSS库**

* 为避免在jQuery Mobile等库中开销，以处理大量设备和浏览器
* 当模板在应用程序的Web视图中运行时，您可以控制应用程序将支持的平台和版本，并了解将会提供JavaScript支持。 例如，与jQuery Mobile和Onsen UI相比，更喜欢Ionic（可能只是CSS）和Bootstrap。

>[!NOTE]
>
>要深入了解jQuery移动设备，请单击[此处](https://jquerymobile.com/browser-support/1.4/)。

**相对于全栈，首选微库**

* 您的文章所依赖的每个库都会减慢将内容放到设备玻璃上所需的时间。 如果使用新Webview渲染每篇文章，则速度会更慢，因此必须重新初始化每个库
* 如果您的文章未作为SPA（单页应用程序）构建，则可能不需要包含完整堆栈库，如Angular
* 希望使用较小的单用途库来帮助添加页面所需的交互性，例如[Fastclick](https://github.com/ftlabs/fastclick)或[Velocity.js](https://velocityjs.org)

**最大限度地减小文章有效负载的大小**

* 以合理的分辨率使用尽可能小的资产，以有效地覆盖您将支持的最大视区
* 在图像上使用诸如&#x200B;*ImageOptim*&#x200B;之类的工具来删除任何多余的元数据

## 提前{#getting-ahead}

要进一步了解其他两个角色和职责，请参阅以下资源：

* [管理员](/help/mobile/aem-mobile.md)
* [作者](/help/mobile/aem-mobile-on-demand.md)
