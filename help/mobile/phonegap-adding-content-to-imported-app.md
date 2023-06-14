---
title: 您的混合应用程序是否已为AEM Mobile做好准备？
description: 了解混合应用程序。 Experience Manager中的应用程序通常分为两个部分。 “shell”和“content”以及此页面提供了有关这些主题的更多分析。
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# 您的混合应用程序是否已为Adobe Experience Manager Mobile做好准备？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

您已将混合PhoneGap或Cordova应用程序导入AEM，现在该怎么办？ 您可能希望向应用程序添加可创作内容。 要完成此任务，您需要全面了解AEM应用程序的结构。 AEM中的应用程序通常分为两个部分。 “shell”和“content”。 “shell”包含应用程序的静态部分；例如PhoneGap配置文件、应用程序框架和导航控件。 导入的归档文件的内容将作为Shell的一部分存储。 在本文档的上下文中，shell是由应用程序开发人员构建的混合式PhoneGap应用程序的所有非AEM创作内容。

内容是指由AEM开发人员构建的、在AEM中创作的组件、模板和创作页面。 内容被分类为开发人员内容或创作内容。 组件、设计和页面模板被视为开发内容，因为它们由开发人员构建。 创作内容是使用组件和模板构建的页面。 这些页面通常由设计人员或营销人员完成。

将创作AEM页面添加到混合应用程序需要应用程序开发人员和AEM开发人员之间的协调。 在要添加创作内容的应用程序中的任何位置，应用程序开发人员都必须采用可在Experience Manager中叠加的结构来组织这些页面。 应用程序开发人员必须能够向Experience Manager开发人员提供将Experience Manager创作的内容添加到其中的路径。 然后，在混合应用程序中提供一个占位符页面，该页面将在Experience Manager开发人员创作页面内容后替换。

为了使解释更易于遵循，正在使用AEMExperience Cloud： AEM Mobile混合引用来解释这些概念。 混合引用应用程序包含带有侧菜单的欢迎页面。

![chlimage_1-76](assets/chlimage_1-76.png)

在本例中，将创作应用程序的欢迎页面。 查看源 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). 请注意，应用程序开发人员已定义欢迎页面，并为应用程序呈现的页面提供了一个模板。 应用程序开发人员和AEM开发人员必须在此页面上进行协调。 混合引用应用程序中欢迎页面模板的路径被定义为“content/mobileapps/hybrid-reference-app/en/welcome.template.html”。 此路径很重要，因为AEM开发人员将使用相同的路径在AEM存储库中创作其欢迎页面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合应用程序和AEM创作内容使用相同的路径很重要，因为它依赖于使用内容同步叠加内容的能力，从而向混合应用程序添加新页面。 在导入过程中，将混合应用程序导入AEM时，会设置内容同步配置。

![chlimage_1-78](assets/chlimage_1-78.png)

当您从应用程序仪表板“下载源”时，将运行这些ContentSync脚本以汇编混合应用程序的存档。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync首先拉入应用程序的“外壳”，该外壳是存储混合应用程序的所有应用程序开发内容的地方。 然后，它会拉入应用程序的“内容”。 现在，如果“shell”中的页面具有与“content”中相同的路径，则“shell”下的页面将被“content”下的页面（替换）。 因此，在混合引用应用程序示例中，如果在AEM中创建的某个页面具有与“content/mobileapps/hybrid-reference-app/en/welcome.template.html”相同的路径，则当ContentSync运行时，它会覆盖作为混合引用应用程序一部分的页面。 它会将其与AEM中位于该位置的任何内容叠加。 叠加由ContentSync处理，因此对于使用应用程序的用户而言，使用AEM创作内容对应用程序进行更新看起来无缝无缝，无需重建应用程序。 因此，在运行应用程序时，欢迎页面如下所示：

![chlimage_1-80](assets/chlimage_1-80.png)
