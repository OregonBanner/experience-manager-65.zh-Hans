---
title: 新增註解至範例頁面
seo-title: Add Comment to Sample Page
description: 新增自訂註解至頁面
seo-description: Add Custom Comments to a page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 新增註解至範例頁面  {#add-comment-to-sample-page}

現在，自訂註解系統的元件已放置於應用程式目錄(/apps)中，可以使用擴充元件。 要受影響的網站中評論系統的執行個體必須將其資源型別設定為自訂評論系統，並包含所有必要的使用者端程式庫。

## 識別所需的Clientlibs {#identify-required-clientlibs}

對於延伸的「註釋」，預設「註釋」的樣式和功能所需的使用者端程式庫也是必要的。

此 [社群元件指南](/help/communities/components-guide.md) 會識別所需的使用者端程式庫。 瀏覽至「元件指南」並檢視「註解」元件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

請注意，Comments需要三個使用者端程式庫才能正確呈現和運作。 在參照擴充註解時，必須包含這些註解，而且 [延伸註解的使用者端程式庫](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`)。

![comments-component1](assets/comments-component1.png)

### 新增自訂註解至頁面 {#add-custom-comments-to-a-page}

由於每頁只能有一個註解系統，所以建立範例頁面會比較簡單，如短文所述 [建立範例頁面](/help/communities/create-sample-page.md) 教學課程。

建立後，進入設計模式並讓自訂元件群組可供使用，以允許 `Alt Comments` 要新增至頁面的元件。

為了讓「註解」顯示並正常運作，必須將「註解」的使用者端程式庫新增至頁面的clientlibslist (請參閱 [Communities元件的Clientlibs](/help/communities/clientlibs.md))。

#### 範例頁面上的註解Clientlibs {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：範例頁面上的替代註解 {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 作者：範例頁面註解節點 {#author-sample-page-comments-node}

您可以在CRXDE中檢視範例頁面之comments節點的屬性，以驗證resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 發佈範例頁面 {#publish-sample-page}

將自訂元件新增至頁面後，也需要（重新） [發佈頁面](/help/communities/sites-console.md#publishing-the-site).

#### 發佈：範例頁面上的替代註解 {#publish-alt-comment-on-sample-page}

在發佈自訂應用程式和範例頁面後，可以輸入註解。 登入時，請使用 [示範使用者](/help/communities/tutorials.md#demo-users) 或管理員，可以發表評論。

以下是aaron.mcdonald@mailinator.com發表評論：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

現在，延伸元件在預設外觀下已正常運作，修改外觀的時候到了。
