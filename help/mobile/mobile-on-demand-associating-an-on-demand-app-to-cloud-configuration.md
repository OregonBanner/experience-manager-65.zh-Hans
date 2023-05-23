---
title: 云配置
seo-title: Cloud Configuration
description: 將隨選應用程式與雲端設定建立關聯，可讓Adobe Experience Manager (AEM)建立雙向連結，直接與Mobile On-Demand託管的專案通訊。 請詳閱本頁以瞭解更多資訊。
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# 云配置{#cloud-configuration}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

將隨選應用程式與雲端設定建立關聯，可讓Adobe Experience Manager (AEM)建立雙向連結，直接與Mobile On-Demand託管的專案通訊。 將應用程式連結至Mobile On-Demand專案後，您就能在AEM內建立內容（例如文章、橫幅和集合），並將內容提供給Mobile On-Demand。

從那裡可以發佈、預覽和管理內容。 您也可以將現有的Mobile On-Demand內容匯入AEM並執行內容編輯。

## 設定雲端設定 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>開始為On-Demand應用程式設定雲端設定之前，您必須熟悉AEM Mobile布建和設定AEM Mobile On-demand Services使用者端。
>
>如需詳細資訊，請參閱 [設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 在管理區段中。

若要設定Mobile On-DemandCloud Services，請按一下 **管理連線** 從您的應用程式儀表板動態磚。

您應熟悉應用程式控制面板和可用的圖磚。 另請參閱 [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 以取得更多詳細資料。

### 設定雲端設定的連結 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>確保您有現有的On-Demand使用者端和雲端設定。
>
>如需詳細資訊，請參閱 [設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 在管理區段中。

下列步驟說明如何設定雲端設定的連結：

1. 從 **行動**，選擇 **應用程式** 並從目錄取得您的Mobile On-Demand應用程式。
1. 按一下 **管理連線** 圖磚。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 輸入現有的組態，或輸入 **設定標題**， **裝置ID**、和 **裝置Token**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 一旦您的 **裝置ID** 和 **裝置Token** 已驗證，請從清單中選擇您的隨選專案。

   按一下 **提交**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   此 **管理連線** 圖磚會顯示您的雲端設定。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您嘗試變更此應用程式與哪個專案相關聯，則在控制面板中切換專案時，您將會收到內容完整性問題的警告，如下圖所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 后续步骤 {#the-next-steps}

為您的應用程式設定雲端設定後，請參閱以下管理內容的資源：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
