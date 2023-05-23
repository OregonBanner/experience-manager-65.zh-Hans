---
title: 管理橫幅
seo-title: Managing Banners
description: 橫幅通常代表圖形式促銷連結。 請詳閱本頁以瞭解更多資訊。
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# 管理橫幅{#managing-banners}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

內容管理動作是建置區塊，可協助您建立和管理應用程式內的內容。 會對應用程式內的內容執行下列動作。

## 橫幅概觀 {#banners-overview}

橫幅通常代表圖形式促銷連結。

>[!NOTE]
>
>請參閱線上說明中的下列資源，瞭解AEM Mobile應用程式中的下列主題：
>
>* [設計考量](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [建立橫幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>


## 建立橫幅 {#creating-a-banner}

建立文章的一般工作流程如下：

1. 選取 **行動** 從側邊欄移除。
1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理橫幅** 圖磚。
1. 完成精靈的每個步驟，以繼續建立新橫幅。
1. 準備就緒後，按一下 **建立**.
1. 您的新橫幅會出現在 **管理橫幅** 圖磚。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 匯入新橫幅 {#importing-a-new-banner}

現有的Mobile On-Demand內容可以從Mobile On-Demand下載（匯入）到AEM。 如此可讓您編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包括影像。

匯入新文章的工作流程

1. 從Mobile從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下右上角的向下箭頭 **管理橫幅** 並選取匯入橫幅。
1. 按一下 **匯入橫幅** 在對話方塊上，然後按一下「關閉」。
1. 您的Mobile On-Demand文章現在會出現在 **管理橫幅** 圖磚。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 編輯橫幅 {#editing-a-banner}

使用內建的AEM拖放編輯器來新增或變更文章。 可以新增/移除文字和影像等元件。 可以插入DAM Assets中的影像。

>[!CAUTION]
>
>編輯器中只能開啟在AEM中建立的橫幅。

編輯文章的工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從**管理橫幅**圖磚中選取AEM來源的橫幅。
1. 從清單檢視中按一下醒目提示的橫幅，以在內容編輯器中開啟它。
1. 使用內容編輯器拖曳橫幅內容（手稿、影像、文字等）。

### 檢視和編輯橫幅內的中繼資料 {#viewing-and-editing-the-metadata-within-a-banner}

橫幅有許多屬性，例如標題、說明、影像。 此動作用於檢視和修改此類屬性。 或者，您也可以在儲存時將這些變更上傳至Mobile On-Demand。

檢視/編輯文章的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從中選擇橫幅 **管理橫幅** 圖磚。

1. 選取 **屬性** 動作列中的。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後按一下 **儲存** 完成時。
1. 或者，您可以立即將變更上傳至Mobile On-Demand。

## 上傳橫幅 {#uploading-a-banner}

上傳動作會複製所選內容，並將其新增至Mobile On-Demand專案。 現有的Mobile On-Demand內容將由新版本取代。

上傳橫幅的一般工作流程：

1. 從 **行動**，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在 **管理橫幅** 圖磚，選取橫幅以上傳至Mobile On-Demand。
1. 如有需要，從清單檢視中新增更多橫幅。
1. 選取 **上傳** 從動作列，然後按一下對話方塊中的「上傳」 。
1. 您的橫幅現在已上傳至Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 刪除橫幅 {#deleting-a-banner}

此操作會從Mobile On-Demand以及本機的AEM執行個體中刪除選取的橫幅（選擇性）。

刪除橫幅的一般工作流程：

1. 在Mobile中，從目錄中選擇您的Mobile On-Demand應用程式。
1. 選取要刪除的橫幅 **管理橫幅** 圖磚。
1. 確定在清單中選取它（視需要選取要刪除的其他專案）。
1. 按一下 **刪除** 動作列中的。
1. 檢查您是否要從AEM和Mobile On-Demand中刪除。
1. 单击&#x200B;**删除**。
1. 您的橫幅現在已從清單中移除。

### 后续步骤 {#the-next-steps}

如需管理橫幅的詳細資訊，請參閱

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
