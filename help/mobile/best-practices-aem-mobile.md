---
title: AEM Mobile On-demand Services的最佳实践
description: 了解最佳实践和指南，帮助符合条件的Adobe Experience Manager (AEM)开发人员访问要构建移动应用程序模板和组件的网站。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 最佳实践 {#best-practices}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

构建AEM Mobile On-demand Services应用程序与构建直接在Cordova（或PhoneGap）外壳中运行的应用程序不同。 开发人员应该熟悉：

* 现成支持的插件和特定于Adobe Experience Manager (AEM) Mobile的插件。

>[!NOTE]
>
>要深入了解插件，请参阅以下资源：
>
>* [在AEM Mobile中使用Cordova插件](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用特定于AEM Mobile且启用了Cordova的插件](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* 使用插件功能的模板应以这样的方式编写，即仍然可以在浏览器中创作这些模板，而无需使用插件桥。

   * 例如，确保等待 *deviceready* 函数。

## AEM开发人员指南 {#guidelines-for-aem-developers}

以下准则可帮助符合条件的AEM开发人员创建要构建移动应用程序模板和组件的网站：

**构建AEM站点模板以鼓励重复使用和可扩展性**

* 与单个整体脚本文件相比，更喜欢多个组件脚本文件

   * 提供了多个空扩展点，例如 *customheaderlibs.html* 和 *customfooterlibs.html*，这允许开发人员更改页面模板，同时尽可能少地复制核心代码
   * 随后，可通过Sling的 *sling：resourceSuperType* 机理

* 与将JSP作为模板语言相比，首选Sightly/HTL

   * 使用此选项鼓励将代码与标记分离，提供内置的XSS保护，并具有更熟悉的语法

**优化设备上性能**

* 应使用dps-article contentsync模板将特定于文章的脚本和样式表包含在文章有效负荷中
* 通过dps-HTMLResources contentsync模板，由多个文章共享的脚本和样式表应包含在共享资源中
* 请勿引用任何渲染阻止的外部脚本

>[!NOTE]
>
>您可以详细了解渲染阻止外部脚本 [此处](https://developers.google.com/speed/docs/insights/BlockingJS).

**与特定于Web的相比，更喜欢特定于应用程序的客户端JS和CSS库**

* 避免jQuery Mobile等库处理大量设备和浏览器的开销
* 当模板在应用程序的Webview中运行时，您可以控制应用程序将支持的平台和版本，并了解是否支持JavaScript。 例如，与jQuery Mobile和Onsen UI相比，偏好Ionic（只是CSS）与Bootstrap。

>[!NOTE]
>
>要更深入地了解jQuery移动设备，请单击 [此处](https://jquerymobile.com/browser-support/1.4/).

**与全栈库相比，更倾向于使用微库**

* 将内容放到设备玻璃上的时间被您的文章所依赖的每个库所减慢。 使用新的Web视图呈现每篇文章时，这种减速会更加严重，因此必须从头开始再次初始化每个库
* 如果您的文章未构建为SPA（单页应用程序），则可能不需要包含Angular等全栈库
* 首选更小的单用途库，这些库可帮助添加页面所需的交互性，例如 [Fastclick](https://github.com/ftlabs/fastclick) 或 [Velocity.js](https://velocityjs.org)

**最小化文章有效负载的大小**

* 使用尽可能最小的资产，以便以合理的分辨率有效地覆盖您支持的最大视区
* 使用工具，如 *ImageOptim* 以删除任何多余的元数据

## 快速入门 {#getting-ahead}

要详细了解其他两个角色和职责，请参阅以下资源：

* [管理员](/help/mobile/aem-mobile.md)
* [创作](/help/mobile/aem-mobile-on-demand.md)
