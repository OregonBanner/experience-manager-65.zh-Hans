---
title: 构建应用程序
seo-title: Structure an App
description: 请阅读本页以了解如何创建应用程序结构。 本页介绍如何构建模板和组件，以及有关JavaScript和CSS Clientlibs的信息。
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 构建应用程序{#structure-an-app}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM Mobile项目包含一组不同的内容类型，包括页面、JavaScript和CSS客户端库、可重用的AEM组件、内容同步配置和PhoneGap应用程序Shell内容。 将新的AEM Mobile应用程序基于 [入门套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 是将所有不同类型的内容纳入我们推荐结构中的好方法，以便长期实现可移植性和可维护性。

## 页面内容 {#page-content}

应用程序的页面应全部位于/content/mobileapps下方，以便AEM Mobile控制台能够识别这些页面。

![chlimage_1-52](assets/chlimage_1-52.png)

按照AEM的惯例，应用程序的第一页应该是一个重定向，以重定向到其子页面之一，该子页面将用作应用程序的默认语言(在Geometrixx和入门工具包案例中为“en”)。 顶级区域设置页面通常会从基础的“splash-page”组件(/libs/mobileapps/components/splash-page)继承内容，该组件负责支持无线内容同步更新安装所需的初始化(可以在/etc/clientlibs/mobile/content-sync/js/contentInit.js上找到contentInit代码)。

## 模板和组件 {#templates-and-components}

应用程序的模板和组件代码应位于/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 按照惯例，您应将模板和组件代码放置在/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 对于已在AEM中使用Site的开发人员而言，应该熟悉此模式。 默认情况下，随后通常会执行此操作，因为/apps/在发布实例上被锁定为匿名访问。 因此，您的原始JSP代码会被隐藏起来，不会受到潜在攻击者的影响。

特定于应用程序的模板可以配置为仅使用 `allowedPaths` 属性节点，并将其值设置为“/content/mobileapps(/.&amp;ast;)?&#39;  — 或者，如果模板只能用于单个应用程序，则需要更具体的操作。 的 `allowedParents` 和 `allowedChildren` 此外，还可以利用属性以非常精细的方式控制作者可以根据创建新页面的位置来使用哪些模板。

从头开始创建新应用程序页面组件时，建议将 `sling:resourceSuperType` 属性更改为“mobileapps/components/angular/ng-page”。 这将设置您的页面，以便创作和渲染为单页应用程序，并允许您覆盖组件可能需要更改的任何.jsp文件。 由于ng-page根本不包含任何UI框架，因此开发人员通常最终会覆盖（至少）“template.jsp”(从/libs/mobileapps/components/angular/ng-page/template.jsp覆盖)。

希望利用AngularJS的可创作页面组件具有等效项 `sling:resourceSuperType` 组件位于/libs/mobileapps/components/angular/ng-component，可以按相同方式覆盖和自定义组件。

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

在客户端库方面，开发人员可以使用一些选项来将这些库放置在存储库中的位置。 以下模式可供指导，但并不是一个硬要求。

如果您的客户端代码可以独立存放，并且与应用程序的特定组件无关（这意味着它可能会在其他应用程序中重复使用），我们建议将其存储在/etc/clientlibs/中&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. 另一方面，如果clientlib特定于单个应用程序，则可以将其嵌套为应用程序设计节点的子项；/etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs。 此clientlib的类别不应被其他lib使用，而应在必要时用于嵌入其他lib。 按照此模式，开发人员无需在每次将客户端库添加到应用程序时添加新的内容同步配置，而只需更新应用程序设计clientlib的“嵌入”属性即可。 例如，查看位于/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixxclientlibs-all内容同步配置节点。

如果您的客户端代码与特定组件紧密耦合，请将该代码放置在嵌套在/apps/中组件位置下方的客户端库中，并将其类别嵌入到您应用程序的“design”clientlib中。

## PhoneGap配置 {#phonegap-configuration}

每个AEM Mobile应用程序都包含一个目录，其中托管PhoneGap使用的配置文件 [命令行界面](https://github.com/phonegap/phonegap-cli) 和 [PhoneGap内部版本](https://build.phonegap.com/) 将Web内容转换为可运行的应用程序。 例如，在Geometrixx示例中，此目录(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)作为Shell的一部分找到；由于仅包含无法实时更新的内容（例如处理设备API的插件以及应用程序本身的配置），因此做出了设计决策。

在此目录中，您还会找到 [科尔多瓦挂钩](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) 可用于安装插件、将资源文件放置在其平台特定位置以及应在内部版本中执行的其他操作。 注意：作为下载每个插件作为内部版本一部分的替代方法，您可以按照Kitchen Sink应用程序和 [包含插件源代码](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 的其他部分。

## 后续步骤 {#the-next-steps}

了解应用程序结构后，请参阅 [使用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md).
