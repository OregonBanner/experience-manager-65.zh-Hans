---
title: AEM Communities概述
seo-title: AEM Communities概述
description: AEM Communities功能和设置的概述
seo-description: AEM Communities功能和设置的概述
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# AEM Communities概述 {#aem-communities-overview}

利用 Adobe Experience Manager (AEM) Communities，可以快速创建内部部署社区网站，从而提升性能和网站管理能力，同时促进网站访客转化为有价值的社区成员。

有关AEM Communities的授权许可以及针对支持功能和Adobe Analytics的其他授权许可的信息，请与您的客户代表联系。

## 社区功能 {#communities-features}

AEM Communities支持与站点访客建立关系，这包括：

* **通过博客** 、问题与答案和事件日历提供信息，
* 通过 **论坛** 、评论和其他社区内容(通常称为用户生成的内容(UGC))获得洞察。
* 它允许 **由发布环境** 、
* **使用Twitter** 和Facebook进行社交登录，
* **社区内容的内联翻译** ,
* **从已发布的社区站点** 、
* **评分** ，奖章，
* **文件共享**,
* **通知** 和 **活动流**,
* 允许 **在用户生成** 的内容中标记(@tonticle)其他注册成员，以引起他们的注意。
* 支持 **在启用组件** （例如“目录”和“课程播放”、“任务”、“文件库”）上进行键盘导航。

社区功能可以使用GitHub.com上公开提供的 [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) ，或通过新的We.Retail参考实施进行演示。

## 社区站点 {#community-sites}

社区站点是使用简单向导创建的AEM站点，该向导生成的网站具有预先连接到该站点的许多常见功能。

站点 [创建向导](/help/communities/sites-console.md):

