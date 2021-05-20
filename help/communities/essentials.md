---
title: 组件、功能和功能要点
seo-title: 组件、功能和功能要点
description: 社区站点、模板和组的工作方式
seo-description: 社区站点、模板和组的工作方式
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# 组件、函数和功能要点{#component-function-and-feature-essentials}

AEM Communities功能要求网站访客成为成员并登录到[社区网站](overview.md#communitiessites)，然后才能发布内容。 因此，[社区站点模板](sites.md)被设计为包括登录功能以及用户配置文件、消息传送、搜索、审核和翻译。[](sites-console.md)

当[社区组功能](functions.md#groups-function)包含在所选社区站点模板中时，社区站点将支持创建社区组的成员。

以下是社区组件、功能和功能的基本信息链接。

## 基本组件{#base-components}

* [评论](essentials-comments.md)
* [审核](reviews-basics.md)
* [计数](tally.md)

   * [点赞](essentials-liking.md)
   * [评级](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（不再可用）*

## 具有函数{#components-with-functions}的组件

* [活动流](essentials-activities.md)
* [指定任务](essentials-assignments.md)
* [博客](blog-developer-basics.md) ( `Journal`)

* [日历](calendar-basics-for-developers.md)
* [目录](catalog-developer-essentials.md)
* [专题内容](essentials-featured.md)
* [文件库](essentials-file-library.md)
* [论坛](essentials-forum.md)
* [组](essentials-groups.md)
* [构思](ideation.md)
* [排行榜](leaderboard.md)
* [问题与解答](qna-essentials.md) `(QnA)`

## 功能 {#features}

* [客户端库](clientlibs.md)
* [社区站点](sites-for-developers.md)
* [组件OSGi事件](events.md)
* [组件侧加载](sideloading.md)
* [消息](essentials-messaging.md)
* [富文本编辑器](rte.md)
* [评分和徽章](configure-scoring.md)
* [搜索](search-implementation.md)
* [社交图](essentials-socialgraph.md)
* [存储资源提供程序](srp-and-ugc.md) `(SRP)`

* [标记](tag.md)

## Javaocs {#javadocs}

[在线javadocs](../../help/sites-developing/reference-materials.md)反映了AEM 6.3版本中提供的API。
社区API位于`com.adobe.cq.social.*`包中。

对于每个[功能包](deploy-communities.md#latestfeaturepack)，都提供一个javadoc jar。 有关更多信息，请访问[使用Maven for Communities](maven.md#javadocs)。

## 附加信息 {#additional-information}

* [社交组件框架(SCF)](scf.md)

   * [客户端自定义](client-customize.md)
   * [服务器端自定义](server-customize.md)
   * [存储资源提供程序概述](srp.md)

* [编码准则](code-guide.md)
* [教程](tutorials.md)
* [疑难解答](troubleshooting.md)
