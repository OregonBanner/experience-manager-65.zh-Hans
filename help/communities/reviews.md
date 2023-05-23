---
title: 使用稽核和稽核摘要（顯示）
seo-title: Using Reviews and Reviews Summary (Display)
description: 新增複查和複查摘要元件至頁面
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 2%

---

# 使用稽核和稽核摘要（顯示） {#using-reviews-and-reviews-summary-display}

此 `Reviews` 元件是以下專案的組合： [註解](comments.md) 和 [評等](rating.md) 元件可供使用。

此 `Reviews Summary (Display)` 元件提供作用中或已關閉之執行個體的摘要， `Reviews` 在網站上其他位置顯示的元件。

>[!NOTE]
>
>不支援評論的匿名張貼。 網站訪客必須註冊（成為會員）並登入才能參與。 已登入的訪客可隨時更新其評論。

## 新增複查至頁面 {#adding-a-review-to-a-page}

若要新增 `Reviews` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Reviews` 並將其拖曳至頁面上某個位置，例如與功能相對的位置以供使用者檢閱。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](reviews-basics.md#essentials-for-client-side) 包含，這就是 `Reviews` 元件隨即出現。

![create-review](assets/create-review.png)

## 設定稽核 {#configuring-reviews}

選取已放置的 `Reviews` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 允許的評等]** 索引標籤中，指定要顯示給成員的完整評等清單。 第一個評等應該是整體/一般評等，因為它是提供以下專案的平均評等的評等： `Review Summary (Display)` 元件。 預設設定中的下兩個評等應該給予不同的標題，「Subrating 1」或「Subrating 2」除外。

![允許評等](assets/configure-review1.png)

* **[!UICONTROL 允许的评级]**

   成員可選擇的評等清單。

   使用向上鍵、向下鍵和刪除按鈕來修改可見選取專案。

   按一下 **[!UICONTROL 新增專案]** 以新增其他評等選擇。

在 **[!UICONTROL 必要的評等]** 標籤，從清單重新輸入專案 **[!UICONTROL 允許的評等]** 需要評等的。 如果專案僅在「允許的評等」標籤上指定，則當成員提交時，該專案可能會保持未標籤狀態。

在網站上，必要的評等會以星號標示。 如果專案為必要專案且未標籤，則會向成員顯示訊息，並拒絕提交，直到標籤完所有必要的評等為止。

![required-rating](assets/configure-review2.png)

* **[!UICONTROL 所需的评级]**

   允許的評等子集，指出所需的評等。

   使用向上鍵、向下鍵和刪除按鈕來修改可見選取專案。

   按一下 **[!UICONTROL 新增專案]** 以新增其他回應選擇。

>[!NOTE]
>
>若專案輸入於 **[!UICONTROL 必要的評等]** 標籤上未指定的 **[!UICONTROL 允許的評等]** 索引標籤中，則不會包含在要評級的專案中。

在 **[!UICONTROL 評論]** 索引標籤中，指定如何處理稽核。

![审核](assets/configure-review3.png)

* **[!UICONTROL 允許回覆]**

   如果勾選，則允許回複稽核。 預設為未勾選。

* **[!UICONTROL 已关闭]**

   如果勾選，則新評論和回覆將關閉審閱。 預設為未勾選。

* **[!UICONTROL 允许文件上传]**

   如果勾選，則允許上傳檔案附件以供稽核。 預設為未勾選。

* **最大文件大小**

   相關條件僅限於 **[!UICONTROL 允許檔案上傳]** 已勾選。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為10 MB。

* **[!UICONTROL 最大消息长度]**

   可在文字方塊中輸入的最大字元數。 預設為4096個字元。

* **[!UICONTROL 允许的文件类型]**

   相關條件僅限於 **[!UICONTROL 允許檔案上傳]** 已勾選。 以「點」分隔符號分隔的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則不允許未指定的檔案型別。 預設為none，因此允許所有檔案型別。

* **[!UICONTROL 富文本编辑器]**

   如果勾選，可輸入帶有標籤的貼文。 預設為未勾選。

* **[!UICONTROL 允许投票]**

   如果勾選，請為主題加入投票功能。 預設為未勾選。

在 **[!UICONTROL 使用者稽核]** 索引標籤中，指定如何管理已發佈的稽核。 如需詳細資訊，請參閱 [稽核使用者產生的內容](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 预审]**

   如果勾選，則必須先核准稽核，評論才會出現在發佈網站上。 預設為未勾選。

* **[!UICONTROL 刪除評論]**

   如果勾選，發表評論的成員將獲得刪除的能力。 預設為未勾選。

* **[!UICONTROL 拒絕評論]**

   如果勾選，則允許版主拒絕評論。 預設為未勾選。

* **[!UICONTROL 關閉/重新開啟檢閱]**

   如果勾選，則允許版主關閉和重新開啟檢閱。 預設為未勾選。

* **[!UICONTROL 標幟評論]**

   如果勾選，則允許成員將稽核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 標幟原因清單]**

   如果勾選，則允許成員從下拉式清單中選擇將評論標籤為不適當的原因。 預設為未勾選。

* **[!UICONTROL 自訂標幟原因]**

   如果勾選，則允許成員輸入他們自己的理由，將稽核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 稽核臨界值]**

   輸入在通知版主之前，成員必須標幟稽核的次數。 預設為一次(1)。

* **[!UICONTROL 標幟限制]**

   輸入將評論從公開檢視隱藏之前必須標幟的次數。 此數字必須大於或等於 **[!UICONTROL 稽核臨界值]**. 預設值為5。

### 新增檢閱摘要（顯示）至頁面 {#adding-a-review-summary-display-to-a-page}

若要新增 `Reviews Summary (Display)` 元件至作者模式下的頁面，找到元件

* `Communities / Reviews Summary (Display)`

並將其拖曳至將顯示作用中或已關閉評論之摘要的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](reviews-basics.md#essentials-for-client-side) 包含，這就是 `Reviews Summary (Display)`元件隨即出現。

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>「平均」反映所彙總稽核的「允許評等」標籤上所列第一個專案的票數。

### 設定稽核摘要（顯示） {#configuring-reviews-summary-display}

選取已放置的 `Reviews Summary (Display)` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 稽核摘要]** 標籤

![review-summary](assets/configure-review6.png)

* `Review Path`

   輸入或瀏覽至放置的執行個體 `reviews`要摘要的元件，例如，如果新增至 [Geometrixx參與網站，](getting-started.md) 路徑會是：

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果勾選，則包括橫條圖的顯示，指出所摘要的評論中有多少個星級評等。 預設為未勾選。

### 變更為自訂稽核型別 {#changing-to-a-custom-review-type}

「稽核」元件使用「註解系統」。

透過變更「註解資源型別」，註解系統不再使用預設值產生註解的執行個體，而是由開發人員自訂（擴充）的執行個體。

知道自訂資源型別後，請輸入 [設計模式](../../help/sites-authoring/default-components-designmode.md) 並連按兩下置入的 `Comments` 元件以開啟具有額外索引標籤的對話方塊。

在 **[!UICONTROL 資源型別]** 索引標籤中，為以下專案的新執行個體指定自訂resourceType `Comments or Voting` 元件：

![評論投票](assets/configure-review7.png)

* **[!UICONTROL 评论资源类型]**

   導覽至擴充功能的resourceType `comment`/apps中的元件（單一註釋）。 例如：`/apps/social/commons/components/hbs/comments/comment`。

   此資源將識別訪客發表評論時建立的UGC的resourceType。

* **[!UICONTROL 投票资源类型]**

   導覽至擴充功能的resourceType `voting`/apps中的元件。 例如：`/apps/social/components/hbs/voting`。

   此資源將識別訪客張貼投票時建立的UGC資源型別。

* **[!UICONTROL 註解系統資源型別]**

   導覽至擴充功能的resourceType `comments`/apps中的元件（註解系統）。 除非頁面範本，否則保留空白 [動態包含](scf.md#add-or-include-a-communities-component) 基礎指令碼中的「註解系統」，而非以資源（註解節點）的形式新增至頁面。 閱讀以下內容以瞭解更多資訊： [{{include}} 協助程式](handlebars-helpers.md#include).

## 網站訪客體驗 {#site-visitor-experience}

### 版主和管理員 {#moderators-and-administrators}

當登入的使用者具有版主或管理員許可權時，無論審閱的作者是誰，他們都能執行元件設定所允許的版主任務。

### 成员 {#members}

網站訪客登入時，根據設定，他們可能：

* 發表新評論
* 編輯自己的評論
* 刪除自己的評論
* 標示其他人的評論意見

每個成員只允許一個評等。 會員可隨時變更其評等。

### 匿名 {#anonymous}

未登入的網站訪客只能閱讀張貼的評論，並在支援時進行翻譯，但不得新增評等或評論，亦不得標示其他人的評論意見。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [檢閱Essentials](reviews-basics.md) 適用於開發人員的頁面。

有關張貼的評論的稽核，請參閱 [稽核使用者產生的內容](moderate-ugc.md).

如需已張貼評論的翻譯，請參閱 [翻譯使用者產生的內容](translate-ugc.md).
