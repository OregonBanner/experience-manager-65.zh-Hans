---
title: Activity Stream Essentials
description: 成员执行的最近活动的列表或单个内容线程上的最近活动的列表
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# Activity Stream Essentials {#activity-stream-essentials}

已登录的社区成员的活动，例如向论坛或博客发文，被收集到流中，该流可以通过活动流组件的配置以各种方式被过滤和显示。

当社区成员关注感兴趣的帖子或其他社区成员时，关注功能会添加另一组活动。

全部 [社区站点](/help/communities/overview.md#communitiessites) 包括已登录成员的用户配置文件页面，该页面将以相同方式显示成员活动。

## 概念 {#concepts}

An *活动流* 是成员最近执行的活动的列表或单个内容线程上的最近活动的列表，如论坛主题或博客。

成员可以关注活动流，方法是关注另一个个人或内容。

A *新闻馈送* 是成员后面紧跟的活动流合并到单个流中。

A *[社交图](/help/communities/essentials-socialgraph.md)* 捕获一个成员与另一个成员的以下关系。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅 <a href="/help/communities/activities.md">活动流功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [活动流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活动流侦听器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 活动流功能 {#activity-stream-function}

社区站点结构包括 [活动流功能](/help/communities/functions.md#activity-stream-function)，包括已配置的 `activity streams` 组件。
