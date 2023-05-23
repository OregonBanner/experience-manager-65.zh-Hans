---
title: 管理集合
seo-title: Managing Collections
description: 系列代表定義良好的貯體，其中填入了適合封面主題的文章或橫幅等內容。 請詳閱本頁以瞭解更多資訊。
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 管理集合{#managing-collections}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

內容管理動作是建置區塊，可協助您建立和管理應用程式內的內容。 會對應用程式內的內容執行下列動作。

## 集合概述 {#collections-overview}

集合代表定義良好 *貯體* 填入適合封面主題的文章或橫幅等內容。

>[!NOTE]
>
>請參閱線上說明中的下列資源，瞭解AEM Mobile應用程式中的下列主題：
>
>* [設計考量](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理集合](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## 建立集合 {#creating-a-collection}

建立集合的一般工作流程如下：

1. 選取 **行動** 從側邊欄移除。
1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理集合** 圖磚。
1. 完成精靈的每個步驟，以繼續建立您的新文章。
1. 準備就緒後，按一下 **建立**.
1. 您的新文章會出現在 **管理集合** 圖磚。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 匯入新的集合 {#importing-a-new-collection}

現有的Mobile On-Demand內容可以從Mobile On-Demand下載（匯入）到AEM。 如此可讓您編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包括影像。

匯入新集合的工作流程

1. 從Mobile從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理集合** 並選取匯入集合。
1. 按一下 **匯入集合** 在對話方塊上，然後按一下「關閉」。
1. 您的Mobile On-Demand集合現在會出現在 **管理集合** 圖磚。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 編輯集合 {#editing-a-collection}

使用內建的AEM拖放編輯器來新增或變更文章。 可以新增/移除文字和影像等元件。 可以插入DAM Assets中的影像。

編輯集合的工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 選取AEM來源文章，從 **管理集合** 圖磚。
1. 從清單檢視中按一下醒目提示的集合，以在內容編輯器中開啟它。
1. 使用內容編輯器來拖曳集合內容（手稿、影像、文字等）。

### 檢視和編輯收藏集中的中繼資料 {#viewing-and-editing-the-metadata-within-a-collection}

集合具有許多屬性，例如標題、說明、影像。 此動作用於檢視和修改此類屬性。 或者，您也可以在儲存時將這些變更上傳至Mobile On-Demand。

檢視/編輯集合的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從中選擇集合 **管理集合** 圖磚。

1. 選取 **屬性** 動作列中的。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後按一下 **儲存** 完成時。
1. 或者，您可以立即將變更上傳至Mobile On-Demand。

## 上傳集合 {#uploading-a-collection}

上傳動作會複製所選內容，並將其新增至Mobile On-Demand專案。 現有的Mobile On-Demand內容將由新版本取代。

上傳集合的一般工作流程：

1. 從 **行動**，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在 **管理集合** 圖磚，選取文章以上傳至Mobile On-Demand。
1. 如有需要，可從清單檢視新增更多集合。
1. 選取 **上傳** 從動作列，然後按一下對話方塊中的「上傳」 。
1. 您的集合現已上傳至Mobile On-Demand。

## 刪除集合 {#deleting-a-collection}

此作業會從Mobile On-Demand刪除選取的集合，並選擇性地從本機AEM執行個體刪除。

刪除集合的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在中選取要刪除的文章 **管理集合** 圖磚。
1. 確定在清單中選取它，（視需要選取要刪除的其他專案）。
1. 按一下 **刪除** 動作列中的。
1. 檢查您是否要從AEM和Mobile On-Demand中刪除。
1. 单击&#x200B;**删除**。
1. 您的集合現在已從清單中移除。

## 新增內容至集合 {#adding-content-to-collections}

集合本質上是一類相關內容。 它們會將文章、橫幅等內容收集到封裝中，以定義應用程式的導覽結構。 集合可以巢狀。

>[!NOTE]
>
>內容必須先上傳至Mobile On-Demand，才能新增至集合。

集合基本上是相關內容的類別：它們會將文章、橫幅等內容收集在一起，放入可定義應用程式導覽結構的套件中。 集合可以巢狀。

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 選取先前上傳的文章（或橫幅/集合）
1. 從動作列選擇「新增至」。
1. 從對話方塊中選取先前上傳的集合。
1. 按一下 **更新** 以新增內容至集合。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

如需有關管理集合的資訊，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
