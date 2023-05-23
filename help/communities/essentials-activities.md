---
title: Activity Stream Essentials
seo-title: Activity Stream Essentials
description: 成員最近執行的活動清單，或單一內容執行緒上最近活動的清單
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

已登入社群成員的活動（例如張貼至論壇或部落格）會收集到資料流中，可透過活動資料流元件的設定以各種方式篩選和顯示。

當社群成員關注感興趣的張貼或其他社群成員時，關注功能會新增另一組活動。

全部 [社群網站](/help/communities/overview.md#communitiessites) 加入已登入成員的使用者設定檔頁面，以相同方式顯示成員活動。

## 概念 {#concepts}

一個 *活動資料流* 是成員最近執行的活動清單，或是單一內容對話串（例如論壇主題或部落格）上最近活動的清單。

成員可以跟隨活動資料流，方法是跟隨其他個人或內容。

A *動態消息* 是活動串流後面跟著一個成員合併為單一串流的過程。

A *[社交圖](/help/communities/essentials-socialgraph.md)* 擷取一個成員與另一個成員的下列關係。

## 適用於使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>另請參閱 <a href="/help/communities/activities.md">活動資料流功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](/help/communities/client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [活動串流API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [活動串流接聽程式API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [伺服器端自訂](/help/communities/server-customize.md)

### 活动流功能 {#activity-stream-function}

社群網站結構包含 [活動資料流功能](/help/communities/functions.md#activity-stream-function)，包括已設定的 `activity streams` 元件。
