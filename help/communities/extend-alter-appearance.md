---
title: 變更外觀(HBS)
seo-title: Alter the Appearance
description: 修改HBS指令碼
seo-description: Modify the HBS scripts
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 變更外觀(HBS) {#alter-the-appearance-hbs}

現在，應用程式目錄(/apps)中的自訂註解系統元件已準備就緒，且resourceSuperType已參照預設註解系統和註冊的自訂模型/檢視，可以修改實作。

如需簡單示範，則會移除視覺功能，也就是張貼評論的登入使用者顯示的人物化身。

>[!NOTE]
>
>若要使用擴充功能，受影響網站中的註解系統例項(/content)必須將其資源型別設定為自訂註解系統。

## 修改HBS指令碼 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 開啟 [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 註解包含註解貼文頭像的標籤（~第21行）：

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* 開啟 [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 將包含下一個註解專案頭像的標籤註釋掉（~第44行）：

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 選取 **全部儲存**

### 復寫自訂應用程式 {#replicate-custom-app}

修改應用程式後，必須重新復寫自訂元件。

其中一個方法是使用：

* 從主功能表

   * 選取 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 復寫]**.
   * 選取 **[!UICONTROL 啟動樹狀結構]**.
   * 設定 `Start Path` 至 `/apps/custom`.
   * 取消選取 **[!UICONTROL 僅限已修改的專案]**.
   * 選取 **[!UICONTROL 啟動]** 按鈕。

### 在發佈的範例頁面上檢視修改後的註解 {#view-modified-comment-on-published-sample-page}

[繼續體驗](/help/communities/extend-sample-page.md#publish-sample-page) 在仍以相同使用者身分登入的發佈執行個體上，現在可以重新整理發布環境中的頁面以檢視修改以移除頭像：

![view-modified-content](assets/view-modified-content.png)

### 範例註解擴充功能套件 {#sample-comment-extension-package}

附件是本教學課程中建立之自訂註解應用程式的套件。

[获取文件](assets/sample-comment-extension-6-1-fp3.zip)
