---
title: AEM Communities 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Communities。
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 61%

---


# AEM Communities release notes {#aem-communities-release-notes}

继续阅读以了解自 6.4 发行版以后对 AEM Communities 所做的改进。To learn about the new features in greater detail, see [AEM 6.5 Communities User Guide](https://helpx.adobe.com/cn/experience-manager/6-4/communities/user-guide.html).

To obtain the latest release, see the [Deploying Communities](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases) section of the documentation.

## 主要增强功能 {#major-enhancements}

### 对社区互动的增强功能 {#enhancements-to-community-engagement}

**@Mentions支持** AEM Communities现在允许注册用户在用户生成的内容中标记（提及）其他注册成员以引起其注意。 然后通知标记（提及）的成员，并在通知中包含指向相应用户生成的内容的深层链接。但是，用户可以选择禁用／启用Web和电子邮件通知。

![@Mentions 支持](assets/at-mentions.png)

社区用户无需搜索他们的名字、姓氏或用户名，即可查看是否有人与他们联系或需要他们注意。此外，它还允许 UGC 作者寻求能够最佳解决问题并提出意见或建议的特定注册用户的答复。

The community administrators need to **Enable Mention** on community components to allow registered users use the functionality on those components.

**组消息传递**

现在，已注册的社区成员可以通过单个电子邮件合成将私聊信息批量发送到组，而不是将相同的邮件分别发送给组成员。To allow [group messaging](/help/communities/configure-messaging.md), enable both the instances of [Messaging Operations Service](/help/communities/messaging.md#group-messaging).

![组消息](assets/group-messaging.png)

### 批量审核增强功能 {#enhancements-to-bulk-moderation}

批量审核中的自定义过滤器

[现在可以开](/help/communities/moderation.md#custom-filters) 发自定义过滤器并将其添加到批量协调UI。

[Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 中提供了一个演示通过标记进行筛选的[样本项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)。该项目可用作开发类似自定义筛选器的基础。

![自定义筛选器](assets/custom-tag-filter.png)

**批量审核中列表视图**

在批量审核中提供了一个改进了 UI 的新列表视图，用于显示用户生成的内容条目。

![列表视图中的批量审核](assets/list-view-moderation.png)

### 站点和组管理增强功能 {#enhancements-to-site-and-group-management}

**作者端站点和组管理员**

AEM 6.5 以后的 Communities 允许对不同的社区站点和组/嵌套组进行分散式管理。托管多个社区站点和嵌套组的组织现在可以在创建站点（和组）时在作者端选择管理员角色成员。

![站点管理员](assets/site-admin.png)

站点管理员可以在任何级别的层次结构中创建组，并成为默认管理员。以后，其他组管理员可以删除这些管理员。 组管理员可以管理其组 G1 并创建嵌套在 G1 下的子组。

### 启用增强功能 {#enhancements-to-enablement}

**SCORM 2017.1 支持**

The enablement functionality of AEM 6.5 Communities support Shareable Content Object Reference Model [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.

* 启用组件上的键盘导航支持
* AEM Communities中的支持组件（例如目录和课程播放、任务、文件库）支持键盘导航以改进辅助功能。

### 其他增强功能 {#other-enhancements}

* Solr 7支持
* AEM 6.5 Communities在设置MSRP和DSRP时支持Apache Solr 7.0版本的搜索平台。
