---
title: 社群群組Essentials
seo-title: Community Group Essentials
description: 動態建立社群網站
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

# 社群群組Essentials  {#community-group-essentials}

社群群組功能可讓發佈和作者環境中的授權使用者在社群網站中動態建立子社群。

截至社群 [feature pack 1](deploy-communities.md#latestfeaturepack)，群組可巢狀內嵌於其他群組中

## 適用於使用者端的Essentials {#essentials-for-client-side}

### 社群群組成員清單 {#community-groups-member-list}

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
   <td> <strong>範本</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>另請參閱 <a href="creating-groups.md">社群群組</a></td>
  </tr>
 </tbody>
</table>

### 社区组 {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [社群群組API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [社群群組端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 群組功能 {#groups-function}

社群網站結構包含 [群組功能](functions.md#groups-function) 將支援建立新的 `community groups` 從發佈和作者環境。 建立的社群群組將包含 `community groups member list` 列出群組成員的元件。

一或多個 [社群群組範本](tools-groups.md)（提供社群群組頁面設計），可在將函式新增至時為「群組」函式進行設定 [社群網站範本](sites.md) 或巢狀內嵌在社群群組範本中。

納入多個社群群組範本後，授權使用者可選擇在為社群網站建立新社群群組時看到的設計，如以下章節所示： [社群群組](creating-groups.md) 適用於作者。

### 巢狀群組 {#nested-groups}

截至社群 [FP1](deploy-communities.md#latestfeaturepack)，群組功能可包含在群組範本中，以便巢狀群組（子社群）。

當社群網站或群組範本包含「群組」功能時，可以：

* 在作者環境中建立子社群。

* 設定為允許時，在發佈環境中建立群組。

在作者環境中建立群組時，必須先發佈社群網站，然後再發佈群組。 發佈社群網站將會發佈群組的頁面，而不會建立子社群的成員群組（ACL已設定至這些群組）。 因此，在群組明確發佈之前，受限制的（秘密）群組可能一直可見。

## 連結和相關資訊 {#links-and-related-information}

* [管理使用者和使用者群組](users.md)
* [社群群組主控台](groups.md)
* [群組功能](functions.md#groups-function)
* [组模板](tools-groups.md)
