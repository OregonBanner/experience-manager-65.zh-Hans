---
title: AEM Communities概述
seo-title: AEM Communities Overview
description: AEM Communities功能和设置概述
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# AEM Communities概述 {#aem-communities-overview}

Adobe Experience Manager(AEM)Communities提供了快速创建内部部署社区网站的功能，该网站已改进性能、改进了网站管理，并鼓励将网站访客转换为有价值的社区成员。

## 社区功能 {#communities-features}

AEM Communities支持与网站访客建立关系，该关系：

* **通知** 通过博客、问答和事件日历，
* While **洞察** 通过论坛、评论和其他社区内容，通常称为用户生成内容(UGC)。
* 它允许 **审核** 由发布环境中的受信任成员进行，
* **社交登录** twitter和Facebook,
* **内联翻译** 社区内容，
* **社区组创建** 从已发布的社区网站中，
* **评分** 授予徽章，
* **文件共享**,
* **通知** 和 **活动流**,
* 允许 **标记** (@mention)用户生成内容中的其他注册成员，以引起他们的注意。

社区功能可使用 [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) 可在GitHub.com上公开获取，或通过新的We.Retail参考实施获取。

## 社区站点 {#community-sites}

社区站点是使用简单向导创建的AEM站点，该向导会生成一个网站，该网站具有许多预先连接到该站点的常用功能。

的 [站点创建向导](/help/communities/sites-console.md):

