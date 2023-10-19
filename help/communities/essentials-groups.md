---
title: 社区组要点
description: 了解授权用户如何使用社区组功能在社区站点中动态创建子社区。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 1%

---

# 社区组要点  {#community-group-essentials}

社区组功能允许子社区由发布和创作环境中的授权用户在社区站点中动态创建。

截止社区 [功能包1](deploy-communities.md#latestfeaturepack)时，组可以嵌套在其他组内。

## 适用于客户端的Essentials {#essentials-for-client-side}

### 社区组成员列表 {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>social/group/components/hbs/community groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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

## 服务器端的Essentials {#essentials-for-server-side}

* [社区组API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社区组端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 组功能 {#groups-function}

社区站点结构包括 [“组”功能](functions.md#groups-function) 支持创建新的 `community groups` 发布和创作环境。 创建的社区组包括 `community groups member list` 列出组成员的组件。

一个或多个 [社区组模板](tools-groups.md)提供了社区组页面设计，可以为“组”功能进行配置。 将函数添加到时为true [社区站点模板](sites.md) 或嵌套在社区组模板内。

可以选择多个社区组模板。 即，在为社区站点创建社区组时向授权用户呈现的设计选择。 请参阅以下部分 [社区组](creating-groups.md) 供作者使用。

### 嵌套组 {#nested-groups}

截止社区 [FP1](deploy-communities.md#latestfeaturepack)，组模板中可以包含组函数，这样可以嵌套组（子社区）。

当社区站点或组模板包含组功能时，可以：

* 在创作环境中创建子社区。

* 配置允许后，在发布环境中创建组。

在创作环境中创建组时，必须首先发布社区站点，然后发布组。 发布社区站点会发布组的页面，而不创建设置了ACL的子社区的成员组。 因此，在显式发布某个受限（机密）组之前，该组可能一直可见。

## 链接和相关信息 {#links-and-related-information}

* [管理用户和用户组](users.md)
* [社区组控制台](groups.md)
* [组功能](functions.md#groups-function)
* [组模板](tools-groups.md)
