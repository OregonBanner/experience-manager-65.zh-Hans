---
title: 构建应用程序
seo-title: 构建应用程序
description: 可查看本页以了解如何创建应用程序结构。 本页介绍如何构造模板和组件以及JavaScript和CSS Clientlibs上的信息。
seo-description: 可查看本页以了解如何创建应用程序结构。 本页介绍如何构造模板和组件以及JavaScript和CSS Clientlibs上的信息。
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 构建应用程序{#structure-an-app}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM mobile项目涉及一组不同的内容类型，包括页面、JavaScript和CSS客户端库、可重用的AEM组件、内容同步配置和PhoneGap应用程序Shell内容。 将新的AEM mobile应用程序基于 [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) ，是将所有不同类型的内容放入我们推荐结构中以简化长期可移植性和可维护性的好方法。

## 页面内容 {#page-content}

应用程序的页面应全部位于/content/mobileapps下方，以便AEM Mobile控制台识别这些页面。

![chlimage_1-52](assets/chlimage_1-52.png)

根据AEM惯例，应用程序的第一页应重定向到其子页面之一，该子页面用作应用程序的默认语言（在Geometrixx和Starter Kit案例中均为“en”）。 顶级区域设置页面通常从基础“splash-page”组件(/libs/mobileapps/components/splash-page)继承，该组件负责支持无线内容同步更新安装所必需的初始化(contentInit代码位于/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 模板和组件 {#templates-and-components}

您的应用程序的模板和组件代码应位于/apps/&lt;brand name>/&lt;app name>中。 根据惯例，您应将模板和组件代码放在/apps/&lt;brand name>/&lt;app name>中。 对于已在AEM中使用Site的开发人员来说，此模式应该很熟悉。 通常，在发布实例上，其后跟/apps/默认被锁定为匿名访问。 因此，您的原始JSP代码被隐藏，不会受到潜在攻击者的攻击。

特定于应用程序的模板只能通过使用模板本身的属性节点将其值设置为“ `allowedPaths` /content/mobileapps(/)”来进行配置。&amp;ast;)?&#39; -或者，如果模板仅可用于单个应用程序，则更具体一些。 还可 `allowedParents` 以利 `allowedChildren` 用和属性，根据创建新页面的位置对创作者可以使用哪些模板进行细致的控制。

从头开始创建新的应用程序页面组件时，建议将其属性设置为“mobileapps/components/angular/ng-page”。 `sling:resourceSuperType` 这将设置您的页面，以便创作和呈现为单页应用程序，并允许您覆盖组件可能需要更改的任何。jsp文件。 由于ng-page根本不包含任何UI框架，开发人员通常会最终覆盖（至少）“template.jsp”(从/libs/mobileapps/components/angular/ng-page/template.jsp覆盖)。

希望利用AngularJS的可创作页面组件在/libs/mobileapps/components/angular/ng-component处有一个对等组件，该组件可以以相同的方式覆盖和自定义。 `sling:resourceSuperType`

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

在客户端库方面，开发人员可以使用几个选项将它们放入存储库中。 以下是指导性的，但不是硬要求。

如果您的客户端代码可以独立存在，并且与应用程序的特定组件无关（即可能在其他应用程序中重复使用），我们建议将其存储在/etc/clientlibs/&lt;brand name>/&lt;lib name>中。 另一方面，如果clientlib特定于单个应用程序，则可以将其嵌套为应用程序设计节点的子级；/etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs. 此clientlib的类别不应被其他lib使用，并应根据需要用于嵌入其他lib。 遵循这种模式，开发人员不必在每次将客户端库添加到应用程序时都添加新的内容同步配置，而只需更新应用程序设计clientlib的“embeds”属性。 例如，查看位于/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixx clientlibs-all内容同步配置节点。

如果您的客户端代码与特定组件紧密集成，请将该代码放在嵌套在组件位置下方的客户端库中/apps/中，并将其类别嵌入到应用程序的“design”clientlib中。

## PhoneGap配置 {#phonegap-configuration}

每个AEM Mobile应用程序都包含一个目录，其中存放PhoneGap命令行界面和 [](https://github.com/phonegap/phonegap-cli)[](https://build.phonegap.com/) PhoneGap内部版本使用的配置文件，以将Web内容转换为可运行的应用程序。 在Geometrixx示例中，此目录(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)作为Shell的一部分；由于它仅包含无法通过无线更新的内容（如处理设备API的插件和应用程序本身的配置），因此作出了设计决策。

在此目录中，您还会找到许多 [Cordova挂钩](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) ，这些挂钩可用于安装插件、将资源文件放在其平台特定位置以及作为构建的一部分执行的其他操作。 注意：作为下载每个插件作为构建的一部分的替代方法，您可以按照Kitchen Sink应用程序的模式，将插件源代码 [包含在应用程序项目的其余部分](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 。

## 后续步骤 {#the-next-steps}

了解应用程序结构后，请参阅使 [用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md)。
