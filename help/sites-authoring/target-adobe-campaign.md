---
title: 鎖定您的Adobe Campaign
description: 設定細分後，您可以為Adobe Campaign建立鎖定目標的體驗。
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 鎖定您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定您的Adobe Campaign電子報，您必須先設定分段，而這僅在傳統UI （適用於使用者端內容）中可用。 之後，您就可以建立Adobe Campaign的鎖定目標體驗。 本節將說明這兩者。

## 在AEM中設定分段 {#setting-up-segmentation-in-aem}

若要設定區段，您必須使用傳統UI來設定區段。 其餘步驟可以在標準UI中執行。

設定細分包括建立區段、品牌、行銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 開啟 [分段主控台](http://localhost:4502/miscadmin#/etc/segmentation) 於 **&lt;host>：&lt;port>/miscadmin#/etc/segment**.
1. 建立新頁面並輸入標題 — 例如， **AC區段** — 並選取 **區段(Adobe Campaign)** 範本。
1. 在左側的樹狀檢視中選取建立的頁面。
1. 建立區段，例如鎖定男性使用者，方法是在您建立的區段下建立一個名為「男性」的新頁面，然後選取 **區段(Adobe Campaign)** 範本。
1. 開啟已建立的區段頁面，並拖放 **區段ID** 從sidekick到頁面。
1. 連按兩下特徵，輸入ID，在此例中代表Adobe Campaign中定義的男性區段 — 例如， **男性**  — 並按一下 **確定**. 應會顯示下列訊息： *`targetData.segmentCode == "MALE"`*
1. 對另一個區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌 {#creating-a-brand}

若要建立品牌：

1. 在 **網站**，導覽至 **行銷活動** 資料夾（例如在We.Retail中）。
1. 按一下 **建立頁面** 並輸入頁面的標題，例如We.Retail Brand，然後選取 **品牌** 範本。

### 创建活动 {#creating-a-campaign}

若要建立行銷活動：

1. 開啟 **品牌** 您剛才建立的頁面。
1. 按一下 **建立頁面** 並輸入頁面的標題，例如We.Retail Campaign，然後選取 **Campaign** 範本並按一下 **建立**.

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟 **Campaign** 您剛才建立的頁面。
1. 按一下「 」，為您的區段建立體驗 **建立頁面** 並輸入頁面的標題，例如，當您為「男性」區段建立體驗時，請選取 **體驗** 範本。
1. 開啟已建立的體驗頁面。
1. 按一下 **編輯**，然後按一下「區段」下方的 **新增專案**.
1. 輸入男性區段的路徑，例如 **/etc/segmentation/ac-segments/male** 並按一下 **確定**. 應會顯示下列訊息： *體驗鎖定目標：男性*
1. 重複上述步驟，為所有區段（例如女性目標）建立體驗。

## 建立具有目標內容的新聞稿 {#creating-a-newsletter-with-targeted-content}

建立區段、品牌、行銷活動和體驗後，您可以建立具有目標內容的新聞稿。 建立體驗後，您可以將體驗連結至區段。

>[!NOTE]
>
>[電子郵件範例僅適用於Geometrixx](/help/sites-developing/we-retail.md). 請從「封裝共用」下載範例Geometrixx內容。

若要建立具有目標內容的Newsletter：

1. 建立具有目標內容的Newsletter：在Geometrixx Outdoors中的電子郵件促銷活動下方，按一下或點選 **建立** > **頁面**，然後選取其中一個Adobe Campaign郵件範本。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 在Newsletter中，新增文字和個人化元件。
1. 將文字新增至「文字與個人化」元件，例如「這是預設值」。
1. 按一下旁邊的箭頭 **編輯** 並選取 **目標定位**.
1. 從「品牌」下拉式選單中選取您的品牌，然後選取您的Campaign。 （這是您先前建立的品牌和行銷活動）。
1. 按一下 **開始定位**. 您會看到您的區段出現在「對象」區域中。 如果沒有相符的已定義區段，則會使用預設體驗。

   >[!NOTE]
   >
   >根據預設，AEM隨附的電子郵件範例會使用Adobe Campaign作為目標定位引擎。 針對自訂電子報，您可能需要選取Adobe Campaign作為定位引擎。 鎖定目標時，點選或按一下工具列中的「+」，輸入新活動的標題，然後選取 **Adobe Campaign** 作為目標定位引擎。

1. 按一下 **預設** 然後是您新增的文字和個人化元件，您會看到裡面有箭頭的靶心。 按一下圖示以鎖定此元件。

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. 導覽至另一個區段（男性），然後按一下 **新增優惠方案** 並按一下加號圖示+。 然後編輯選件。
1. 導覽至另一個區段（女性）並按一下 **新增優惠方案** 和加號圖示+。 然後編輯此選件。
1. 按一下 **下一個** 若要檢視對應，請按一下 **下一個** 若要檢視未套用至Adobe Campaign的設定，請按一下 **儲存**.

   當內容用於Adobe Campaign內的傳遞時，AEM會自動為Adobe Campaign產生正確的鎖定目的碼

1. 在Adobe Campaign中建立您的傳遞 — 選取 **包含AEM內容的電子郵件傳遞** 並視情況選取本機AEM帳戶，然後確認您的變更。

   在HTML檢視中，Adobe Campaign鎖定目標程式碼會包含目標元件的不同體驗。

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >如果您也在Adobe Campaign中設定區段，請按一下 **預覽** 將顯示每個區段的體驗。
