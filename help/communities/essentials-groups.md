---
title: Community Group Essentials
seo-title: Community Group Essentials
description: 动态创建社区站点
seo-description: 动态创建社区站点
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Community Group Essentials {#community-group-essentials}

社区组功能是允许从发布和创作环境授权用户在社区站点内动态创建子社区的功能。

自Communities功 [能包1起](deploy-communities.md#latestfeaturepack)，组可嵌套在其他组中

## 客户端必备工具 {#essentials-for-client-side}

### 社区组成员列表 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／组/组件/hbs/社区组成员列表</td>
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
   <td>查看 <a href="creating-groups.md">社区组</a></td>
  </tr>
 </tbody>
</table>

### 社区组 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／组/组件/hbs/社区组</td>
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

## 服务器端必备工具 {#essentials-for-server-side}

* [社区组API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社区组端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 组函数 {#groups-function}

包含“组”功能的社区站 [点结构](functions.md#groups-function) ，将支持从发布和创 `community groups` 作环境创建新内容。 创建的社区组将包含 `community groups member list` 一个将列出组成员的组件。

当该功 [能被添加到社区站点模板或嵌套在社区组模板中时](tools-groups.md)[](sites.md) ，可以为“组”功能配置一个或多个社区组模板，该模板提供社区组页面的设计。

加入多个社区组模板后，在为社区站点创建新的社区组时向授权用户展示了一个设计选择，如作者的社区组部分 [所示](creating-groups.md) 。

### 嵌套用户组 {#nested-groups}

自Communities [FP1起](deploy-communities.md#latestfeaturepack),“组”功能可能包含在组模板中，因此允许嵌套组（子社区）。

当社区站点或组模板包含“组”功能时，

* 在创作环境中创建子社区
* 在发布环境中创建组（如果配置为允许）

在创作环境中创建组时，首先必须发布社区站点，然后发布组。 发布社区站点将发布组的页面，而不创建设置了ACL的子社区的成员组。 因此，在显式发布组之前，受限（秘密）组可以是可见的。

## 链接和相关信息 {#links-and-related-information}

* [管理用户和用户组](users.md)
* [社区组控制台](groups.md)
* [组函数](functions.md#groups-function)
* [组模板](tools-groups.md)

