---
title: 社区组基本工具
seo-title: 社区组基本工具
description: 动态创建社区站点
seo-description: 动态创建社区站点
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# 社区组基本工具  {#community-group-essentials}

社区组功能是允许来自发布和创作环境的授权用户在社区站点内动态创建子社区的功能。

自“社区 [”功能包](deploy-communities.md#latestfeaturepack)1起，组可以嵌套在其他组中

## 客户端必备工具 {#essentials-for-client-side}

### 社区组成员列表 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／组/组件/hbs/社区成员列表</td>
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

包含“组”功能的社 [区站点结构](functions.md#groups-function) ，将支持从发布和 `community groups` 作者环境创建新站点。 创建的社区组将包 `community groups member list` 含一个将列表组成员的组件。

当该功 [能被添加到社区站点模板或嵌套在社区组模板中时](tools-groups.md)，可以为“组”功能配置一个或多 [个社区组模板，该模板提供社](sites.md) 区组页面的设计。

加入多个社区组模板后，在为社区站点创建新社区组时向授权用户展示设计选项，如作者社区组 [部分](creating-groups.md) 所示。

### 嵌套组 {#nested-groups}

自Communities [FP1起](deploy-communities.md#latestfeaturepack)，组功能可以包含在组模板中，从而允许嵌套组（子社区）。

当社区站点或组模板包含“组”功能时，可以：

* 在作者环境创建子社区。

* 在发布环境中创建组（如果配置为允许）。

在创作环境中创建组时，必须先发布社区站点，然后发布组。 发布社区站点将发布组的页面，而不创建设置ACL的子社区成员组。 因此，在显式发布组之前，受限（秘密）组可以是可见的。

## 链接和相关信息 {#links-and-related-information}

* [管理用户和用户组](users.md)
* [社区组控制台](groups.md)
* [组函数](functions.md#groups-function)
* [组模板](tools-groups.md)

