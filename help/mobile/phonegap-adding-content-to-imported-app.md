---
title: 你的混合应用准备好迎接AEM Mobile了吗？
seo-title: 你的混合应用准备好迎接AEM Mobile了吗？
description: 可查看本页以了解混合应用程序。 AEM中的应用程序通常分为两部分。 “shell”和“content”以及本页可更深入地了解这些主题。
seo-description: 可查看本页以了解混合应用程序。 AEM中的应用程序通常分为两部分。 “shell”和“content”以及本页可更深入地了解这些主题。
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---


# 您的混合应用程序准备好迎接AEM Mobile了吗？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

因此，您已将Hybrid PhoneGap或Cordova应用程序导入AEM，现在怎么办？ 您可能希望向应用程序添加可创作内容。 要完成此任务，您需要对AEM应用程序的结构有全面的了解。 AEM中的应用程序通常分为两部分。 “shell”和“content”。 “外壳”由应用的静态部分组成；如PhoneGap配置文件、应用程序框架和导航控件。 导入的存档内容会作为外壳程序的一部分进行存储。 在此文档中，shell是应用程序开发人员构建的Hybrid PhoneGap应用程序的所有非AEM创作内容。

内容是指在AEM中由AEM开发人员构建的创作的组件、模板和创作的页面。 内容被分类为开发人员内容或创作内容。 组件、设计和页面模板由开发人员构建，因此被视为开发内容。 创作内容是使用组件和模板构建的页面。 这些操作通常由设计人员或营销人员完成。

将创作的AEM页面添加到您的混合应用程序需要应用程序开发人员与AEM开发人员之间的协调。 在应用程序中要添加创作内容的任意位置，应用程序开发人员需要以可在AEM中覆盖的结构组织这些页面。 应用程序开发人员必须能够向AEM开发人员提供添加AEM创作内容的路径，然后在混合应用程序中提供占位符页，该占位符页将在AEM开发人员创作页面内容后被替换。

为了使解释更易于遵循，我们将使用AEMMarketing Cloud:AEM Mobile混合参考，以解释这些概念。 Hybrid Reference应用程序包含带侧面菜单的欢迎页面。

![chlimage_1-76](assets/chlimage_1-76.png)

在此示例中，我们将创作应用程序的欢迎页面。 查看源[https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75)。 我们看到应用程序开发人员已定义欢迎页面并为应用程序呈现的页面提供模板。 这是应用程序开发人员和AEM开发人员需要协调的地方。 混合引用应用程序中欢迎页面模板的路径定义为“content/mobileapps/hybrid-reference-app/en/welcome.template.html”。 此路径非常重要，因为AEM开发人员将使用相同的路径在AEM存储库中创作其欢迎页面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合应用程序和AEM创作的内容使用相同的路径很重要，因为我们依靠使用内容同步功能叠加内容来向混合应用程序添加新页面。 将混合应用程序作为导入过程的一部分导入AEM时，将设置内容同步配置。

![chlimage_1-78](assets/chlimage_1-78.png)

当您从应用程序“下载源”仪表板时，将运行这些ContentSync脚本以组合混合应用程序的存档。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync首先引入应用程序的“shell”，即存储所有应用程序开发的Hybrid应用程序内容的位置，然后引入应用程序的“内容”。 现在，如果“shell”中有与“content”中路径相同的页面，则“shell”下的页面将被“content”下的页面（替换）。 换言之，如果我们在AEM中创建的页面与ContentSync运行时的“content/mobileapps/hybrid-reference-app/en/welcome.template.html”路径相同，则该页面会将作为Hybrid Reference应用程序一部分的页面与AEM中该位置的任何内容相叠加。 叠加由ContentSync负责，因此对于使用应用程序的人员，对包含AEM创作内容的应用程序的更新将看起来无缝，并且不需要重新构建应用程序。 因此，运行应用程序时欢迎页面将显示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
