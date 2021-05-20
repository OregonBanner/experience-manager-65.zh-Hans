---
title: 创建SCF沙盒
seo-title: 创建SCF沙盒
description: 本教程主要面向对使用SCF组件感兴趣的AEM新开发人员。  它将指导创建SCF沙盒站点
seo-description: 本教程主要面向对使用SCF组件感兴趣的AEM新开发人员。  它将指导创建SCF沙盒站点
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 创建SCF沙盒{#create-an-scf-sandbox}


自AEM 6.1 Communities起，快速创建沙盒的最简单方法是创建社区站点。 请参阅[AEM Communities快速入门](getting-started.md)。

对开发人员而言，另一个有用的工具是[社区组件指南](components-guide.md)，该指南允许探索社区组件和功能并快速为其制作原型。

创建网站的练习对于了解AEM网站的结构（可能包括Communities功能）非常有用，同时也提供了一些简单的页面，可以在这些页面上探索与[社交组件框架(SCF)](scf.md)一起使用。

本教程主要面向对使用SCF组件感兴趣的AEM新开发人员。 它将介绍如何创建SCF沙盒网站，与[如何创建功能完备的Internet网站](../../help/sites-developing/website.md)的教程类似，该教程重点介绍网站结构，如导航、徽标、搜索、工具栏和列出子页面。

开发过程在创作实例中进行，而在发布实例中尝试网站最好。

本教程中的步骤如下：

* [设置网站结构](setup-website.md)
* [初始沙盒应用程序](initial-app.md)
* [初始沙盒内容](initial-content.md)
* [开发沙盒应用程序](develop-app.md)
* [添加Clientlibs](add-clientlibs.md)
* [开发沙盒内容](develop-content.md)

>[!CAUTION]
>
>本教程不会使用使用[社区站点控制台](sites-console.md)创建的功能创建社区站点。 例如，本教程未介绍如何设置登录、自注册、[社交登录](social-login.md)、消息传送、用户档案等。
>
>如果首选简单的社区站点，请阅读[创建示例页面](create-sample-page.md)教程。

## 前提条件 {#prerequisites}

本教程假定您安装了一个AEM作者和一个AEM发布实例，其中[最新版本](deploy-communities.md#latest-releases)的Communities。

以下是一些对初次使用AEM平台的开发人员有用的链接：

* [快速入门](../../help/sites-deploying/deploy.md#getting-started):用于部署AEM实例。

   * [基础知识](../../help/sites-developing/the-basics.md):适用于网站和功能的开发人员。
   * [作者的首要步骤](../../help/sites-authoring/first-steps.md):，以创作页面内容。

## 使用CRXDE Lite开发环境{#using-crxde-lite-development-environment}

AEM开发人员在[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)开发环境中花费的大部分时间都花在创作实例上。 CRXDE Lite提供了对CRX存储库的较少限制的访问。 经典UI工具和触屏UI控制台提供了对CRX存储库特定部分的更结构化的访问。

使用管理权限登录后，可通过多种方式访问CRXDE Lite:

1. 从全局导航中，选择导航&#x200B;**[!UICONTROL 工具>CRXDE Lite]**。

   ![crxde-lite](assets/tools-crxde.png)

2. 从[经典UI欢迎页面](http://localhost:4502/welcome.html)中，向下滚动，然后单击右侧面板中的&#x200B;**[!UICONTROL CRXDE Lite]**。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接浏览到`CRXDE Lite`:`<server>:<port>/crx/de`

   例如，在本地创作实例上：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

要使用CRXDE Lite，您必须使用开发人员或管理员权限登录。 对于默认的localhost实例，您可以使用

* `username: admin`
* `password: admin`


**请注** 意，此登录将超时，您需要使用CRXDe Lite工具栏右端的下拉菜单定期重新登录。

如果未登录，您将无法导航JCR存储库或执行任何编辑/保存操作。

***如有疑问，请重新登录！***

![重新登录](assets/relogin.png)
