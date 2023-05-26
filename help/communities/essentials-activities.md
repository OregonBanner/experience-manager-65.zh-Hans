---
title: Activity Stream Essentials
seo-title: Activity Stream Essentials
description: 成员最近执行的活动的列表或单个内容线程上最近活动的列表
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
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
source-wordcount: '296'
ht-degree: 2%

---

# Activity Stream Essentials {#activity-stream-essentials}

已登录社区成员的活动（例如向论坛或博客发文）被收集到流中，该流可以通过活动流组件的配置以各种方式被过滤和显示。

当社区成员关注感兴趣的帖子或其他社区成员时，关注功能会添加另一组活动。

全部 [社区站点](/help/communities/overview.md#communitiessites) 包括已登录成员的用户配置文件页面，该页面将以相同方式显示成员活动。

## 概念 {#concepts}

An *活动流* 是成员最近执行的活动的列表，或者单个内容线程上最近活动的列表，例如论坛主题或博客。

成员可以关注活动流，方法是关注另一个个人或内容。

A *新闻馈送* 是活动流后跟一个成员合并成一个流。

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
   <td>参见 <a href="/help/communities/activities.md">活动流功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端Essentials {#essentials-for-server-side}

* [活动流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活动流侦听器API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 活动流功能 {#activity-stream-function}

社区站点结构包括 [活动流功能](/help/communities/functions.md#activity-stream-function)，包括已配置的 `activity streams` 组件。
