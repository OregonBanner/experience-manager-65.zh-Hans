---
title: 傳統UI標籤控制檯
seo-title: Classic UI Tagging Console
description: 瞭解傳統UI標籤控制檯。
seo-description: Learn about the Classic UI Tagging Console.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 傳統UI標籤控制檯{#classic-ui-tagging-console}

本節內容適用於Classic UI標籤控制檯。

觸控最佳化的UI標籤控制檯是 [此處](/help/sites-administering/tags.md#tagging-console).

若要存取Classic UI標籤控制檯：

* 於作者
* 以管理許可權登入
* 瀏覽至主控台，例如， [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 建立標籤和名稱空間 {#creating-tags-and-namespaces}

1. 根據您開始的層級，您可以使用以下專案建立標籤或名稱空間： **新增**：

   如果您選取 **標籤** 您可以建立名稱空間：

   ![](assets/creating_tags_andnamespaces.png)

   如果您選取名稱空間(例如 **示範**)您可以在該名稱空間中建立標籤：

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在這兩種情況下，請輸入

   * **标题**
(
*必填*)標籤的顯示標題。 雖然可以輸入任何字元，但建議您不要使用這些特殊字元：

      * `colon (:)`  — 名稱空間分隔符號
      * `forward slash (/)`  — 子標籤分隔符號

      如果輸入，這些字元將不會顯示。

   * **名称**
(
*必填*)標籤的節點名稱。

   * **描述**
(
*可選*)標籤的說明。

   * 選取 **建立**


## 編輯標籤 {#editing-tags}

1. 在右側窗格中，選取您要編輯的標籤。
1. 按一下 **編輯**.
1. 您可以修改 **標題** 和 **說明**.
1. 按一下 **儲存** 以關閉對話方塊。

## 刪除標籤 {#deleting-tags}

1. 在右窗格中，選取您要刪除的標籤。
1. 单击&#x200B;**删除**。
1. 按一下 **是** 以關閉對話方塊。

   標籤不應再列出。

## 啟用和停用標籤 {#activating-and-deactivating-tags}

1. 在右側窗格中，選取您要啟用（發佈）或停用（取消發佈）的名稱空間或標籤。
1. 按一下 **啟動** 或 **停用** 視需要。

## 清單 — 顯示參照標籤的位置 {#list-showing-where-tags-are-referenced}

**清單** 開啟新視窗，顯示使用反白標籤的所有頁面的路徑：

![](assets/list_showing_wheretagsarereferenced.png)

## 移動標籤 {#moving-tags}

為協助標籤管理員和開發人員清理分類或重新命名標籤ID，可以將標籤移動到新位置：

1. 開啟 **標籤** 主控台。
1. 選取標籤並按一下 **移動……** 在頂端工具列中（或前後關聯功能表中）。
1. 在 **移動標籤** 對話方塊，定義：

   * **至**，目的地節點。
   * **重新命名為**，即新節點名稱。

1. 按一下 **移動**.

此 **移動標籤** 對話方塊如下所示：

![](assets/move_tag.png)

>[!NOTE]
>
>作者不應移動標籤或重新命名標籤ID。 必要時，作者只應 [變更標籤標題](#editing-tags).

## 合併標籤 {#merging-tags}

分類法有重複專案時，可使用合併標籤。 當標籤A合併到標籤B時，所有使用標籤A的頁面都將使用標籤B標籤，並且標籤A不再可供作者使用。

若要將標籤合併至另一個標籤：

1. 開啟 **標籤** 主控台。
1. 選取標籤並按一下 **合併……** 在頂端工具列中（或前後關聯功能表中）。
1. 在 **合併標籤** 對話方塊，定義：

   * **到**，目的地節點。

1. 按一下 **合併**.

此 **合併標籤** 對話方塊如下所示：

![](assets/mergetag.png)

## 計算標籤的使用量 {#counting-usage-of-tags}

若要檢視某個標籤的使用次數：

1. 開啟 **標籤** 主控台。
1. 按一下 **計數使用情況** 在頂端工具列中：計數欄會顯示結果。

## 管理不同語言的標籤 {#managing-tags-in-different-languages}

選填 `title`標籤的屬性可翻譯成多種語言。 標籤 `titles` 然後可以根據使用者語言或頁面語言顯示。

### 定義多種語言的標籤標題 {#defining-tag-titles-in-multiple-languages}

下列程式說明如何翻譯 `title`標籤的 **動物** 英文、德文和法文：

1. 前往 **標籤** 主控台。
1. 編輯標籤 **動物** 以下 **標籤** > **Stock Photography**.
1. 新增以下語言的翻譯：

   * **英文**：動物
   * **德文**：地標
   * **法文**：Animaux

1. 保存更改。

對話方塊如下所示：

![](assets/edit_tag.png)

「標籤」控制檯會使用使用者語言設定，因此對於Animal標籤，會針對在使用者屬性中將語言設定為法文的使用者顯示「Animaux」。

若要新增語言至對話方塊，請參閱區段 [新增語言至編輯標籤對話方塊](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 在 **為開發人員加上標籤** 區段。

### 以指定語言在頁面屬性中顯示標籤標題 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

依預設，標籤 `titles`在中，頁面屬性會以頁面語言顯示。 頁面屬性中的標籤對話方塊有一個可顯示標籤的語言欄位 `titles`使用不同語言。 下列程式說明如何顯示標籤 `titles`法文：

1. 請參閱上一節，將法文翻譯新增至 **動物** 以下 **標籤** > **Stock Photography**.
1. 開啟的頁面屬性 **產品** 的英文分支中的頁面 **Geometrixx** 網站。
1. 開啟 **標籤/關鍵字** 對話方塊（選取「標籤/關鍵字」顯示區域右側的下拉式功能表），然後選取 **法文** 從右下角的下拉式選單中選取語言。
1. 使用左右箭頭捲動，直到能夠選取 **Stock Photography** 標籤

   選取 **動物** (**Animaux**)，並選取對話方塊外部以關閉它，並將標籤新增至頁面屬性。

   ![](assets/french_tag.png)

依預設，「頁面屬性」對話方塊會顯示標籤 `titles`根據頁面語言。

一般而言，如果頁面語言可用，則會從頁面語言取得標籤的語言。 當 [ `tag` Widget](/help/sites-developing/building.md#tagging-on-the-client-side) 在其他情況下使用（例如在表單或對話方塊中），標籤語言取決於上下文。

>[!NOTE]
>
>標準頁面元件中的標籤雲和中繼關鍵字會使用當地語系化的標籤 `titles`根據頁面語言（如果可用）。
