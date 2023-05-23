---
title: 活動趨勢
seo-title: Activity Trends
description: 將社群活動清單元件新增至頁面
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# 活動趨勢 {#activity-trends}

## 简介 {#introduction}

此 `Community Activity List` 元件提供新增成員貼文和檢視的趨勢資訊，以及貼文和內容檢視的功能。

本檔案說明：

* 新增 `Community Activity List` 元件至 [社群網站](/help/communities/overview.md#community-sites).

* 的組態設定 `Community Activity List` 元件。

### 要求 {#requirement}

的資料 `Community Activity List` 只有在Adobe Analytics已獲得授權並針對社群網站進行設定時，才可使用。

另請參閱 [Communities功能的Analytics設定](/help/communities/analytics.md).

### 將社群活動清單新增至頁面 {#adding-a-community-activity-list-to-a-page}

若要新增 `Community Activity List` 元件至作者模式下的頁面，找到元件

* `Communities / Community Activity List`

並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當元件首次放置於社群網站的頁面時，以下是元件的顯示方式：

![社群活動](assets/community-activity.png)

### 設定社群活動清單  {#configuring-community-activity-list}

選取已放置的 `Community Activity List` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **註解** 索引標籤中，指定是否要顯示已上傳檔案的註解及顯示方式：

![属性](assets/activity-list-properties.png)

* **类型**

   指定是否要顯示有關社群成員或使用者產生內容(UGC)的資料。

   從下列專案選取：

   * `Members`
   * `Content`

   預設為 `Members`.

* **显示标题**

   資料上方顯示的描述性標題，例如 `Trending Content`.
預設為無標題。

* **显示数量**

   要列出的專案數。
預設值為10。

* **活动类型**

   選取下列其中一項：

   * `Views`（頁面瀏覽次數）
   * `Posts`（建立UGC）
   * `Follows`
   * `Likes`

   預設為「檢視」。

* **时间段**

   選取下列其中一項：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   預設為 `Total`.

* **上下文路径**

   提供將活動範圍限定為網站子集（例如特定部落格）的功能。
預設為整個社群網站。

* **成员数量整合**

   取消選取（關閉）時，只會計算最上層的貼文。 例如，如果內容是根頁面（預設），則 `Activity Type` 之 `Posts` 永遠不會顯示任何活動，因為無法將內容發佈到根頁面。 如果勾選，則會包含所有下級頁面上的計數。
預設為已核取。

### 包含4個元件的範例頁面 {#example-page-with-components}

**排名在前的訪客** config：型別=成員，活動型別=檢視

**主要貢獻者** config：型別=成員，活動型別=貼文

**熱門內容** 設定：型別=內容，活動型別=檢視，

**趨勢內容** config： Type = Content， Activity type = Posts

![元件](assets/activity-list-components.png)
