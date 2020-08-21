---
title: 创建SCF沙箱
seo-title: 创建SCF沙箱
description: 本教程主要针对AEM新手的开发人员，他们对使用SCF组件感兴趣。  它将逐步介绍如何创建SCF沙箱站点
seo-description: 本教程主要针对AEM新手的开发人员，他们对使用SCF组件感兴趣。  它将逐步介绍如何创建SCF沙箱站点
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---



# 创建SCF沙箱  {#create-an-scf-sandbox}


自AEM 6.1 Communities起，快速创建沙箱的最简单方法是创建社区站点。 See [Getting Started with AEM Communities](getting-started.md).

另一个对开发人员有用的工 [具是“社区组件](components-guide.md)”指南，它允许探索社区组件和功能并快速为它们创建原型。

创建网站的练习对于理解AEM网站的结构（可能包括Communities功能）非常有用，同时还提供了一些简单的页面，用于探 [索与社交组件框架(SCF)的结合](scf.md)。

本教程主要针对AEM新手的开发人员，他们对使用SCF组件感兴趣。 它将逐步介绍如何创建SCF沙箱站点，与 [如何创建功能齐全的Internet网站教程类似](../../help/sites-developing/website.md) ，该网站侧重于站点结构，如导航、徽标、搜索、工具栏和列出子页面。

在创作实例上进行开发，而在发布实例上试验站点最好。

本教程中的步骤有：

* [设置网站结构](setup-website.md)
* [初始沙箱应用程序](initial-app.md)
* [初始沙箱内容](initial-content.md)
* [开发沙箱应用程序](develop-app.md)
* [添加客户端库](add-clientlibs.md)
* [开发沙箱内容](develop-content.md)

>[!CAUTION]
>
>本教程不创建具有使用“社区站点”控制台创建的功 [能的社区站点](sites-console.md)。 例如，本教程不介绍如何设置登录、自注册、社 [交登录](social-login.md)、消息、用户档案等。
>
>如果首选的是简单的社区站点，请遵 [循创建示例页面教程](create-sample-page.md) 。

## 前提条件 {#prerequisites}

本教程假定您安装了一个AEM作者和一个AEM发布实例，该实例具有最 [新版](deploy-communities.md#latest-releases) Communities。

下面是刚接触AEM平台的开发人员的一些有用链接：

* [入门](../../help/sites-deploying/deploy.md#getting-started):部署AEM实例。

   * [基础知识](../../help/sites-developing/the-basics.md):面向网站和功能的开发人员。
   * [创作的最初步骤](../../help/sites-authoring/first-steps.md):创作页面内容。

## 使用CRXDE Lite开发环境 {#using-crxde-lite-development-environment}

AEM开发人员将大部分时间用在创作 [实例的](../../help/sites-developing/developing-with-crxde-lite.md) CRXDE Lite开发环境中。 CRXDE Lite提供对CRX存储库的较少受限访问。 经典UI工具和触屏优化UI控制台提供对CRX存储库特定部分的更结构化的访问。

使用管理权限登录后，可通过多种方式访问CRXDE Lite:

1. 从全局导航中，选择导航 **[!UICONTROL 工具>CRXDE Lite]**。

   ![crxde-lite](assets/tools-crxde.png)

2. 从经典 [UI欢迎页面](http://localhost:4502/welcome.html)，向下滚动并单 **[!UICONTROL 击右面]** 板中的“CRXDE Lite”。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接浏览 `CRXDE Lite`: `<server>:<port>/crx/de`

   例如，在本地作者实例上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

要使用CRXDE Lite，您必须使用开发人员或管理员权限登录。 对于默认的localhost实例，您可以使用

* `username: admin`
* `password: admin`


**请注意** ，此登录将超时，您需要使用CRXDe Lite工具栏右端的下拉菜单定期重新登录。

如果未登录，您将无法导航JCR存储库或执行任何编辑／保存操作。

***如果有疑问，请重新登录！***

![重新登录](assets/relogin.png)
