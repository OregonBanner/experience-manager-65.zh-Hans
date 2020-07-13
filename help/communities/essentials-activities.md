---
title: 活动流基础
seo-title: 活动流基础
description: 成员对单个内容线程执行的最近活动列表或最近活动的列表
seo-description: 成员对单个内容线程执行的最近活动列表或最近活动的列表
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---


# 活动流基础 {#activity-stream-essentials}

已签名的社区成员的活动，例如发布到论坛或博客，被收集到流中，该流可以通过配置活动流组件以各种方式被过滤和显示。

当社区成员关注感兴趣的帖子或其他社区成员时，跟踪功能会添加另一组活动。

所有 [社区站点](/help/communities/overview.md#communitiessites) 都包含已登录成员的用户用户档案页，该用户活动页将以相同方式显示成员。

## 概念 {#concepts}

活动 *流* 是成员对单个内容线程（如论坛主题或博客）执行的最近活动的列表或最近活动的列表。

成员可以通过关注其他个人或内容来关注活动流。

新 *闻源* ，是活动流的合并，其后是成员到单个流中。

社 *[交图](/help/communities/essentials-socialgraph.md)*，捕获一个成员与另一个成员的以下关系。

## 客户端必备工具 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／活动流／组件/hbs/活动流</td>
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
   <td>查看 <a href="/help/communities/activities.md">活动流功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [活动流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活动流监听器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 活动流功能 {#activity-stream-function}

一种包括活动流功能的 [社区站点结构](/help/communities/functions.md#activity-stream-function)，包括配置的 `activity streams` 组件。
