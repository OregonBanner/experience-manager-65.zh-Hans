---
title: 排行榜功能
seo-title: Leaderboard Feature
description: 新增排行榜元件至頁面
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# 排行榜功能 {#leaderboard-feature}

## 简介 {#introduction}

此 `Leaderboard` 元件可讓使用者根據獲得的點數（基本評分）或專長（進階評分）來排名成員，藉此瞭解成員在社群內的互動方式。

在頁面上加入排行榜元件之前，必須先設定 [社群評分和預算](/help/communities/implementing-scoring.md).

本檔案的這一節將說明：

* 新增 `Leaderboard` 元件至 [社群網站](/help/communities/overview.md#community-sites).
* 的組態設定 `Leaderboard` 元件。

### 新增排行榜至頁面 {#adding-a-leaderboard-to-a-page}

若要新增 `Leaderboard` 元件至作者模式下的頁面，找到元件

* `Communities / Leaderboard`

並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當元件首次放置於社群網站的頁面時，以下是元件的顯示方式：

![排行榜](assets/leaderboard.png)

### 設定排行榜 {#configuring-leaderboard}

選取已放置的 `Leaderboard` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 設定索引標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤中，指定與顯示之成員相關的資訊：

* **显示名称**

   為展示板顯示的描述性名稱，反映為顯示徽章和分數而選取的規則。
預設為 `Leaderboard`，則不會輸入任何內容。

* **徽章**

   如果勾選，則排行榜會包含徽章圖示欄。
預設為未勾選。

* **徽章名称**

   如果勾選，則排行榜會包含徽章名稱的欄。
預設為未勾選。

* **使用頭像**

   如果勾選，成員的頭像影像會包含在排行榜中，位於其名稱連結至成員個人檔案的旁邊。
預設為未勾選。

#### 規則標籤 {#rules-tab}

在 **規則** 標籤、社群網站及其評分和徽章規則

* **规则位置**

   （必要）評分/徽章規則的設定位置。

* **评分规则**

   （必要）產生要顯示之分數的特定規則。

* **徽章规则**

   （必要）產生要顯示之徽章的特定規則。

* **显示限制**

   每頁顯示的成員數目。預設為10。

### 範例：參與者排行榜 {#example-participants-leaderboard}

此排行榜會報告套用基本評分規則的結果。

排行榜元件設定：

* 設定標籤：

   * 显示名称 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名称
      * 使用頭像

* 規則標籤：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules//reference-badging`
   * 显示限制 = `10`

![參與者 — 排行榜](assets/participants-leaderboard.png)

### 範例：專家排行榜 {#example-experts-leaderboard}

此排行榜會報告套用進階評分規則的結果。

排行榜元件設定：

* 設定標籤：

   * 显示名称 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用頭像

* 規則標籤：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 显示限制 = `10`

![experts-leaderboard](assets/experts-leaderboard.png)

### 附加信息 {#additional-information}

如需詳細資訊，請參閱 [排行榜要點](/help/communities/leaderboard.md) 適用於開發人員的頁面。

建立規則的指示見 [社群評分和預算](/help/communities/implementing-scoring.md) 管理員頁面。
