---
title: 活动流要点
seo-title: 活动流要点
description: 成员执行的最近活动列表或单个内容线程上的最近活动列表
seo-description: 成员执行的最近活动列表或单个内容线程上的最近活动列表
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# 活动流要点{#activity-stream-essentials}

已登录社区成员的活动，例如向论坛或博客发帖，被收集到流中，该流可以通过配置活动流组件以各种方式过滤和显示。

在社区成员关注感兴趣的帖子或其他社区成员时，跟踪功能又增加了一组活动。

所有[社区站点](/help/communities/overview.md#communitiessites)都包含登录成员的用户配置文件页面，该用户配置文件页面将以相同方式显示成员活动。

## 概念  {#concepts}

*活动流*&#x200B;是成员执行的最近活动的列表或单个内容线程（如论坛主题或博客）上的最近活动的列表。

成员可以通过跟踪其他个人或内容来跟踪活动流。

*新闻源*&#x200B;是将一个成员跟踪的活动流合并到单个流中。

*[社交图](/help/communities/essentials-socialgraph.md)*&#x200B;捕获一个成员与另一个成员的以下关系。

## 客户端{#essentials-for-client-side}的要点

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/活动流/组件/hbs/活动流</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>请参阅<a href="/help/communities/activities.md">活动流功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端{#essentials-for-server-side}的要点

* [活动流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活动流侦听器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 活动流功能 {#activity-stream-function}

包含[活动流函数](/help/communities/functions.md#activity-stream-function)的社区站点结构，包括已配置的`activity streams`组件。
