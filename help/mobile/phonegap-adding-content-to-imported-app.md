---
title: 您的混合应用程序是否已准备就绪，可用于AEM Mobile?
seo-title: 您的混合应用程序是否已准备就绪，可用于AEM Mobile?
description: 请阅读本页以了解有关混合应用程序的信息。 AEM中的应用程序通常分为两部分。 “shell”和“内容”以及本页对这些主题提供了更多分析。
seo-description: 请阅读本页以了解有关混合应用程序的信息。 AEM中的应用程序通常分为两部分。 “shell”和“内容”以及本页对这些主题提供了更多分析。
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# 您的混合应用程序是否已准备好用于AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

因此，您已将Hybrid PhoneGap或Cordova应用程序导入AEM，现在怎么办？ 您可能希望向应用程序添加可创作内容。 要完成此任务，您需要对AEM应用程序的结构有一般的了解。 AEM中的应用程序通常分为两部分。 “shell”和“内容”。 “shell”由应用程序的静态部分组成；例如PhoneGap配置文件、应用程序框架和导航控件。 导入的存档内容将作为Shell的一部分进行存储。 在本文档的上下文中，shell是由应用程序开发人员构建的混合PhoneGap应用程序的所有非AEM创作内容。

内容是指在AEM中由AEM开发人员构建的创作组件、模板和创作的页面。 内容被分类为开发人员内容或创作内容。 组件、设计和页面模板被视为开发内容，因为它们是由开发人员构建的。 创作内容是使用组件和模板构建的页面。 这些操作通常由设计人员或营销人员完成。

将创作的AEM页面添加到混合应用程序时，需要应用程序开发人员与AEM开发人员之间进行协调。 在应用程序中要添加创作内容的任意位置，应用程序开发人员都需要按照可以在AEM中覆盖的结构来组织这些页面。 应用程序开发人员必须能够向AEM开发人员提供添加AEM创作内容的路径，然后在混合应用程序中提供占位符页面，该占位符页面将在AEM开发人员创作页面内容后替换。

为了更便于遵循，我们将使用AEMMarketing Cloud:AEM Mobile混合参考，以说明相关概念。 混合引用应用程序包含一个带侧面菜单的欢迎页面。

![chlimage_1-76](assets/chlimage_1-76.png)

在本例中，我们将创作应用程序的欢迎页面。 查看源[https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75)。 我们看到应用程序开发人员定义了一个欢迎页面并为应用程序呈现的页面提供了模板。 应用程序开发人员和AEM开发人员需要在此处进行协调。 混合引用应用程序中欢迎页面模板的路径被定义为“content/mobileapps/hybrid-reference-app/en/welcome.template.html”。 此路径非常重要，因为AEM开发人员将使用相同的路径在AEM存储库中创作其欢迎页面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合应用程序和AEM创作内容使用相同路径很重要，因为我们依赖使用内容同步来叠加内容的功能来向混合应用程序添加新页面。 将混合应用程序导入AEM作为导入流程的一部分时，将设置内容同步配置。

![chlimage_1-78](assets/chlimage_1-78.png)

当您从应用程序功能板“下载源”时，将运行这些ContentSync脚本以组合混合应用程序的存档。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync先提取应用程序的“shell”，然后提取应用程序的“内容”。 现在，如果“shell”中的页面与“内容”中的页面具有相同的路径，则“shell”下的页面将被“content”下的页面（替换）。 换言之，在混合引用应用程序示例中，如果我们在AEM中创建的页面在ContentSync运行时具有与“content/mobileapps/hybrid-reference-app/en/welcome.template.html”相同的路径，则它将用AEM中该位置的任何内容来覆盖混合引用应用程序一部分的页面。 叠加图由ContentSync负责，因此对于使用应用程序的人员，对于使用AEM创作内容的应用程序的更新将看起来无缝，并且不需要重新构建应用程序。 因此，运行应用程序时，欢迎页面将如下所示：

![chlimage_1-80](assets/chlimage_1-80.png)
