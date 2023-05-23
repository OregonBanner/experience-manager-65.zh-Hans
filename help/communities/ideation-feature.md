---
title: 創意力功能
seo-title: Ideation Feature
description: 新增和設定創意力功能
seo-description: Adding and configuring the Ideation feature
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 9%

---

# 創意力功能 {#ideation-feature}

## 简介 {#introduction}

創意力功能為發佈環境中的登入網站訪客（社群成員）提供一個區域，以：

* 建立想法並與社群分享。
* 檢視並評論想法。
* 遵循想法。
* 投票支援一個想法。

本檔案的這一節將說明：

* 將創意力功能新增至AEM網站。
* 創意力元件的組態設定。

### 將構思新增至頁面 {#adding-a-ideation-to-a-page}

若要新增 `Ideation` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Ideation`

並將其拖曳至應顯示創意的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/ideation.md#essentials-for-client-side) 包含，這就是 `Ideation` 元件將會出現：

![構思](assets/ideation.png)

### 設定構思 {#configuring-an-ideation}

選取已放置的 `Ideation` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

![創意力設定](assets/ideation-settings.png)

#### 設定索引標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤中，指定想法和評論的設定：

* **允许附加缩略图**
* **附加缩略图时的大小上限**
* **缩略图的最小图像大小**
* **缩略图大小最大值**
* **允许拥有权限的成员**
* **允许的拥有权限的成员**
* **在作者编辑模式下阻止“用户生成内容”**
* **构思标题**

* 想法的顯示標題。 預設為 `Ideation`.
* **构思描述**

   要顯示為創意子標題的說明。 預設為無說明。

* **每页主题数**

   定義每個頁面顯示的想法/貼文數。 預設值為10。

* **已审核**

   如果勾選，則必須先核准張貼想法和評論，才可將其顯示在發佈網站上。 預設為未勾選。

* **已关闭**

   如果勾選，創意力論壇將不接受新的想法和評論。 預設為未勾選。

* **富文本编辑器**

   如果勾選，便可以輸入附有標籤的想法和評論。 預設為未勾選。

* **允许标记**

   如果勾選，則允許成員將標籤新增至其貼文(請參閱 **[!UICONTROL 標籤欄位]** 標籤)。 預設為未勾選。

* **允许文件上传**

   如果勾選，允許將檔案附件新增至創意或註解。 預設為未勾選。

* **最大文件大小**

   相關條件僅限於 `Allow File Uploads` 已勾選。 此欄位將限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允许的文件类型**

   相關條件僅限於 `Allow File Uploads` 已勾選。 以「點」分隔符號分隔的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則不允許上傳未指定的檔案型別。 預設為none，因此允許所有檔案型別。

* **附加图像文件最大大小**

   只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152 (2 Mb)。

* **允許回覆**

   如果勾選，則允許回覆張貼至創意的評論。 預設為未勾選。

* **允许投票**

   如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **允许用户删除评论和主题**

   如果勾選，則允許成員刪除他們發表的評論和想法。 預設為未勾選。

* **允许关注**

   如果勾選，在創意貼文中加入以下功能，讓會員能夠 [已通知](/help/communities/notifications.md) 新貼文數量。 預設為未勾選。

* **允许电子邮件订阅**

   如果勾選，則允許成員透過電子郵件接收新貼文的通知([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 待檢查及 [電子郵件已設定](/help/communities/email.md). 預設為未勾選。

* **允许投票**

   如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **显示徽章**

   如果勾選，則顯示已認列和已指派 [徽章](/help/communities/implementing-scoring.md) 以會員的想法為基礎。 預設為未勾選。

* **不在清單頁面上取得回覆**

* **允许专题内容**

   如果勾選，便可將創意識別為 [精選內容](/help/communities/featured.md). 預設為未勾選。

* **启用提及功能**
* **最大提及次数**
* **UI 提及模式**

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **[!UICONTROL 使用者稽核]** 索引標籤中，指定如何管理已發佈的想法和評論（使用者產生的內容）。 如需詳細資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

* **拒絕貼文**

   如果勾選，受信任的成員版主將可以拒絕貼文，並阻止貼文出現在公開論壇上。 預設為未勾選。

* **關閉/重新開啟主題**

   如果勾選，受信任的成員版主可以關閉主題以進一步編輯和註釋，也可以重新開啟主題。 預設為未勾選。

* **標幟貼文**

   如果勾選，則允許成員將其他人的主題或評論標籤為不適當。 預設為未勾選。

* **標幟原因清單**

   如果勾選，則允許成員從下拉式清單中選擇將主題或註解標幟為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

   如果勾選，則允許成員輸入他們自己的理由，將主題或評論標籤為不適當。 預設為未勾選。

* **稽核臨界值**

   輸入在通知版主之前，主題或評論必須由成員標幟的次數。 預設值為1 （一次）。

* **標幟限制**

   輸入主題或註解在公開視窗中隱藏前必須標幟的次數。 如果設為–1，則已標幟的主題或註解絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於稽核臨界值。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在 **[!UICONTROL 標籤欄位]** 標籤底下允許的標籤下，可套用的標籤 **[!UICONTROL 設定]** 索引標籤中，會根據所選的名稱空間而有所限制。

* **允许的命名空间**

   相關條件 `Allow Tagging` 已勾選下方的 **[!UICONTROL 設定]** 標籤。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）以及「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建议限制**

   輸入要顯示為論壇成員張貼建議之標籤數目。 值 **-1** 表示沒有限制。 預設值為0。

#### 排序設定索引標籤 {#sort-settings-tab}

在 **[!UICONTROL 排序設定]** 索引標籤中，指定張貼的評論在顯示時的排序方式。

* **排序方式**

   檢查所有允許的排序選擇： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. 預設為 `Newest, Oldest, Last Updated`.

* **设置为默认**

   下拉式選單，選取其中一個核取的排序選項，以顯示為預設值。 預設為 `Newest`.

* **选择分析排序的时间选项**

   下拉以選取其中一項 `All, Last 24 Hours, Last 7 Days, Last 30 Days`. 預設為 `All`.

## 網站訪客體驗 {#site-visitor-experience}

### 建立構想 {#creating-idea}

如同所有Communities功能一樣，網站訪客如果未登入，只能讀取想法並檢視其他意見（透過評論和投票/贊）。

登入後，成員可能會建立新的想法。

![create-new-idea](assets/create-new-idea.png)

在提交想法之前，成員可以儲存草稿。

藉由選取 `Save as Draft` 按鈕，則會儲存草稿。

![儲存構想](assets/save-idea.png)

在中檢視儲存的草稿時 `My Drafts` 索引標籤，選取 `Read More` 若要重新進入編輯模式：

![edit-idea](assets/edit-idea.png)

#### 提供意見回饋 {#providing-feedback}

當創意發佈後，其他成員可以登入，開啟創意( `Read More`)並加上註解，因此可增加票數並發表意見。

![意見反應](assets/feedback-idea.png)

### 附加信息 {#additional-information}

如需詳細資訊，請參閱 [創意力基本要素](/help/communities/ideation.md) 適用於開發人員的頁面。

有關張貼主題和評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤張貼的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
