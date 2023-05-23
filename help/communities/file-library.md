---
title: 檔案庫功能
seo-title: File Library Feature
description: 檔案庫功能可讓登入的網站訪客上傳、管理和下載檔案
seo-description: The File Library feature lets signed-in site visitors upload, manage, and download files
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 7%

---

# 檔案庫功能{#file-library-feature}

## 简介 {#introduction}

檔案庫功能為登入網站訪客（社群成員）提供在社群網站內上傳、管理和下載檔案的位置。

本檔案的這一節將說明：

* 將檔案庫功能新增至AEM網站。
* 的組態設定 `File Library` 元件。

### 新增檔案程式庫至頁面 {#adding-a-file-library-to-a-page}

若要新增 `File Library` 元件至作者模式下的頁面，找到元件：

* `Communities / File Library`

並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/essentials-file-library.md#essentials-for-client-side) 包含，這就是 `File Library` 元件將會出現：

![file-library1](assets/file-library1.png)

### 設定檔案庫 {#configuring-file-library}

選取已放置的 `File Library` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 評論索引標籤 {#comments-tab}

在 **註解** 索引標籤中，指定是否要顯示已上傳檔案的註解及顯示方式：

* **允许对文件发表评论**

   如果勾選，則允許對上傳的檔案發表評論。 預設為未勾選。

* **每页的评论数**

   限制每頁顯示的評論數以及顯示的回複數。 預設為 **10**.

* **最大文件大小**

   此值將限制上傳的檔案大小。 預設限製為104857600 (10 Mb)。

* **最大消息长度**

   可在文字方塊中輸入的最大字元數。 預設為4096個字元。

* **允许的文件类型**

   以「點」分隔符號分隔的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則不允許未指定的檔案型別。 並未指定預設值，因此允許所有檔案型別。

* **富文本编辑器**

   如果勾選，則可以使用標籤輸入註釋。 預設為未勾選。

* **删除评论**

   如果勾選，則允許使用者刪除自己的評論。 預設為已核取。

* **允许标记**

   如果勾選，則會啟用將標籤新增至檔案的功能。 預設為未勾選。

* **允许的命名空间**

   如果勾選「允許標籤」，則可用標籤將限製為已勾選的名稱空間。 如果未勾選任何專案，則允許全部勾選。 預設為所有名稱空間。

* **建议限制**

   如果勾選「允許標籤」，此設定會限制要顯示的建議標籤數量。 如果設為–1，則沒有限制。 預設值為–1。

* **允许投票**

   如果勾選，將會啟用為檔案投票的功能。 預設為未勾選。

* **允许关注**

   如果勾選，請在部落格中加入以下功能，讓成員能夠 [已通知](/help/communities/notifications.md) 新貼文數量。 預設為未勾選。

* **启用提及功能**

   啟用後，可讓註冊社群使用者識別其他註冊成員（使用名字、姓氏、使用者名稱），並使用通用@user-name語語法標籤這些成員。 標籤的使用者會收到有關其提及的通知。

* **最大提及次数**

   限制貼文中允許提及的最大數量。 預設值為10。

* **UI 提及模式**

   指定允許的模式字串，以在貼文中標籤(@mention)註冊使用者。 例如~{{familyName}}{{givenName}}.

* **允许主题回复**

   如果勾選，則允許回覆已發佈的評論。 預設為未勾選。

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **使用者稽核** 索引標籤中，如果允許評論，則設定評論的稽核：

* **预审**

   如果勾選，註解必須先獲得核准，才會出現在發佈網站上。 預設為未勾選。

* **删除评论**

   如果勾選，發表評論的訪客將獲得刪除評論的功能。 預設為已核取。

* **拒絕評論**

   如果勾選，則允許受信任的成員版主拒絕評論。 預設為未勾選。

* **關閉/重新開啟註解**

   如果勾選，則允許受信任的成員版主關閉和重新開啟註解。 預設為未勾選。

* **標幟評論**

   如果勾選，則允許訪客將評論標幟為不適當。 預設為未勾選。

* **標幟原因清單**

   如果勾選，則允許訪客從下拉式清單中選擇將評論標幟為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

   如果勾選，則允許訪客輸入將評論標幟為不適當的原因。 預設為未勾選。

* **稽核臨界值**

   輸入在通知版主之前，訪客必須標籤評論的次數。 預設為一次(**1**)。

* **標幟限制**

   輸入在將評論從公開檢視隱藏之前必須將其標幟的次數。 此數字必須大於或等於 **稽核臨界值**. 預設值為5。

### 排序設定索引標籤 {#sort-settings-tab}

排序方式

设置为默认

### 附加信息 {#additional-information}

如需詳細資訊，請參閱 [檔案程式庫程式集](/help/communities/essentials-file-library.md) 適用於開發人員的頁面。

有關張貼主題和評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤張貼的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
