---
title: 上傳共用資源
seo-title: Uploading Shared Resources
description: 內容管理動作是建置區塊，可協助您建立和管理應用程式內的內容。 請依照本頁面瞭解如何上傳共用資源。
seo-description: Content Management actions are the building blocks that help to create and manage content within an application. Follow this page to learn about uploading shared resources.
uuid: f3595299-1279-4b94-9a49-9d1893250549
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 958461b0-4cbb-452b-88ea-9b98ada14750
exl-id: 4b3acc7c-f1f7-4837-ae3a-9435d6ce1349
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 上傳共用資源 {#uploading-shared-resources}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

內容管理動作是建置區塊，可協助您建立和管理應用程式內的內容。 會對應用程式內的內容執行下列動作。

>[!NOTE]
>
>若要深入瞭解AEM Mobile應用程式的設計考量事項，請參閱 [AEM Mobile應用程式的設計考量事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html) 在「線上說明」中。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 上傳共用資源 {#uploading-shared-resources-1}

通常，文章等內容需要所有作者甚至應用程式具有相同的外觀和風格。 因此，讓指令碼、css和字型可供所有人使用至關重要。 此作業會將這類共用資源傳送至Mobile On-Demand，然後可視需要加以使用。

設定應用程式並將其與雲端設定建立關聯後，您就可以上傳共用資源。 如需將應用程式與雲端設定建立關聯的詳細步驟，請按一下 [此處](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md).

>[!NOTE]
>
>共用資源會使用ContentSync來收集所有不同的資源。 另請參閱 [使用ContentSync的行動裝置](/help/mobile/mobile-ondemand-contentsync.md) 以取得更多詳細資料。

請依照下列步驟為文章上傳共用資源：

1. 選取文章來源 **管理文章** 圖磚。
1. 按一下 **上傳共用資源** 上傳共用的HTML資源。

   ![chlimage_1-133](assets/chlimage_1-133.png)

### 下一步 {#the-next-step}

瞭解如何建立和發佈內容後，請參閱

* [針對AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

或者，您仍需瞭解撰寫主題，請參閱

[為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
