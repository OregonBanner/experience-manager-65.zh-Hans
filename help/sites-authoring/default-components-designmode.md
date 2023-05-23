---
title: 在設計模式中設定預設元件
description: 在設計模式中設定元件
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 4%

---

# 在設計模式中設定預設元件{#configuring-components-in-design-mode}

當現成安裝AEM執行個體時，元件瀏覽器中會立即提供一組元件選擇。

除了這些以外，您也可以使用其他各種元件。 您可以使用設計模式來 [啟用/停用此類元件](#enable-disable-components). 啟用並位於您的頁面時，您可以使用設計模式來 [設定元件設計的各個方面](#configuring-the-design-of-a-component) 藉由編輯屬性引數。

>[!NOTE]
>
>編輯這些元件時務必謹慎。 設計設定通常是整個網站設計中不可或缺的一部分，因此只有具有適當許可權和經驗的人才能加以變更，通常是管理員或開發人員。 另請參閱 [開發元件](/help/sites-developing/components.md) 以取得詳細資訊。

>[!NOTE]
>
>設計模式僅適用於靜態範本。 使用可編輯範本建立的範本應使用進行編輯 [範本編輯器](/help/sites-authoring/templates.md).

>[!NOTE]
>
>設計模式僅適用於儲存為( `/etc`)。
>
>從AEM 6.4開始，建議將設計儲存為下的設定資料 `/apps` 以支援連續部署情境。 設計儲存在 `/apps` 在執行階段不可編輯，且這類範本的非管理員使用者將無法使用設計模式。

這涉及新增或移除頁面段落系統中允許的元件。 段落系統( `parsys`)是包含所有其他段落元件的複合元件。 段落系統可讓作者將不同型別的元件新增至頁面，因為它包含所有其他段落元件。 每個段落型別都表示為一個元件。

例如，產品頁面的內容可能包含包含以下內容的段落系統：

* 產品的影像（以影像或文欄位落的形式）
* 產品說明（以文欄位落顯示）
* 含有技術資料的表格（作為表格段落）
* 使用者填寫的表單（表單開頭、表單元素和表單結尾段落）

>[!NOTE]
>
>另請參閱 [開發元件](/help/sites-developing/components.md) 和 [使用範本和元件的准則](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 如需更多關於 `parsys`.

>[!CAUTION]
>
>若要定義靜態範本的設計，建議使用本文所述的「設計模式」編輯設計
>
>例如，在CRX DE中修改設計不是最佳做法，此類設計的應用可能與預期行為不同。 檢視開發人員檔案 [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) 以取得詳細資訊。

## 啟用/停用元件 {#enable-disable-components}

啟用或停用元件：

1. 選取 **設計** 模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 點選或按一下元件。 選取時，元件會有藍色邊框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 按一下或點選 **父級** 圖示。

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   這將會選取包含目前元件的段落系統。

1. 此 **設定** 段落系統的圖示將顯示在父項的動作列中。

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   選取此選項以顯示對話方塊。

1. 使用對話方塊可定義編輯目前頁面時元件瀏覽器中可用的元件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   此對話方塊有兩個標籤：

   * 允许的组件
   * 设置

   **允许的组件**

   於 **允許的元件** 標籤，定義哪些元件可用於parsys。

   * 元件會依其元件群組分組，可展開和收合這些元件。
   * 透過勾選群組名稱，可以選取整個群組，而取消勾選則可以取消選取所有群組。
   * 減號表示至少選取了一個群組中的專案，但並未選取所有專案。
   * 搜尋可依名稱篩選元件。
   * 无论是否应用了过滤器，组件组名称右侧列出的数字都表示这些组中选定组件的总数。

   您可以按頁面元件定義設定。 如果子頁面使用相同的範本和/或頁面元件（通常對齊），則相同的設定將套用至對應的段落系統。

   >[!NOTE]
   >
   >調適型表單元件可在調適型表單容器內運作，以運用Forms生態系統。 因此，這些元件必須僅在最適化表單編輯器中使用，且在網站頁面編輯器中無法運作。

   **设置**

   於 **設定** 索引標籤您可以定義其他選項，例如為每個元件繪製錨點，以及定義每個容器的儲存格邊距。

1. 選取 **完成** 以儲存您的設定。

## 設定元件設計 {#configuring-the-design-of-a-component}

1. 選取 **設計** 模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 點選或按一下具有藍色邊框的元件。 在此範例中，選取了主圖影像元件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用 **設定** 圖示以開啟對話方塊。

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在「設計」對話方塊中，您可以根據可用的設計引數來設定元件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   此對話方塊有三個索引標籤：

   * 主要
   * 功能
   * 样式

   **属性**

   此 **屬性** 索引標籤可讓您設定元件的重要設計引數。 例如，對於影像元件，您可以定義影像允許的大小上限和最小值。

   **功能**

   此 **功能** 索引標籤可讓您啟用或停用元件的其他功能。 例如，對於影像元件，您可以定義影像的方向、可用的裁切選項，以及是否可以上傳影像。

   **样式**

   此 **樣式** 索引標籤可讓您定義要與元件搭配使用的CSS類別和樣式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用 **新增** 按鈕來新增其他專案至多重專案對話方塊清單。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   使用**刪除**圖示從多專案對話方塊清單中移除專案。

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用 **移動** 圖示可重新排列多專案對話方塊清單中的專案順序。

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 按一下或點選 **完成** 圖示以儲存並關閉對話方塊。
