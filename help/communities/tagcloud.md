---
title: 使用社交標籤雲
seo-title: Using Social Tag Cloud
description: 將Social Tag Cloud元件新增至頁面
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# 使用社交標籤雲 {#using-social-tag-cloud}

## 简介 {#introduction}

此 `Social Tag Cloud` 元件會醒目提示發佈內容時社群成員套用的標籤。 這是識別趨勢主題並允許網站訪客快速找到標籤內容的方法。

如需其他識別目前趨勢的方法，請造訪 [活動趨勢](trends.md).

本頁會記錄 `Social Tag Cloud` 元件對話方塊設定及說明使用者體驗。

如需開發人員的詳細資訊，請參閱 [標籤Essentials](tag.md).

另請參閱 [管理標籤](../../help/sites-administering/tags.md) 以取得關於建立和管理標籤以及已對哪些內容標籤套用的資訊。

## 新增社交標籤雲端 {#adding-a-social-tag-cloud}

若要新增 `Social Tag Cloud` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Social Tag Cloud` 並將其拖曳至應顯示tag cloud的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](tag.md#essentials-for-client-side) 包含，這就是 `Social Tag Cloud` 元件將會出現：

![社交標籤](assets/social-tag.png)

## 設定社交標籤雲端 {#configuring-social-tag-cloud}

選取已放置的 `Social Tag Cloud` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 社交標籤雲]** 標籤，指定要顯示的標籤，如果標籤是作用中的連結，則指定搜尋結果的頁面位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 要顯示的社交標籤]**
識別要顯示的UGC標籤。 下拉式清單選項包括：

   * `From page and child pages`
   * `All tags`

   預設值為 `From page and child pages`，其中「page」是指 **頁面** 設定於下方。

* **[!UICONTROL 页面]**

   （若非必要，則為必要） `All tags)` 頁面的UGC路徑。 如果保留為空白，預設值為目前頁面。

* **[!UICONTROL 标记上无链接]**

   如果勾選，標籤會以純文字顯示在標籤雲中。 如果未勾選，則標籤會顯示為作用中連結，可在套用該標籤的所有內容上搜尋。 預設為未勾選，且需要 **[!UICONTROL 搜尋結果路徑]** 待設定。

* **[!UICONTROL 搜尋結果路徑]**

   頁面的路徑，該頁面上 `Search Result` 元件已放置，設定為參照UGC，其中包含指定的UGC路徑 **頁面** 設定。

## 變更社交標籤雲端的顯示 {#change-display-of-social-tag-cloud}

若要編輯顯示 **社交標籤雲**，輸入 [設計模式](../../help/sites-authoring/default-components-designmode.md) 並連按兩下置入的 `Social Tag Cloud` 元件以開啟具有額外索引標籤的對話方塊。

使用 **[!UICONTROL 社交標籤雲端（設計）]** 標籤中，指定標籤的顯示方式。 標籤可能是簡單標籤、預設名稱空間中的單一單字，或是階層式分類法：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 显示完整的标题路径]**

   如果勾選，會顯示父標籤的標題和每個套用標籤的名稱空間。

   例如：

   * 已选中: `Geometrixx Media: Gadgets / Cars`
   * 未选中: `Cars`

   簡單標籤沒有區別。

   預設為未勾選。

* **[!UICONTROL 仅显示叶标记]**

   如果勾選，僅顯示不包含其他標籤的已套用標籤。

   例如，假定TagID為：

   `Geometrixx Media: Gadgets / Cars`

   有3個標籤可以套用：

   `Geometrixx Media (the namespace)`, `Gadgets`, 和 `Cars`

   * 已核取：僅限 `Cars` 將會顯示（如果套用）。
   * 未核取： `Geometrixx Media` 和 `Gadgets`以及 `Cars` 將會顯示（如果套用）。

   簡單標籤是葉標籤。

   預設為未勾選。

* **[!UICONTROL 链接模板]**

   透過元件編輯對話方塊啟用連結時，預設以外的範本可用於在標籤雲中顯示連結。

* **[!UICONTROL 所有标记相同尺寸]**

   如果勾選，則標籤雲中的所有字詞的樣式都相同。 如果未勾選，文字會根據其使用方式而採用不同的樣式。 預設為未勾選。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [標籤Essentials](tag.md) 適用於開發人員的頁面。

另請參閱 [標籤使用者產生的內容](tag-ugc.md) (UGC)，以瞭解建立和管理標籤的相關資訊。