* 根据选定的社区站点模板组合站 [点的功能](/help/communities/sites.md) ，该模板是：

   * 由社区功 [能构建](#community-functions)
   * 可选 [社区组功能](#communitygroups)

* 使用设置进行配置：

   * 审核
   * 登录
   * 转换

* 提供基本功能：

   * 响应式设计：使用 [Twitter Bootstrap主题](https://getbootstrap.com)

   * 登录：自助注册、社交 [登录](/help/communities/social-login.md)、用户用户档案

      * 通知：成员会看到与他们相关的事件，以及用户生成的内容( [@interticated)](/help/communities/overview.md#mentionssupport)。

      * 消息传递：会员可以在社区站点内发送或接收消息。
      * 搜索：能够在社区站点内进行搜索。
      * 语言切换：能够为多语言站点选择 [语言](/help/sites-administering/translation.md)。

      * 管理：允许授权成员审核和管理社区站点内的用户。

* 消除了许多页面级创作步骤：

   * 品牌：可选上传横幅图像，以在社区站点的所有页面上显示
      * 导航菜单：为社区站点模板中包含的功能提供了导航链接。

要体验快速创建新社区站点的轻松性，请访 [问AEM Communities快速入门](/help/communities/getting-started.md)。

## 社区内容持久性 {#community-content-persistence}

为了提高社区内容的性能和同步性，AEM Communities需要专门针对在所有AEM（创作和发布）实例之间共享的用户生成内容(UGC)的公用存储。

通过存储资源提供者(SRP)可轻松访问社区内容，该提供者提供一个层，用于将访问与底层拓扑分开，并支持UGC的公共存储。

要进一步了解社区内容持久性和建议的部署，请参阅：

* [社区内容存储](/help/communities/working-with-srp.md)，其中讨论了UGC的可用SRP存储选项。
* [推荐的拓扑](/help/communities/topologies.md)，它根据用例和SRP选择讨论拓扑。
* [升级到AEM 6.5 Communities](/help/communities/upgrade.md)，它在转到AEM 6.5时提供有关UGC的有用信息。

## 社区控制台 {#communities-consoles}

在创作环境中，全局导航控制台提供对“社区”控制 [台的访问](/help/communities/consoles.md)，该控制台包含：

* [站点](/help/communities/sites-console.md)控制台

   * 站点创建
   * 站点编辑
   * 站点管理
   * [“社区组](/help/communities/groups.md) ”控制台

* [审核控制台](/help/communities/moderation.md) ,

   * 创作和发布环境的通用批量协调UI。
   * 新的筛选条件。

* [“成员”和“组](/help/communities/members.md) ”管理控制台

   * 提供从创作环境创建和管理发布端用户（成员）的功能。
   * 提供禁止会员的功能。
   * 提供从创作环境创建和管理发布端用户组（成员组）的功能。

* [“报告](/help/communities/reports.md) ”控制台

   * 提供生成任务、帖子和视图报告的功能。

* [“资源](/help/communities/resources.md) ”控制台

   * 提供创建支持资源和学习路径的功能。
   * 提供对有关启用资源和学习路径的报告的访问。

全局工具控制台提供对以下社区工具的访问：

* [站点模板](/help/communities/tools.md#sitetemplatesconsole) “控制台

   * 创建和管理社区站点模板。

* [“组模板](/help/communities/tools.md#grouptemplatesconsole) ”控制台

   * 创建和管理社区组模板。

* [“社区功能](/help/communities/tools.md#communityfunctionsconsole) ”控制台

   * 创建和管理社区功能。

* [存储配置控制台](/help/communities/tools.md#storageconfiguratonconsole)

   * 选择并配置站 [点的公](/help/communities/working-with-srp.md) 用商店。

* [组件指南](/help/communities/components-guide.md)

   * 示例站点“社 [区组件”](https://localhost:4502/editor.html/content/community-components/en.html)，它提供所有社区组件的示例，包括它们的默认配置以及试验这些组件的能力。

## 社区站点模板 {#community-site-templates}

社区站点的创建基于社区站点模板的选择，以快速设置独立于任何示例站点的社区站点。

社区站点模板由社区功能和社区组模板组成，它为社区站点提供了结构，包括登录名、用户用户档案、消息、站点菜单、搜索、主题和品牌功能。

请参阅“站 [点模板”控制台](/help/communities/sites.md)。

## 社区功能 {#community-functions}

社区体验预期的功能众所周知。 在AEM Communities中，这些功能可以作为构件块提供，称为社区功能。

社区功能是普通的AEM页面，其中包括连接到功能中的组件，该功能可以轻松地集成到社区站点模板中。

请参阅“社 [区功能”控制台](/help/communities/functions.md)。

## 社区组和组模板 {#community-groups-and-group-templates}

社区组功能是让来自作者和发布环境的授权用户和社区成员在社区站点内动态创建子社区的功能。

在创作环境中，当模板的结构包含“组”功能时，可以在现有社区站点内创建社区组（子社区）或嵌套在现有组内 [](/help/communities/functions.md#groups-function)。

创建社区组需要选择提供社区组页面设计的社区组模板。 将“组”功能添加到模板结构时，该功能将配置为指定一个组模板或在创建新社区组时提供模板选择。

另请参阅：

* [站点组控制台](/help/communities/groups.md) ，用于在创作环境中创建子社区。
* [“组模板”控制台](/help/communities/tools-groups.md) ，用于为组创建站点结构。
* [AEM Communities快速入门](/help/communities/getting-started.md) ，以获取有关快速创建包含嵌套组的社区站点的教程。

## 社区组件 {#community-components}

构 [建社区站点的社区组件](/help/communities/author-communities.md) ，可用于向任何AEM站点添加社区功能。

社区 [组件指南](/help/communities/components-guide.md) ，可用于交互式探索组件。

## 社区类型 {#types-of-communities}

### 参与社区 {#engagement-community}

参与社区是一个社区站点，其重点是吸引客户通知、征求反馈并允许客户作为社区成员进行交互。

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
* 分析报告

要体验快速创建新参与社区的轻松性，请访 [问AEM Communities快速入门](/help/communities/getting-started.md)。

### Enablement Community {#enablement-community}

支持社区是一个社区站点，其中包含在线学习功能。

支持社区的功能可能包括：

* 参与社区的所有 [功能](#engagement-community)。
* 能够分配内容和学习。 资源。
* 支持SCORM内容，如测验和测试。
* 任务完成跟踪。
* 访问报告和分析。
* 能够通过论坛、消息、评论和评级与学习资源进行对话。

在配置Enablement Add-on时可以创建 [Enablement Community](/help/communities/enablement.md)，这需要额外的许可才能在生产环境中使用。 支持社区站点将包含任务 [功能](#community-functions)。

要体验创建新启用社区的轻松性，请访 [问AEM Communities for Enablement快速入门](/help/communities/getting-started-enablement.md)。

## AEM Demo Machine {#aem-demo-machine}

AEM演示 [机器管理并运行AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) Sites [、](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)Assets [、](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)Communities、AppsDemus和 [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)FormsForms的AEM Demo Machine，通常需要的设置比启动QuickStart实例的设置更多。 AEM Demo Machine将设置其他基 [础结构](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) ，如MongoDB、Solr、MySQL、FFmpeg和电子邮件服务器。

AEM Demo Machine包括：

* 图形 [用户界面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置属性和 [目标](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 的Apache ANT [脚本](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)。

* 要安装的包。

在Windows、MacOS和Linux上，AEM Demo Machine已通过CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功测试。

AEM Demo Machine需要有效的AEM许可证。

>[!NOTE]
>
>视图 [AEM Demo Machine](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) (13:26)的视频简介。


## AEM Communities文档 {#aem-communities-documentation}

* 访问 [部署社区](deploy-communities.md) ，了解推荐的部署。
* 访问 [管理社区站点](administer-landing.md) ，了解如何创建社区站点、添加社区组、配置社区站点模板、管理社区内容、管理成员、标记、通知、评分和标记。
* 访问 [开发社区](communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。
* 访问 [创作社区组件](author-communities.md) ，了解如何创作和配置社区组件。

