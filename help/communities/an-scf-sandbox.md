---
title: 创建SCF沙箱
seo-title: 创建SCF沙箱
description: 本教程主要面向对使用SCF组件感兴趣的AEM新手的开发人员。  它将逐步介绍如何创建SCF沙箱站点
seo-description: 本教程主要面向对使用SCF组件感兴趣的AEM新手的开发人员。  它将逐步介绍如何创建SCF沙箱站点
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---



# 创建SCF沙箱 {#create-an-scf-sandbox}


自AEM 6.1 Communities起，快速创建沙箱的最简单方法是创建社区站点。 See [Getting Started with AEM Communities](getting-started.md).

对开发人员来说，另一个有用的工具是“ [社区组件”指南](components-guide.md)，它允许探索社区组件和功能并快速创建原型。

创建网站的练习有助于理解AEM网站的结构（其中可能包括社区功能），同时提供可探索如何使用社交组件框架( [SCF)的简单页面](scf.md)。

本教程主要面向对使用SCF组件感兴趣的AEM新手的开发人员。 它将逐步介绍如何创建SCF沙箱站点，与“如何创建功能齐备的Internet网站 [](../../help/sites-developing/website.md) ”教程相似，该教程侧重于站点结构，如导航、徽标、搜索、工具栏和列出子页面。

在创作实例上进行开发，而在发布实例上试验站点最好。

本教程中的步骤有：

* [设置网站结构](setup-website.md)
* [初始沙箱应用程序](initial-app.md)
* [初始沙箱内容](initial-content.md)
* [开发沙箱应用程序](develop-app.md)
* [添加Clientlibs](add-clientlibs.md)
* [开发沙箱内容](develop-content.md)

>[!CAUTION]
>
>本教程不创建具有使用“社区站点”控制台创建的功能 [的社区站点](sites-console.md)。 例如，本教程不介绍如何设置登录、自助注册、社交 [登录](social-login.md)、消息、配置文件等。
>
>如果首选使用简单的社区站点，请遵循 [创建示例页面教程](create-sample-page.md) 。

## 前提条件 {#prerequisites}

本教程假定您安装了一个AEM作者和一个AEM发布实例，该实例具有最 [新版](deploy-communities.md#latest-releases) Communities。

以下是一些对AEM平台新手的开发人员有用的链接：

* [入门](../../help/sites-deploying/deploy.md#getting-started):用于部署AEM实例

   * [基础](../../help/sites-developing/the-basics.md):面向网站和功能开发人员
   * [作者的首步](../../help/sites-authoring/first-steps.md):用于创作页面内容

## 使用CRXDE Lite开发环境 {#using-crxde-lite-development-environment}

AEM开发人员在 [](../../help/sites-developing/developing-with-crxde-lite.md) CRXDE Lite开发环境中的大部分时间都花在创作实例上。 CRXDE Lite提供对CRX存储库的较少限制的访问。 经典UI工具和触屏优化UI控制台提供对CRX存储库特定部分的更结构化的访问。

使用管理权限登录后，可通过多种方式访问CRXDE Lite:

1. 从全局导航中，选择导 **[!UICONTROL 航工具> CRXDE Lite]**。

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. 在经典 [UI欢迎页中](http://localhost:4502/welcome.html)，向下滚动并单 **[!UICONTROL 击右面板中的CRXDE Lite]** 。

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. 直接浏览到 `CRXDE Lite`: `<server>:<port>/crx/de`

   例如，在本地作者实例上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

要使用CRXDE Lite，您必须使用开发人员或管理员权限登录。 对于默认的localhost实例，您可以使用

* `username: admin`
* `password: admin`


**请注意** ，此登录将超时，您需要使用CRXDe Lite工具栏右端的下拉菜单定期重新登录。

如果未登录，您将无法导航JCR存储库或执行任何编辑／保存操作。

***如有疑问，请重新登录！***

![chlimage_1-352](assets/chlimage_1-352.png)
