---
title: AEM Communities概述
seo-title: AEM Communities概述
description: AEM Communities功能和设置概述
seo-description: AEM Communities功能和设置概述
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---

# AEM Communities概述{#aem-communities-overview}

利用 Adobe Experience Manager (AEM) Communities，可以快速创建内部部署社区网站，从而提升性能和网站管理能力，同时促进网站访客转化为有价值的社区成员。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 社区功能{#communities-features}

AEM Communities支持与网站访客建立关系，该关系：

* **** 通过博客、问答和事件日历提供信息，
* 而&#x200B;**通过论坛、评论和其他社区内容获取分析**，通常称为用户生成内容(UGC)。
* 它允许发布环境中受信任的成员&#x200B;**审核**。
* **与Twitter** 和Facebook的社交登录，
* **社区** 内容的内联翻译，
* **从已发布的** 社区网站创建社区组，
* **** 奖章，
* **文件共享**、
* **** 通知和 **活动流**、
* 允许&#x200B;**标记**(@mention)用户生成内容中的其他已注册成员，以引起他们的注意。
* 在启用组件上支持&#x200B;**键盘导航**（例如，“目录和课程播放”、“任务”、“文件库”）。

社区功能可以使用GitHub.com上公开提供的[AEM演示机器](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)或通过新的We.Retail参考实施进行演示。

## 社区站点 {#community-sites}

社区站点是使用简单向导创建的AEM站点，该向导会生成一个网站，该网站具有许多预先连接到该站点的常用功能。

[站点创建向导](/help/communities/sites-console.md):

* 根据所选[社区站点模板](/help/communities/sites.md)组合站点的功能，即：

   * 从[社区函数](#community-functions)构建
   * 可选[社区组](#communitygroups)功能

* 使用设置配置：

   * 审核
   * 登录
   * 转换

* 提供基本功能：

   * 响应式设计：使用[TwitterBootstrap主题](https://getbootstrap.com)

   * 登录：自注册， [社交登录](/help/communities/social-login.md)，用户配置文件

      * 通知：
成员会看到与其相关的事件，以及用户生成的内容，其中它们位于[@mentioned](/help/communities/overview.md#mentionssupport)。

      * 消息传送：成员可以在社区站点内发送或接收消息。
      * 搜索：能够在社区站点内进行搜索。
      * 语言切换：能够为[多语言站点](/help/sites-administering/translation.md)选择语言。

      * 管理：有权访问已授权的成员以审核和管理社区站点中的用户。

* 消除了许多页面级别的创作步骤：

   * 品牌策略：可选上载横幅图像，以在社区网站的所有页面上显示
   * 导航菜单：为社区站点模板中包含的功能提供了导航链接。

要体验快速创建新社区站点的便利性，请访问[AEM Communities快速入门](/help/communities/getting-started.md)。

## 社区内容持久性{#community-content-persistence}

为了提高社区内容的性能和同步，AEM Communities要求专门为所有AEM（创作和发布）实例之间共享的用户生成内容(UGC)提供一个通用存储区。

通过存储资源提供程序(SRP)可以轻松访问社区内容，该提供程序提供一个层，用于将访问与底层拓扑分离，并支持UGC的公共存储。

要了解有关社区内容持久性和推荐部署的更多信息，请参阅：

* [社区内容存储](/help/communities/working-with-srp.md)，讨论UGC的可用SRP存储选项。
* [推荐的拓扑](/help/communities/topologies.md)，该拓扑根据用例和SRP选择讨论了拓扑。
* [升级到AEM 6.5 Communities](/help/communities/upgrade.md)，在迁移到AEM 6.5时，该工具提供有关UGC的有用信息。

## 社区控制台{#communities-consoles}

在创作环境中，全局导航控制台提供对[Communities console](/help/communities/consoles.md)的访问，其中包含：

* [站点](/help/communities/sites-console.md)控制台

   * 网站创建
   * 网站编辑
   * 站点管理
   * [社区组控](/help/communities/groups.md) 制台

* [](/help/communities/moderation.md) 审核控制台

   * 适用于创作和发布环境的常用批量审核UI。
   * 新的筛选条件。

* [成员和组管](/help/communities/members.md) 理控制台

   * 提供从创作环境创建和管理发布端用户（成员）的功能。
   * 提供禁止成员的功能。
   * 提供从创作环境创建和管理发布端用户组（成员组）的功能。

* [](/help/communities/reports.md) 报表控制台

   * 提供生成分配、帖子和视图报告的功能。

* [](/help/communities/resources.md) 资源控制台

   * 提供了创建支持资源和学习路径的功能。
   * 提供对有关启用资源和学习路径的报告的访问权限。

全局工具控制台提供对以下社区工具的访问：

* [站点模](/help/communities/tools.md#sitetemplatesconsole) 板控制台

   * 创建和管理社区站点模板。

* [组模板控](/help/communities/tools.md#grouptemplatesconsole) 制台

   * 创建和管理社区组模板。

* [社区功能](/help/communities/tools.md#communityfunctionsconsole) 控制台

   * 创建和管理社区功能。

* [存储配](/help/communities/tools.md#storageconfiguratonconsole) 置控制台

   * 选择并配置站点的[公用商店](/help/communities/working-with-srp.md)。

* [组件指南](/help/communities/components-guide.md)

   * 一个示例站点[社区组件](https://localhost:4502/editor.html/content/community-components/en.html)，为所有社区组件提供了示例及其默认配置和实验功能。

## 社区站点模板 {#community-site-templates}

社区站点创建基于社区站点模板的选择，以快速设置独立于任何示例站点的社区站点。

社区站点模板，由社区功能和社区组模板组成，为社区站点提供了结构，包括登录、用户档案、消息、站点菜单、搜索、主题和品牌特征。

请参阅[站点模板控制台](/help/communities/sites.md)。

## 社区功能 {#community-functions}

社区体验预期的功能已广为人知。 借助AEM Communities，这些功能可用作构建基块，称为社区功能。

社区功能是常规的AEM页面，包括连接到功能中的组件，该功能可轻松纳入社区站点模板中。

请参阅[社区函数控制台](/help/communities/functions.md)。

## 社区组和组模板{#community-groups-and-group-templates}

“社区组”功能允许子社区由创作和发布环境的授权用户和社区成员在社区站点内动态创建。

在创作环境中，当模板的结构包含[组函数](/help/communities/functions.md#groups-function)时，可以在现有社区站点内创建社区组（子社区）或嵌套在现有组内。

创建社区组需要选择社区组模板，以提供社区组页面的设计。 在将群组功能添加到模板结构时，会将其配置为指定一个群组模板，或在创建新社区群组时提供模板选项。

另请参阅：

* [站点组](/help/communities/groups.md) 用于在创作环境中创建子社区。
* [组模板控](/help/communities/tools-groups.md) 制台，用于为组创建站点结构。
* [AEM社区快速入](/help/communities/getting-started.md) 门教程，其中介绍了如何快速创建社区站点（包括嵌套群组）。

## 社区组件{#community-components}

从中构建社区站点的[社区组件](/help/communities/author-communities.md)可用于向任何AEM站点添加社区功能。

[社区组件指南](/help/communities/components-guide.md)可用于交互式探索组件。

## 社区类型{#types-of-communities}

### 参与社区{#engagement-community}

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

要体验快速创建新参与社区的便利性，请访问[AEM Communities快速入门](/help/communities/getting-started.md)。

### 启用社区{#enablement-community}

支持社区是一个社区网站，其中包含用于在线学习的功能。

支持社区的功能可能包括：

* [参与社区](#engagement-community)的所有功能。
* 能够分配内容和学习。 向成员和成员组提供资源。
* 支持SCORM内容，如测验和测试。
* 跟踪分配完成情况。
* 对报告与分析的访问权限。
* 通过论坛、消息、评论和评级进行学习资源对话的能力。

配置[启用附加组件](/help/communities/enablement.md)后，可能会创建启用社区，这需要获得额外的许可才能在生产环境中使用。 支持社区站点将包含[分配函数](#community-functions)。

要体验创建新启用社区的便利性，请访问[AEM Communities支持入门](/help/communities/getting-started-enablement.md)。

## AEM演示机{#aem-demo-machine}

[AEM演示计算机](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)管理并运行AEM [站点](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[资产](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[社区](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[应用程序](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)和[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)的演示，这通常比启动快速启动实例更需要设置。 AEM演示计算机将设置其他[基础架构](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)，如MongoDB、Solr、MySQL、FFmpeg和电子邮件服务器。

AEM演示计算机包括：

* [图形用户界面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置[属性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)和[目标](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)的Apache ANT脚本。

* 要安装的包。

在Windows、MacOS和Linux上，使用CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功测试了AEM演示计算机。

AEM演示计算机需要有效的AEM许可证。

>[!NOTE]
>
>查看AEM演示机(13:26)的[视频简介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)。

## AEM Communities文档{#aem-communities-documentation}

* 访问[部署Communities](deploy-communities.md)以了解建议的部署。
* 访问[管理社区站点](administer-landing.md) ，了解有关创建社区站点、添加社区组、配置社区站点模板、审核社区内容、管理成员、标记、通知、评分和徽章的信息。
* 访问[开发社区](communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。
* 访问[创作社区组件](author-communities.md) ，了解如何使用和配置社区组件进行创作。
