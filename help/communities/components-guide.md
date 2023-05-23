---
title: 社群元件指南
seo-title: Community Components Guide
description: 開始使用社交元件架構(SCF)的互動式開發工具
seo-description: An interactive development tool to get started with the social component framework (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 2%

---

# 社群元件指南  {#community-components-guide}

社群元件指南是互動式開發工具，適用於 [社交元件架構(SCF)](scf.md). 它提供可用的AEM Communities元件清單，或由多個元件建置的更複雜功能清單。

除了每個元件的基本資訊外，本指南還允許實驗SCF元件/功能的工作方式，以及如何對其進行設定或自訂。

如需與每個元件相關的開發基本資訊的相關資訊，請參閱 [功能和元件要點](essentials.md).

## 快速入门 {#getting-started}

本指南適用於製作(localhost：4502)和發佈(localhost：4503)執行個體的開發安裝。

透過瀏覽來存取「社群元件」網站

* [https://&lt;server>：&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

與Communities元件的互動會根據以下因素而有所不同：

* 伺服器（製作或發佈）。
* 網站訪客是否已登入。
* 如果已登入，則會指派給成員的許可權。
* 無論預設SRP與否， [JSRP](jsrp.md)，正在使用中。

在作者上，若要進入編輯模式，請插入 `editor.html` 或 `cf#` 做為伺服器名稱后的第一個路徑區段：

* 标准 UI:

   [https://&lt;server>：&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 经典 UI:

   [https://&lt;server>：&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>在編輯模式下的作者上，頁面上的連結非作用中。
>
>若要導覽至元件頁面，請先選取預覽模式以啟動連結。
>
>在瀏覽器中顯示元件頁面後，請返回「編輯」模式以開啟元件的編輯對話方塊。
>
>如需一般撰寫資訊，請檢視 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).
>
>若不熟悉AEM，請檢視以下說明檔案： [基本處理](../../help/sites-authoring/basic-handling.md).

### 主页 {#home-page}

本指南提供可在頁面左側預覽和建立原型的SCF元件清單。

在編輯模式的作者執行個體上檢視的元件指南：

![community-component1](assets/community-component1.png)

## 元件頁面 {#component-pages}

從頁面左側的清單中選取元件。

![社群 — 元件 — 頁面](assets/community-component2.png)

指南的主體隨即顯示：

1. 標題：所選元件的名稱
1. [使用者端程式庫](#client-side-libraries)：一或多個必要類別的清單
1. [包含](scf.md#add-or-include-a-communities-component)：如果可動態包含元件，則可在作者編輯模式中切換狀態：

   * 如果新增，顯示的文字會是：「透過其par節點包含此元件」。
   * 如果包含，顯示的文字會是：「此元件是以動態方式包含。」
   * 如果不可包含，則不會顯示任何文字

1. 範例元件或特徵：元件或特徵的活動例證。 如果元件，則可能會隨著索引標籤區段中提供的範本、CSS和資料所做的變更而改變。

>[!NOTE]
>
>從左側進行選取後，當瀏覽器視窗太窄時，元件會顯示在元件清單的下方，而不是旁邊。

### 作者互動 {#author-interactions}

在作者執行個體上使用指南時，可以透過開啟其對話方塊來體驗設定元件的體驗。 有關開發人員的資訊，請參閱 [元件和Feature Essentials](essentials.md) 區段，而對話方塊設定則在 [Communities元件](author-communities.md) 區段供作者使用。

在社群元件指南中，某些元件對話方塊設定會以 [包含](scf.md#add-or-include-a-communities-component) 切換狀態。 若要在使用現有資源或動態包含的資源之間切換，請在編輯模式中選取元件和可包含的文字，然後按兩下以開啟編輯對話方塊：

![community-component3](assets/community-component3.png)

在 **範本** 標籤：

![community-component4](assets/community-component4.png)

* **通过 sling:include 包含子组件**

   如果未勾選，「元件指南」將使用存放庫中的現有資源（jcr節點，是par節點的子節點）。

   * 文字顯示為：「透過其par節點包含此元件」。

   如果勾選，「元件指南」將使用Sling來動態包含子節點的resourceType （非現有資源）的元件。

   * 文字顯示為：「此元件是以動態方式納入。」

   預設為未勾選。

### 發佈互動 {#publish-interactions}

在發佈執行個體上使用本指南時，您可以以網站訪客（未登入）和具有各種許可權的成員身分體驗元件和功能。

>[!NOTE]
>
>請注意，如果SRP預設為 [JSRP](jsrp.md)，則在發佈執行個體上輸入的UGC將只會顯示在發佈上，而且會 *not* 可從以下位置看到： [稽核](moderate-ugc.md) 作者執行個體上的主控台。

## 客户端库 {#client-side-libraries}

每個元件所列的使用者端程式庫(clientlibs)為 *必填* 將元件放置到頁面上時要參照的專案。 clientlibs提供一種方法，用於管理和最佳化在瀏覽器中呈現元件所使用的Javascript和CSS的下載。

如需詳細資訊，請造訪 [Communities元件的Clientlibs](clientlibs.md).

## 模拟 {#impersonation}

在作者執行個體上，如果使用者經常以管理員或開發人員的身分登入，為了以其他使用者身分體驗元件登入，請使用 **[!UICONTROL 模擬]** 按鈕以輸入使用者名稱或從下拉式清單中選取，然後按一下按鈕。 按一下「回覆」以登出並結束模擬。

發佈執行個體不需要模擬。 只要使用登入/登出連結來模擬各種使用者即可，例如 [示範使用者](tutorials.md#demo-users).

## 自訂 {#customization}

啟用後，每個SCF元件都可暫時修改元件的範本、CSS和資料，為可能的自訂專案建立原型。

### 啟用自訂 {#enabling-customization}

>[!NOTE]
>
>**此工具為唯讀**. 對範本、CSS或資料所做的任何編輯都不會儲存至存放庫。

若要快速實驗自訂，請 `scg:showIde`屬性必須新增至元件頁面的內容JCR節點，並設定為true。

以註釋元件為例，在作者或發佈執行個體上，以管理員許可權登入：

1. 瀏覽至 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   例如， [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 選取元件的 `jcr:content` 節點

   例如，`/content/community-components/en/comments/jcr:content`

1. 新增屬性

   * **名称** `scg:showIde`
   * **类型** `String`
   * **值** `true`

1. 選取 **[!UICONTROL 全部儲存]**
1. 重新載入指南中的「註解」頁面

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 請注意，範本、CSS和資料現在有3個索引標籤。

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### 範本標籤 {#templates-tab}

選取範本標籤以檢視與元件相關聯的範本。

範本編輯器可編譯本機編輯，並將其套用至頁面頂端的範例元件執行個體，而不會影響存放庫中的元件。

在本機編輯時執行編譯，將藉由在排水槽中放置點並將文字標示為紅色來反白顯示任何錯誤。

### CSS索引標籤 {#css-tab}

選取CSS索引標籤以檢視與元件相關聯的CSS。

如果元件是多個元件的組合，則某些CSS可能會列在其他某個元件下。

CSS編輯器可修改CSS，並將其套用至頁面頂端的範例元件例項。

您可以選取規則，按一下排水槽中規則旁的，以反白使用該規則的DOM部分。

### 資料標籤 {#data-tab}

選取「資料」標籤以顯示.social.json端點資料。 此資料可編輯，且已套用至範例元件例項。

語法錯誤可能會標示在gutter中，並在編輯器中反白顯示。
