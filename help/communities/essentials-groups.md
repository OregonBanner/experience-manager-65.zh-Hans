---
title: 社区组要点
seo-title: Community Group Essentials
description: 动态创建社区站点
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 社区组要点  {#community-group-essentials}

“社区组”功能是让来自发布和创作环境的授权用户在社区站点内动态创建子社区的功能。

截至社区 [功能包1](deploy-communities.md#latestfeaturepack)，则可以将组嵌套在其他组中

## 客户端要点 {#essentials-for-client-side}

### 社区组成员列表 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/组/组件/hbs/社区组成员列表</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>请参阅 <a href="creating-groups.md">社区组</a></td>
  </tr>
 </tbody>
</table>

### 社区组 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/组/组件/hbs/社区组</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端要点 {#essentials-for-server-side}

* [社区组API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社区组端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 组函数 {#groups-function}

一种社区站点结构，包括 [组函数](functions.md#groups-function) 将支持创建新的 `community groups` （从发布和创作环境）。 创建的社区组将包含 `community groups member list` 列出组成员的组件。

一个或多个 [社区组模板](tools-groups.md)，当将功能添加到 [社区站点模板](sites.md) 或嵌套在社区组模板中。

如 [社区团体](creating-groups.md) 作者。

### 嵌套群组 {#nested-groups}

截至社区 [FP1](deploy-communities.md#latestfeaturepack)，则组函数可能包含在组模板中，从而允许嵌套组（子社区）。

当社区站点或组模板包含“组”功能时，可以：

* 在创作环境中创建子社区。

* 在发布环境中创建群组（如果配置为允许）。

在创作环境中创建群组时，需要先发布社区站点，然后再发布群组。 发布社区站点将发布组的页面，而不会创建设置了ACL的子社区成员组。 因此，在明确发布受限（秘密）组之前，该组是可见的。

## 链接和相关信息 {#links-and-related-information}

* [管理用户和用户组](users.md)
* [社区组控制台](groups.md)
* [组函数](functions.md#groups-function)
* [组模板](tools-groups.md)
