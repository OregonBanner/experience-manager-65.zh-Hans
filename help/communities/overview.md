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
translation-type: tm+mt
source-git-commit: 4533fa42fa3fa9f157d5ca8fee1251005b1d587e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---


# AEM Communities概述 {#aem-communities-overview}

利用 Adobe Experience Manager (AEM) Communities，可以快速创建内部部署社区网站，从而提升性能和网站管理能力，同时促进网站访客转化为有价值的社区成员。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 社区功能 {#communities-features}

AEM Communities支持与网站访客建立关系，这包括：

* **通过** 博客、问题与答案和事件日历提供信息，
* 在通 **过论坛** 、评论和其他社区内容获得洞察的同时，这些内容通常称为用户生成的内容(UGC)。
* 它允许 **发布环境** 中受信任的成员进行审核，
* **使用Twitter** 和Facebook进行社交登录，
* **社区内容** 、社区内容的内联翻译
* **从已发布的社区** 站点创建社区组，
* **评分** ，奖章，
* **文件共享**,
* **通知** 和 **活动流**,
* 允许 **在用户** 生成的内容中标记（@提及）其他注册成员，以引起他们的注意。
* 支持 **启用组件** （例如“目录”和“课程播放”、“任务”、“文件库”）上的键盘导航。

社区功能可通过GitHub.com [上公开提供的](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) AEM Demo Machine或通过新的We.Retail参考实施进行演示。

## 社区站点 {#community-sites}

社区站点是使用简单的向导创建的AEM站点，该向导会生成具有许多预先连接到站点的常用功能的网站。

站点 [创建向导](/help/communities/sites-console.md):

* 根据选定的社区站点模板组 [装站点的功](/help/communities/sites.md) 能，即：

   * 由社区功 [能构建](#community-functions)
   * 可选 [社区组功](#communitygroups) 能

* 使用设置进行配置：

   * 审核
   * 登录
   * 转换

* 提供基本功能：

   * 响应式设计：使用 [TwitterBootstrap主题](https://getbootstrap.com)

   * 登录：自助注册、社 [交登录](/help/communities/social-login.md)、用户用户档案

      * 通知：成员会看到与他们相关的事件，以及用户生成的内容，这些内 [容被@itted](/help/communities/overview.md#mentionssupport)。

      * 消息：会员可以在社区站点内发送或接收消息。
      * 搜索：能够在社区站点内进行搜索。
      * 语言切换：能够为多语言站点选 [择语言](/help/sites-administering/translation.md)。

      * 管理：允许授权成员审核和管理社区站点内的用户。

* 消除许多页面级创作步骤：

   * 品牌：可选上传横幅图像以在社区站点的所有页面上显示
   * 导航菜单：为社区站点模板中包含的功能提供了导航链接。

要体验快速创建新社区站点的便利性，请访 [问AEM Communities入门](/help/communities/getting-started.md)。

## 社区内容持久性 {#community-content-persistence}

为了改进社区内容的性能和同步，AEM Communities要求为所有AEM（作者和发布）实例之间共享的用户生成内容(UGC)提供一个专用的公用存储。

社区内容可通过存储资源提供者(SRP)轻松访问，该提供者提供一个层，用于将访问与底层拓扑分离，并支持UGC的公共存储。

要进一步了解社区内容持久性和推荐的部署，请参阅：

* [社区内容存储](/help/communities/working-with-srp.md)，讨论UGC的可用SRP存储选项。
* [推荐拓扑](/help/communities/topologies.md)，它根据用例和SRP选择讨论拓扑。
* [升级到AEM 6.5 Communities](/help/communities/upgrade.md)，在移到AEM 6.5时，它提供有关UGC的有用信息。

## 社区控制台 {#communities-consoles}

在创作环境中，全局导航控制台提供对“社区”控 [制台的访问](/help/communities/consoles.md)，该控制台包含：

* [站点](/help/communities/sites-console.md)控制台

   * 站点创建
   * 站点编辑
   * 站点管理
   * [“社区组](/help/communities/groups.md) ”控制台

* [审核控制](/help/communities/moderation.md) 台

   * 创作和发布环境的通用批量协调UI。
   * 新的筛选条件。

* [成员和组管理](/help/communities/members.md) 控制台

   * 提供从创作环境创建和管理发布端用户（成员）的功能。
   * 提供禁止会员的功能。
   * 提供从创作环境创建和管理发布端用户组（成员组）的功能。

* [“报告](/help/communities/reports.md) ”控制台

   * 提供生成任务、帖子和视图报告的功能。

* [“资源](/help/communities/resources.md) ”控制台

   * 提供创建支持资源和学习路径的功能。
   * 提供对有关启用资源和学习路径的报告的访问。

全局工具控制台提供对以下社区工具的访问：

* [站点模板控制](/help/communities/tools.md#sitetemplatesconsole) 台

   * 创建和管理社区站点模板。

* [“组模板](/help/communities/tools.md#grouptemplatesconsole) ”控制台

   * 创建和管理社区组模板。

* [社区功能控制](/help/communities/tools.md#communityfunctionsconsole) 台

   * 创建和管理社区功能。

* [存储配置](/help/communities/tools.md#storageconfiguratonconsole) 控制台

   * 选择并配置站 [点的公](/help/communities/working-with-srp.md) 用商店。

* [组件指南](/help/communities/components-guide.md)

   * 示例站点“ [社区组件](https://localhost:4502/editor.html/content/community-components/en.html)”，它提供所有社区组件的示例以及它们的默认配置和试验能力。

## 社区站点模板 {#community-site-templates}

社区站点创建基于社区站点模板的选择，以快速设置独立于任何示例站点的社区站点。

社区站点模板由社区功能和社区组模板组成，它提供社区站点的结构，包括登录名、用户用户档案、消息、站点菜单、搜索、主题和品牌特征。

请参阅站 [点模板控制台](/help/communities/sites.md)。

## 社区功能 {#community-functions}

社区体验预期的功能众所周知。 在AEM Communities，这些功能可以作为构件，称为社区功能。

社区功能是普通的AEM页面，包括连接到功能中的组件，该功能可轻松融入社区站点模板中。

请参阅“社 [区功能”控制台](/help/communities/functions.md)。

## 社区组和组模板 {#community-groups-and-group-templates}

社区组功能是允许来自作者和发布环境的授权用户和社区成员在社区站点内动态创建子社区的功能。

从作者环境，当模板的结构包含“组”功能时，可以在现有社区站点内创建社区组（子社区）或嵌套在现有 [组内](/help/communities/functions.md#groups-function)。

创建社区组需要选择提供社区组页面设计的社区组模板。 将“组”功能添加到模板结构后，将配置为指定一个组模板或在创建新社区组时提供模板选项。

另请参阅：

* [站点组控制台](/help/communities/groups.md) ，用于在创作环境中创建子社区。
* [“组模板](/help/communities/tools-groups.md) ”控制台，用于为组创建站点结构。
* [快速创建包含嵌套组](/help/communities/getting-started.md) 的社区站点的教程，快速入门AEM Communities。

## 社区组件 {#community-components}

构 [建社区站点](/help/communities/author-communities.md) 的社区组件可用于向任何AEM站点添加社区功能。

社区 [组件指南](/help/communities/components-guide.md) ，可用于交互式探索这些组件。

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

要体验快速创建新参与社区的便利性，请访 [问AEM Communities入门](/help/communities/getting-started.md)。

### Enablement Community {#enablement-community}

支持社区是一个社区站点，其中包含在线学习功能。

支持社区的功能可能包括：

* 参与社区的所 [有功能](#engagement-community)。
* 能够分配内容和学习。 资源。
* 支持SCORM内容，如测验和测试。
* 任务完成跟踪。
* 访问报告和分析。
* 能够通过论坛、消息、评论和评级与学习资源进行对话。

配置Enablement Add-on时可以创建 [Enablement Community](/help/communities/enablement.md)，这要求在生产环境中使用额外的许可。 支持社区站点将包含 [任务功能](#community-functions)。

要体验创建新的支持社区的轻松性，请访 [问AEM Communities支持入门](/help/communities/getting-started-enablement.md)。

## AEM Demo Machine {#aem-demo-machine}

AEM [Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) 管理和运行AEM Sites [、Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、 [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、 Apps [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)Apps和Bildo Forms的演示，通常需要设置比启动QuickStart实例更多的设置。 AEM Demo Machine将设置其他 [基础](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 架构，如MongoDB、Solr、MySQL、FFmpeg和电子邮件服务器。

AEM Demo Machine包括：

* 图 [形用户界面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置属性和 [目标](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 的 [Apache ANT脚本](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)。

* 要安装的包。

在Windows、MacOS和Linux上，AEM Demo Machine已通过CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功测试了Demo Machine。

AEM Demo Machine需要有效的AEM许可证。

>[!NOTE]
>
>视图 [AEM](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 演示机的简介视频(13:26)。

## AEM Communities文档 {#aem-communities-documentation}

* 访问 [部署社区](deploy-communities.md) ，了解建议的部署。
* 访问 [管理社区站点](administer-landing.md) ，了解如何创建社区站点、添加社区组、配置社区站点模板、管理社区内容、管理成员、标记、通知、评分和徽章。
* 访 [问开发社区](communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。
* 访问 [创作社区组件](author-communities.md) ，了解如何创作和配置社区组件。

