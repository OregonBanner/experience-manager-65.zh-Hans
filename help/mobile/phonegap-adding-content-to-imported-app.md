---
title: 您的混合应用程序是否已为AEM Mobile做好准备？
seo-title: Is your hybrid app ready for AEM Mobile?
description: 关注此页面以了解有关hrybrid应用程序的信息。 AEM中的应用程序通常分为两个部分。 “shell”和“content”以及此页面提供了有关这些主题的更多分析。
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
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
source-wordcount: '741'
ht-degree: 0%

---

# 您的混合应用程序是否已为AEM Mobile做好准备？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

您已将混合PhoneGap或Cordova应用程序导入AEM，现在该怎么办？ 您可能希望向应用程序添加可创作内容。 要完成此任务，您需要全面了解AEM应用程序的结构。 AEM中的应用程序通常分为两个部分。 “shell”和“content”。 “shell”由应用程序的静态部分组成；例如PhoneGap配置文件、应用程序框架和导航控件。 导入的归档文件的内容将作为Shell的一部分存储。 在本文档的上下文中，shell是由应用程序开发人员构建的混合式PhoneGap应用程序的所有非AEM创作内容。

内容是指由AEM开发人员构建的、在AEM中创作的组件、模板和创作页面。 内容被分类为开发人员内容或创作内容。 组件、设计和页面模板被视为开发内容，因为它们由开发人员构建。 创作内容是使用组件和模板构建的页面。 这些操作通常由设计人员或营销人员完成。

将创作AEM页面添加到混合应用程序需要应用程序开发人员和AEM开发人员之间的协调。 在要添加创作内容的应用程序中的任何位置，应用程序开发人员都需要采用可在AEM中叠加的结构来组织这些页面。 应用程序开发人员必须能够向AEM开发人员提供要将AEM创作内容添加到其中的路径，然后在混合应用程序中提供占位符页面，该页面将在AEM开发人员创作页面内容后替换。

为了使解释更易于遵循，我们将使用AEMMarketing Cloud： AEM Mobile混合引用来解释这些概念。 混合引用应用程序包含一个带有侧菜单的微文页面。

![chlimage_1-76](assets/chlimage_1-76.png)

在本例中，我们将创作应用程序的欢迎页面。 查看源 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). 我们看到，应用程序开发人员定义了欢迎页面，并为应用程序呈现的页面提供了一个模板。 这是应用程序开发人员和AEM开发人员需要协调的地方。 混合引用应用程序中欢迎页面模板的路径被定义为“content/mobileapps/hybrid-reference-app/en/welcome.template.html”。 此路径极其重要，因为AEM开发人员将使用相同的路径在AEM存储库中创作其欢迎页面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合应用程序和AEM创作内容使用相同的路径很重要，因为我们依赖使用内容同步来覆盖内容的功能，从而向混合应用程序添加新页面。 在导入过程中将混合应用程序导入AEM时，将设置内容同步配置。

![chlimage_1-78](assets/chlimage_1-78.png)

当您从应用程序仪表板“下载源”时，将运行这些ContentSync脚本以汇编混合应用程序的存档。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync首先拉入应用程序的“shell”（存储了混合应用程序的所有开发内容的位置），然后拉入应用程序的“content”。 现在，如果“shell”中的页面具有与“content”中相同的路径，则“shell”下的页面将被替换为“content”下的页面。 换句话说，在混合引用应用程序示例中，如果我们在AEM中创建在ContentSync运行时路径与“content/mobileapps/hybrid-reference-app/en/welcome.template.html”相同的页面，则该页面将覆盖作为混合引用应用程序一部分的页面，同时包含该位置AEM中的内容。 叠加由ContentSync负责，因此对于使用应用程序的用户而言，通过AEM创作的内容对应用程序进行的更新看起来无缝无缝，无需重建应用程序。 因此，在运行应用程序时，欢迎页面将显示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