* 根据所选的 [社区站点模板](/help/communities/sites.md) 即：

   * 从 [社区功能](#community-functions)
   * 可选 [社区团体](#communitygroups) 功能

* 使用设置配置：

   * 审核
   * 登录
   * 转换

* 提供基本功能：

   * 响应式设计：使用 [TwitterBootstrap主题](https://getbootstrap.com)

   * 登录：自我登记， [社交登录](/help/communities/social-login.md)，用户配置文件

      * 通知：成员会看到与其相关的事件，以及用户生成的内容 [@mentioned](/help/communities/overview.md#mentionssupport).

      * 消息传送：成员可以在社区站点内发送或接收消息。
      * 搜索：能够在社区站点内进行搜索。
      * 语言切换：能够为 [多语言站点](/help/sites-administering/translation.md).

      * 管理：有权访问已授权的成员以审核和管理社区站点中的用户。

* 消除了许多页面级别的创作步骤：

   * 品牌策略：可选上载横幅图像，以在社区网站的所有页面上显示
   * 导航菜单：为社区站点模板中包含的功能提供了导航链接。

要体验快速创建新社区站点的轻松性，请访问 [开始使用AEM Communities](/help/communities/getting-started.md).

## 社区内容持久性 {#community-content-persistence}

为了提高社区内容的性能和同步，AEM Communities要求专门为所有AEM（创作和发布）实例之间共享的用户生成内容(UGC)提供一个通用存储区。

通过存储资源提供程序(SRP)可以轻松访问社区内容，该提供程序提供一个层，用于将访问与底层拓扑分离，并支持UGC的公共存储。

要了解有关社区内容持久性和推荐部署的更多信息，请参阅：

* [社区内容存储](/help/communities/working-with-srp.md)，其中讨论了UGC的可用SRP存储选项。
* [推荐的拓扑](/help/communities/topologies.md)，其中讨论了基于用例的拓扑和SRP选择。
* [升级到AEM 6.5 Communities](/help/communities/upgrade.md)，可在移动到AEM 6.5时提供有关UGC的有用信息。

## 社区控制台 {#communities-consoles}

在创作环境中，全局导航控制台提供对 [社区控制台](/help/communities/consoles.md)，其中包含：

* [站点](/help/communities/sites-console.md) 控制台

   * 网站创建
   * 网站编辑
   * 站点管理
   * [社区组](/help/communities/groups.md) 控制台

* [审核](/help/communities/moderation.md) 控制台

   * 适用于创作和发布环境的常用批量审核UI。
   * 新的筛选条件。

* [成员和组](/help/communities/members.md) 管理控制台

   * 提供从创作环境创建和管理发布端用户（成员）的功能。
   * 提供禁止成员的功能。
   * 提供从创作环境创建和管理发布端用户组（成员组）的功能。

* [报表](/help/communities/reports.md) 控制台

   * 提供生成分配、帖子和视图报告的功能。

全局工具控制台提供对以下社区工具的访问：

* [网站模板](/help/communities/tools.md#sitetemplatesconsole) 控制台

   * 创建和管理社区站点模板。

* [组模板](/help/communities/tools.md#grouptemplatesconsole) 控制台

   * 创建和管理社区组模板。

* [社区功能](/help/communities/tools.md#communityfunctionsconsole) 控制台

   * 创建和管理社区功能。

* [存储配置](/help/communities/tools.md#storageconfiguratonconsole) 控制台

   * 选择并配置 [公用商店](/help/communities/working-with-srp.md) 中的“隐藏主体”。

* [组件指南](/help/communities/components-guide.md)

   * 一个示例网站， [社区组件](https://localhost:4502/editor.html/content/community-components/en.html)，以提供所有社区组件的示例及其默认配置和试用功能。

## 社区站点模板 {#community-site-templates}

社区站点创建基于社区站点模板的选择，以快速设置独立于任何示例站点的社区站点。

社区站点模板，由社区功能和社区组模板组成，为社区站点提供了结构，包括登录、用户档案、消息、站点菜单、搜索、主题和品牌特征。

请参阅 [站点模板控制台](/help/communities/sites.md).

## 社区功能 {#community-functions}

社区体验预期的功能已广为人知。 借助AEM Communities，这些功能可用作构建基块，称为社区功能。

社区功能是常规的AEM页面，包括连接到功能中的组件，该功能可轻松纳入社区站点模板中。

请参阅 [社区功能控制台](/help/communities/functions.md).

## 社区组和组模板 {#community-groups-and-group-templates}

“社区组”功能允许子社区由创作和发布环境的授权用户和社区成员在社区站点内动态创建。

在创作环境中，当模板的结构包含 [组函数](/help/communities/functions.md#groups-function).

创建社区组需要选择社区组模板，以提供社区组页面的设计。 在将群组功能添加到模板结构时，会将其配置为指定一个群组模板，或在创建新社区群组时提供模板选项。

另请参阅：

* [站点组控制台](/help/communities/groups.md) 用于在创作环境中创建子社区。
* [组模板控制台](/help/communities/tools-groups.md) 用于为组创建站点结构。
* [开始使用AEM Communities](/help/communities/getting-started.md) 有关快速创建包含嵌套群组的社区站点的教程。

## 社区组件 {#community-components}

的 [社区组件](/help/communities/author-communities.md) 从中构建社区站点的社区站点可用于向任何AEM站点添加社区功能。

的 [社区组件指南](/help/communities/components-guide.md) 可用于组件的交互式探索。

## 参与社区 {#engagement-community}

参与社区是一个社区站点，其重点是吸引客户告知、征求反馈并允许客户作为社区成员进行交互。

参与社区的功能可能包括：

* 登录
* 消息
* 论坛
* 评论
* 审核
* 评级
* 投票
* 博客
* 组
* 日历
* 翻译
* 审核
* 通知
* 评分和徽章
* Analytics报表

要体验快速创建新参与社区的轻松性，请访问 [开始使用AEM Communities](/help/communities/getting-started.md).

## AEM Demo Machine {#aem-demo-machine}

的 [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) 管理和运行AEM演示 [站点](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [资产](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [社区](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [应用程序](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 和 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)，这通常比启动快速启动实例需要更多的设置。 AEM演示计算机将设置其他 [基础架构](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 例如MongoDB、Solr、MySQL、FFmpeg和电子邮件服务器。

AEM演示计算机包括：

* A [图形用户界面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 可配置的Apache ANT脚本 [属性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 和 [目标](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* 要安装的包。

在Windows、MacOS和Linux上，使用CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功测试了AEM演示计算机。

AEM演示计算机需要有效的AEM许可证。

>[!NOTE]
>
>查看 [视频简介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 到AEM演示机(13:26)。

## AEM Communities文档 {#aem-communities-documentation}

* 访问 [部署社区](deploy-communities.md) 以了解建议的部署。
* 访问 [管理社区站点](administer-landing.md) 要了解有关创建社区站点、添加社区组、配置社区站点模板、审核社区内容、管理成员、标记、通知、评分和徽章的信息。
* 访问 [发展社区](communities.md) 了解社交组件框架(SCF)和自定义社区组件和功能。
* 访问 [创作社区组件](author-communities.md) 了解如何使用和配置社区组件进行创作。
