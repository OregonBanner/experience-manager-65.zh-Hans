---
title: 最佳实践
seo-title: 最佳实践
description: 可查看本页以了解最佳实践和准则，这些准则和准则将帮助有经验的AEM开发人员构建移动应用程序模板和组件的站点。
seo-description: 可查看本页以了解最佳实践和准则，这些准则和准则将帮助有经验的AEM开发人员构建移动应用程序模板和组件的站点。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 最佳实践 {#best-practices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

构建AEM Mobile On-Demand services应用程序与构建直接在Cordova（或PhoneGap）Shell中运行的应用程序不同。 开发人员应熟悉：

* 现成支持的插件以及特定于AEM mobile的插件。

>[!NOTE]
>
>要详细了解插件，请参阅以下资源：
>
>* [在AEM mobile中使用Cordova插件](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用特定于AEM Mobile的支持Cordova的插件](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>



* 使用插件功能的模板的编写方式应该是，在浏览器中仍可创作，而不存在插件桥接器。

   * 例如，请确保在尝试访问插 *件的API之前* ，等待deviceready函数。

## AEM开发人员准则 {#guidelines-for-aem-developers}

以下准则将帮助希望构建移动应用程序模板和组件的经验丰富的站点AEM开发人员：

**构建AEM站点模板以鼓励重复使用和可扩展性**

* 比单块脚本文件更喜欢多个组件脚本文件

   * 提供了许多空扩展点，如 *customheaderlibs.html* 和 *customfooterlibs.html*，这允许开发人员在尽可能少复制核心代码的同时更改页面模板
   * 然后，可以通过Sling的 *sling:resourceSuperType机制扩展和自定义模板* 。

* 相比JSP，更喜欢Sightly/HTL作为模板语言

   * 使用它可以将代码与标记分离，在XSS保护中内置选件，并且有更熟悉的语法

**优化设备性能**

* 文章有效负荷中应使用dps-article contentsync模板包含文章特定脚本和样式表
* 由多篇文章共享的脚本和样式表应通过dps-HTMLResources contentsync模板包含在共享资源中
* 不引用任何渲染阻止的外部脚本

>[!NOTE]
>
>您可以在此处详细了解关于渲染阻止外部脚本的 [信息](https://developers.google.com/speed/docs/insights/BlockingJS)。

**优先使用特定于应用程序的客户端JS和CSS库，而不是特定于Web的库**

* 为避免jQuery mobile等库的开销，以处理大量设备和浏览器
* 当模板在应用程序的Web视图中运行时，您可以控制应用程序将支持的平台和版本以及JavaScript支持将存在的知识。 例如，比起Bootstrap，更喜欢Ionic（也许只是CSS）而不是jQuery Mobile和Onsen UI。

>[!NOTE]
>
>要详细了解jQuery移动，请单击此 [处](https://jquerymobile.com/browser-support/1.4/)。

**优先使用微型库，而不是全堆栈**

* 将您的内容放到设备的玻璃上所需的时间将因您的文章所依赖的每个库而减少。 当使用新的Web视图渲染每篇文章时，这种速度会更慢，因此必须从头开始重新初始化每个库
* 如果您的文章未作为SPA（单页应用程序）构建，则可能不需要包括像Angular这样的完整堆栈库
* 希望使用较小的单用途库帮助添加页面所需的交互性，如 [Fastclick](https://github.com/ftlabs/fastclick)[或Velocity.js](https://velocityjs.org)

**将文章有效负荷的大小降至最低**

* 以合理的分辨率使用尽可能小的资源，以有效覆盖您将支持的最大视区
* 使用图像上的 *ImageOptim* 等工具删除多余的元数据

## 抢先一步 {#getting-ahead}

要进一步了解其他两个角色和职责，请参阅以下资源：

* [管理员](/help/mobile/aem-mobile.md)
* [创作](/help/mobile/aem-mobile-on-demand.md)
