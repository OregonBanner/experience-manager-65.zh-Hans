---
title: 最佳实践
seo-title: 最佳实践
description: 可查看本页以了解最佳实践和指南，这些实践和指南将帮助需要构建移动应用程序模板和组件的有经验的AEM开发人员构建网站。
seo-description: 可查看本页以了解最佳实践和指南，这些实践和指南将帮助需要构建移动应用程序模板和组件的有经验的AEM开发人员构建网站。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# 最佳实践 {#best-practices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

构建AEM Mobile On-demand Services应用程序与构建直接在Cordova（或PhoneGap）外壳程序中运行的应用程序不同。 开发人员应熟悉：

* 开箱即用支持的插件以及特定于AEM Mobile的插件。

>[!NOTE]
>
>要深入了解插件，请参阅以下资源：
>
>* [使用AEM Mobile的Cordova插件](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用特定于AEM Mobile的支持Cordova的插件](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* 使用插件功能的模板的编写方式应当使其仍可在浏览器中授权，而不必存在插件桥。

   * 例如，请确保在尝试访问插件的API之前等待&#x200B;*deviceready*&#x200B;函数。

## AEM开发人员{#guidelines-for-aem-developers}指南

以下准则将帮助需要构建移动应用程序模板和组件的有经验的AEM站点开发人员：

**构建AEM站点模板以鼓励重复使用和可扩展性**

* 比单个单片脚本文件更喜欢多个组件脚本文件

   * 提供了许多空扩展点，如&#x200B;*customheaderlibs.html*&#x200B;和&#x200B;*customfooterlibs.html*，它们允许开发人员在复制尽可能少的核心代码的同时更改页面模板
   * 然后，可以通过Sling的&#x200B;*sling:resourceSuperType*&#x200B;机制扩展和自定义模板

* 将Sightly/HTL作为模板语言优先于JSP

   * 使用它可以将代码与标记分离，在XSS保护中构建的优惠具有更熟悉的语法

**优化设备性能**

* 应使用dps-article contentsync模板将文章特定脚本和样式表包含在文章有效负荷中
* 由多篇文章共享的脚本和样式表应通过dps-HTMLResources contentsync模板包括在共享资源中
* 不引用任何渲染阻止的外部脚本

>[!NOTE]
>
>您可以在此处](https://developers.google.com/speed/docs/insights/BlockingJS)详细了解渲染阻止外部脚本[。

**与Web特定的JS和CSS库相比，首选应用程序特定的客户端JS和CSS库**

* 避免jQuery Mobile等库的开销以处理大量设备和浏览器
* 当模板在应用程序的Web视图中运行时，您可以控制应用程序将支持的平台和版本以及JavaScript支持将存在的知识。 例如，比起jQuery Mobile和Onsen UI，更喜欢Ion（可能只是CSS），而不是Bootstrap。

>[!NOTE]
>
>要详细了解jQuery Mobile，请单击[此处](https://jquerymobile.com/browser-support/1.4/)。

**优先使用微型库，而不是全堆栈**

* 您的文章所依赖的每个库都会减慢将内容放到设备玻璃上所需的时间。 当使用新的Web视图渲染每篇文章时，速度会进一步放缓，因此必须从头开始重新初始化每个库
* 如果您的文章不是作为SPA（单页应用程序）构建的，则可能不需要包括像Angular这样的完整堆栈库
* 希望使用较小的单用途库来帮助添加页面所需的交互性，如[Fastclick](https://github.com/ftlabs/fastclick)或[Velocity.js](https://velocityjs.org)

**将文章有效负荷的大小降至最低**

* 以合理的分辨率使用尽可能小的资源，以有效覆盖您将支持的最大视区
* 在图像上使用&#x200B;*ImageOptim*&#x200B;等工具删除任何多余的元数据

## 领先{#getting-ahead}

要进一步了解其他两个角色和职责，请参阅以下资源：

* [管理员](/help/mobile/aem-mobile.md)
* [创作](/help/mobile/aem-mobile-on-demand.md)
