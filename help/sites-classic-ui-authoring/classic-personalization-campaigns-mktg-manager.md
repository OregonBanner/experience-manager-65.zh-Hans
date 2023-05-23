---
title: 使用行銷活動管理員
seo-title: Working with the Marketing Campaign Manager
description: 行銷活動管理員(MCM)主控台可協助您管理多管道行銷活動。 使用此行銷自動化軟體，您可以管理所有品牌、行銷活動和體驗，以及相關區段、清單、銷售機會和報表。
seo-description: The Marketing Campaign Manager (MCM) is a console that helps you manage multi-channel campaigns. With this marketing automation software you can manage all your brands, campaigns and experiences together with the related segments, lists, leads, and reports.
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
exl-id: 0e13112b-d9df-4ba6-bd73-431c87890b79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 使用行銷活動管理員{#working-with-the-marketing-campaign-manager}

在AEM中，行銷活動管理員(MCM)是協助您管理多頻道行銷活動的主控台。 使用此行銷自動化軟體，您可以管理所有品牌、行銷活動和體驗，以及相關區段、清單、銷售機會和報表。

您可以從AEM中的不同位置存取MCM；例如，「歡迎」畫面，使用「促銷活動」圖示或URL：

`https://<hostname>:<port>/libs/mcm/content/admin.html`

例如：

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

您可以從MCM存取：

* **[儀表板](#dashboard)**
這分為四個窗格：

   * [清單](#lists)
此窗格會顯示您已建立的清單，以及該清單中的潛在客戶數量。 您可以從此窗格直接建立新清單，或匯入銷售機會以建立新清單。
選取特定清單後，您將會前往 [清單](#lists) 區段會顯示您清單的詳細資訊。

   * [區段](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)
此窗格會顯示您定義的區段。 區段可讓您為共用特定特徵的訪客集合設定特徵。
選取特定區段將會開啟區段定義頁面。

   * [報表](/help/sites-administering/reporting.md)
AEM提供不同的報表，協助您分析和監控執行個體的狀態。 此MCM窗格會列出報表。
選取報告會開啟報告頁面。

   * [行銷活動](#campaigns)
此窗格會列出您的行銷活動體驗，例如 [電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 和 [Teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers).

* **[銷售機會](#leads)**
您可以在此處管理銷售機會。 您可以建立或匯入銷售機會、編輯個別銷售機會的特定詳細資訊，或在不再需要時刪除。 您也可以將潛在客戶放入不同的群組中，稱為「清單」。 **注意：** Adobe不打算進一步增強此功能。
建議為 [善用Adobe Campaign以及與AEM的整合](/help/sites-administering/campaign.md).

* **[清單](#lists)**
您可以在此處管理您的（潛在客戶）清單。**注意：** Adobe不打算進一步增強此功能。
建議為 [善用Adobe Campaign以及與AEM的整合](/help/sites-administering/campaign.md).

* **[行銷活動](#campaigns)**
您可以在此處管理您的品牌、行銷活動和體驗。

## 仪表板 {#dashboard}

儀表板會顯示四個窗格，為您提供清單（潛在客戶）、區段、報表和行銷活動的概覽。 您也可以在這裡存取這些的基本功能。

![mcm_dashboard](assets/mcm_dashboard.png)

### 潜在客户 {#leads}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售機會）。
>建議善用 [Adobe Campaign與AEM的整合](/help/sites-administering/campaign.md).

在AEM MCM中，您可以手動輸入潛在客戶或匯入逗號分隔的清單（例如郵寄清單）來整理和新增潛在客戶。 產生潛在客戶的其他方式來自電子報註冊或社群註冊（如果設定，這些方式可能會觸發填入潛在客戶的工作流程）。 潛在客戶通常會分類並放入清單中，以便您稍後可以對整個清單執行動作；例如，傳送自訂電子郵件給特定清單。

下 **銷售機會** 在左窗格中，您可以建立、匯入、編輯和刪除銷售機會，然後視需要啟用或停用。 您可以將潛在客戶新增至清單，或檢視其已屬於哪些清單。

>[!NOTE]
>
>另請參閱 [使用銷售機會](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads) 以取得特定工作的詳細資訊。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### 列表 {#lists}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理清單）。
>建議善用 [Adobe Campaign與AEM的整合](/help/sites-administering/campaign.md).

清單可讓您將潛在客戶組織到群組中。 透過清單，您可以將行銷活動鎖定在特定人群中；例如，您可以將目標電子報傳送至清單。

下 **清單**，您可以建立、匯入、編輯、合併及刪除清單，然後視需要啟用或停用這些清單，以管理您的清單。 您也可以檢視該清單中的銷售機會、檢視清單是否為其他清單的成員，或檢視說明。

>[!NOTE]
>
>另請參閱 [使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 以取得特定工作的詳細資訊。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### 营销活动 {#campaigns}

>[!NOTE]
>
>另請參閱 [Teaser和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)， [設定您的行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign) 和 [電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 以取得特定工作的詳細資訊。

若要存取現有行銷活動，請在MCM中按一下 **行銷活動**.

![screen_shot_2012-02-21at11106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **在左窗格中**：此清單包含所有品牌和行銷活動。
只要按一下品牌，就會同時完成以下兩個操作：

   * 展開清單以在左側窗格中顯示所有相關行銷活動；此清單也會顯示每個行銷活動存在的體驗數量。
   * 在右窗格中開啟品牌概觀。

* **在右窗格中**：每個品牌都會顯示圖示（不會顯示歷史行銷活動）。
您可以按兩下這些以開啟品牌概觀。

#### 品牌概觀 {#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

從這裡，您可以：

* 檢視此品牌存在的行銷活動和體驗數量（顯示在左窗格中的數量）。
* 建立 **新增……** 此品牌的行銷活動。

* 變更檢視的時間範圍；選取 **周**， **月** 或 **季度**，使用箭頭來選取特定期間或返回 **今天**.

* 選取行銷活動（在右窗格中）以：

   * 編輯 **屬性……**
   * **刪除** 行銷活動。

* 開啟行銷活動概覽（在右側窗格中按兩下行銷活動，或在左側窗格中按一下滑鼠）。

#### 行銷活動概覽 {#campaign-overview}

針對個別行銷活動，有兩個可用的檢視：

1. **日历视图**

   使用圖示：

   ![](do-not-localize/mcm_iconcalendarview.png)

   這會呈現所有接觸點（灰色）清單，以及連線至該接觸點的體驗水準時間範圍（綠色）：

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   從這裡，您可以：

   * 使用箭頭變更您檢視的時間範圍，或返回 **今天**.

   * 使用 **新增接觸點……** 為現有體驗新增接觸點。

   * 按一下Teaser （在右窗格中）以設定 **準時** 和 **關閉時間**.

1. **列表视图**

   使用圖示：

   ![](do-not-localize/mcm_icon_listview.png)

   這會列出所選行銷活動的所有體驗（例如Teaser和電子報）：

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   從這裡，您可以：

   * 建立 **新增……** 體驗；例如Adobe Target選件、Teaser和電子報。
   * **編輯** 特定Teaser頁面或電子報的詳細資料（也可以使用按兩下）。
   * 定義 **屬性……** 特定的Teaser頁面或電子報。
   * **模擬** 體驗（Teaser頁面或電子報）的外觀和風格。
當模擬頁面開啟時，您可以接著開啟Sidekick以切換到該頁面的編輯模式。

   * **分析……** 為頁面產生的曝光次數。

   * **刪除** 不再需要的專案。
   * **搜尋** （將會搜尋體驗的「標題」欄位）。
   * 使用 **進階** 搜尋以將篩選器套用至搜尋。

### 模擬您的Campaign體驗 {#simulating-your-campaign-experiences}

在MCM中，按一下 **行銷活動**. 確定清單檢視為作用中，然後選取所需的行銷活動體驗並按一下 **模擬**. 接觸點（Teaser或Newsletter頁面）將開啟以顯示您選取的體驗，因為訪客會看到它。

![mcm_simulateexperience](assets/mcm_simulateexperience.png)

您也可以從此開啟Sidekick （按一下小型向下箭頭）以變更為更新頁面的編輯模式。

### 分析您的行銷活動體驗 {#analyzing-your-campaign-experiences}

在MCM中，按一下 **行銷活動**. 確定清單檢視為作用中，然後選取所需的行銷活動體驗並選取 **分析……**. 將會顯示一段時間的頁面印象圖表。

![mcm_campaignanalyze](assets/mcm_campaignanalyze.png)
