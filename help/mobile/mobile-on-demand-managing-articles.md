---
title: 管理文章
seo-title: Managing Articles
description: 請依照本頁所述操作，瞭解如何建立和管理文章。
seo-description: Follow this page to learn about creating and managing Articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 管理文章{#managing-articles}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

內容管理動作是建置區塊，可協助您在應用程式中建立和管理文章。 會在應用程式內的文章上執行下列動作。

## 文章概述 {#articles-overview}

文章以文字為基礎，搭配藝術以傳達資訊。

>[!NOTE]
>
>請參閱線上說明中的下列資源，瞭解AEM Mobile應用程式中的下列主題：
>
>* [設計考量](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理文章](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>


## 建立文章 {#creating-an-article}

建立文章的一般工作流程如下：

1. 選取 **行動** 從側邊欄移除。
1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理文章** 圖磚。
1. 選擇文章範本並按一下 **下一個**.
1. 完成精靈的每個步驟，以繼續建立您的新文章。
1. 準備就緒後，按一下 **建立**.
1. 您的新文章會出現在 **管理文章** 圖磚。

## 匯入新文章 {#importing-a-new-article}

現有的Mobile On-Demand內容可以從Mobile On-Demand下載（匯入）到AEM。 如此可讓您編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包括影像。

匯入新文章的工作流程

1. 從Mobile從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理文章** 並選取匯入文章。
1. 按一下 **匯入文章** 在對話方塊上，然後按一下「關閉」。
1. 您的Mobile On-Demand文章現在會出現在 **管理文章** 圖磚。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 編輯文章 {#editing-an-article}

使用內建的AEM拖放編輯器來新增或變更文章。 可以新增/移除文字和影像等元件。 可以插入DAM Assets中的影像。

>[!CAUTION]
>
>編輯器中只能開啟在AEM中建立的文章。

編輯文章的工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 選取AEM來源文章，從 **管理文章** 圖磚。
1. 從清單檢視中按一下醒目提示的文章，以在內容編輯器中開啟它。
1. 使用內容編輯器拖曳文章內容（手稿、影像、文字等）。

### 檢視和編輯文章中的中繼資料 {#viewing-and-editing-the-metadata-within-an-article}

文章、橫幅等內容具有標題、說明、影像等多項屬性。 此動作用於檢視和修改此類屬性。 或者，您也可以在儲存時將這些變更上傳至Mobile On-Demand。

檢視/編輯文章的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從中選擇文章 **管理文章** 圖磚。

1. 選取 **檢視屬性** 動作列中的。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後按一下 **儲存** 完成時。
1. 或者，您可以立即將變更上傳至Mobile On-Demand。

## 上傳文章 {#uploading-an-article}

上傳動作會複製所選內容，並將其新增至Mobile On-Demand專案。 現有的Mobile On-Demand內容將由新版本取代。

上傳文章的一般工作流程：

1. 從 **行動**，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在 **管理文章** 圖磚，選取文章以上傳至Mobile On-Demand。
1. 如有需要，可從清單檢視新增更多文章。
1. 選取 **上傳** 從動作列，然後按一下對話方塊中的「上傳」 。
1. 您的文章現在已上傳至Mobile On-Demand。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 刪除文章 {#deleting-an-article}

此操作會從Mobile On-Demand以及本機AEM執行個體中刪除選取的內容（可選）。

刪除文章的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在中選取要刪除的文章 **管理文章** 圖磚。
1. 確定在清單中選取它，（視需要選取要刪除的其他專案）。
1. 按一下 **刪除** 動作列中的。
1. 檢查您是否要從AEM和Mobile On-Demand中刪除。
1. 单击&#x200B;**删除**。
1. 您的文章現在已從清單中移除。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 后续步骤 {#the-next-steps}

若要瞭解如何管理文章，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
