---
title: 社区组要点
seo-title: 社区组要点
description: 动态创建社区站点
seo-description: 动态创建社区站点
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# 社区组要点{#community-group-essentials}

“社区组”功能是让来自发布和创作环境的授权用户在社区站点内动态创建子社区的功能。

从Communities [功能包1](deploy-communities.md#latestfeaturepack)开始，可以将组嵌套在其他组中

## 客户端{#essentials-for-client-side}的要点

### 社区组成员列表{#community-groups-member-list}

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
   <td>请参阅<a href="creating-groups.md">社区组</a></td>
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

## 服务器端{#essentials-for-server-side}的要点

* [社区组API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社区组端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 组函数{#groups-function}

包含[组函数](functions.md#groups-function)的社区站点结构将支持从发布和创作环境创建新的`community groups`。 创建的社区组将包含一个`community groups member list`组件，该组件将列出该组的成员。

当将该函数添加到[社区站点模板](sites.md)或嵌套在社区组模板中时，可以为“组”功能配置一个或多个[社区组模板](tools-groups.md)，该模板提供社区组页面的设计。

如[社区组](creating-groups.md)中的作者社区组部分所示，如果包含多个社区组模板，则在为社区站点创建新社区组时，会向授权用户呈现一种设计选择。

### 嵌套组{#nested-groups}

从社区[FP1](deploy-communities.md#latestfeaturepack)开始，组函数可以包含在组模板中，从而允许嵌套组（子社区）。

当社区站点或组模板包含“组”功能时，可以：

* 在创作环境中创建子社区。

* 在发布环境中创建群组（如果配置为允许）。

在创作环境中创建群组时，需要先发布社区站点，然后再发布群组。 发布社区站点将发布组的页面，而不会创建设置了ACL的子社区成员组。 因此，在明确发布受限（秘密）组之前，该组是可见的。

## 链接和相关信息{#links-and-related-information}

* [管理用户和用户组](users.md)
* [社区组控制台](groups.md)
* [组函数](functions.md#groups-function)
* [组模板](tools-groups.md)
