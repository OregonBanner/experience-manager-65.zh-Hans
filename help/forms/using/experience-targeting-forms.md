---
title: 在AEM Forms中建立鎖定目標的體驗
seo-title: Create targeted experiences in AEM Forms
description: 在AEM Forms中使用Target，為鎖定目標客戶建立自訂體驗。
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 在AEM Forms中建立鎖定目標的體驗 {#create-targeted-experiences-in-aem-forms}

## 將Adobe Target與AEM Forms整合 {#integrate-adobe-target-with-aem-forms}

Adobe Target與AEM整合，可讓您建立針對目標對象自訂的體驗。 透過Adobe Target，您可以建立A/B測試、測量使用者回應，並為目標使用者產生自訂的網頁內容。 您可以整合Adobe Target與AEM Forms，以針對最適化表單和互動式通訊的影像元件。

在AEM中設定Adobe Target以搭配最適化表單和互動式通訊使用，請參閱 [在AEM中建立Target設定](/help/sites-administering/target.md) 和 [新增框架](/help/sites-administering/target.md).

>[!NOTE]
>
>使用主機名稱或IP位址呈現最適化表單或互動式通訊時，鎖定目標就會運作。 使用localhost轉譯最適化表單或互動式通訊時，它會失敗。

## 建立Target活動 {#creating-a-target-activity}

1. 點選 **Adobe Experience Manager >個人化>活動**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在「活動」頁面中，點選 **建立>建立品牌**.
1. 系統會要求您選擇範本並輸入屬性。

   選取範本，點選 **下一個。** 在屬性區段中輸入品牌標題，然後點選 **建立。**
您的品牌現在已列在活動頁面中。

1. 在「活動」頁面中點選您的品牌。
1. 在品牌的主區域點選 **建立** > **建立活動**.

   建立活動時，您可以指定其詳細資訊、目標和設定。

   「詳細資訊」區段包含名稱、目標定位引擎和目標。 當您選取Adobe Target作為定位引擎時，就會啟用Target雲端設定選項。 選擇您的Target雲端設定、選擇活動型別、提供活動目標，然後點選 **下一個**. 互動式通訊僅支援體驗鎖定目標活動型別。

   Target區段可讓您新增對象體驗並將其命名。 按一下 **新增體驗** 以啟用 **選取對象** 和 **為體驗命名** 選項。 點選 **選取對象** 檢視對象及其來源的清單。 從「對象名稱」清單中選取對象。 點選 **新增體驗** 為體驗命名，然後點選 **下一個**.

   「目標與設定」區段可讓您排程活動並排定其優先順序。 設定活動的開始日期、結束日期和優先順序、目標量度、其他量度和點選 **儲存**.

   活動現在會列在您的品牌頁面中。

   >[!NOTE]
   >
   >您可以忽略錯誤「您的活動已儲存，但未同步至Target。 原因：如果在儲存活動時遇到以下體驗「沒有選件」。

1. 若要啟用Target，請編輯.jsp檔案以包含您的最適化表單範本所使用的使用者端資料庫。

   例如，在現成可用的實作中，按一下 **工具** >  **CRXDE Lite**.

   在CRXDE Lite位址列中，輸入/libs/fd/af/components/page/base/head.jsp以編輯head.jsp檔案。

   此實作使用simpleEnrollment範本。 在此實作中，修改head.jsp檔案以包含下列使用者端程式庫：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 若要啟用最適化表單的目標框架，請導覽至您的表單或互動式通訊，並以編輯模式開啟它。

   若要以編輯模式開啟表單或互動式通訊，請點選 **選取** 然後點選 **開啟**.

   或者，將指標移到表單或互動式通訊圖示上而不選取時，會出現四個按鈕。 您可以點選 **編輯** 按鈕，以在編輯模式中開啟表單。

1. 在頁面工具列中點選 **頁面資訊** ![theme-options](assets/theme-options.png) > **開啟屬性**.
1. 在「一般」標籤中，選擇 **Adobe Target** 欄位。 點選 **儲存並關閉**.

## 將建立的活動套用至最適化表單影像或互動式通訊影像 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 開啟最適化表單和互動式通訊以進行編輯。 如果您要開啟互動式通訊，請開啟Web Channel。

1. 在互動式通訊或最適化表單的製作模式中，新增要鎖定的影像。

   >[!NOTE]
   >
   >AEM Forms僅支援定位影像元件。 確認裝載影像元件的面板未包含任何其他元件，且面板的欄數設為1。

1. 切換來源 **編輯** 至 **目標定位** 模式。 切換模式的選項位於右上角附近。
1. 選取 **品牌**，選取 **活動**，然後點選 **開始定位**. 此 **受眾** 功能表會出現在編輯器的右側。

   ![targeting-menu](assets/targeting-menu.png)

1. 從中選擇對象 **受眾** 功能表，然後點選要定位的影像。 選單出現。 在功能表中，點選 **Target**. 點選影像並點選 **設定**. 在屬性視窗中，選取要針對所選對象顯示的影像。 對所有對象重複此步驟。 互動式通訊或最適化表單中的影像已啟用體驗鎖定目標。

## 檢查建立的活動是否與Target伺服器同步 {#check-if-the-created-activity-syncs-with-the-target-server}

用於鎖定目標與Target伺服器同步的活動。 若要檢查您的活動是否與目標伺服器同步，請在您的品牌頁面中檢查您的活動狀態。

確保活動的狀態為「已同步」。

## 驗證目標行為 {#validate-target-behavior}

若要驗證Target行為：

* 使用目標定位 `wcmmode preview` 在作者模式中
* 使用目標定位 `wcmmode preview` 和 `wcmmode disabled` 在發佈模式中

## 監視影像元件的目標定位 {#monitor-targeting-for-the-image-component}

若要監視表單上影像元件的目標定位，請發佈您的影像、活動和最適化表單。

## 未结问题 {#open-issues}

可見度運算式，針對最適化表單上的目標影像設定焦點失敗。
