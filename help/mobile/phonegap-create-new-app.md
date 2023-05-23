---
title: 使用建立精靈建立新的AEM Mobile應用程式
seo-title: Creating a new AEM Mobile app using create wizard
description: AEM Mobile應用程式以Blueprint為基礎，而該Blueprint定義了頁面結構和屬性。 請依照本頁面的說明操作，瞭解如何根據應用程式範本建立新的應用程式。
seo-description: AEM Mobile apps are based on a blueprint that defines a page structure and properties. Follow this page to learn about how to create a new app based on an app template.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# 使用建立精靈建立新的AEM Mobile應用程式{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM Mobile應用程式以Blueprint為基礎，而該Blueprint定義了頁面結構和屬性。 您可以設定下列應用程式屬性：

* **標題：** 應用程式標題。
* **目的地路徑：** 儲存應用程式的存放庫位置。 保留預設值，以根據應用程式名稱建立路徑。

* **名稱：** 預設值為移除空格字元的Title屬性值。 該名稱在AEM中用來指代應用程式，例如代表應用程式的儲存庫節點。
* **說明：** 應用程式的說明。
* **伺服器URL：** 為應用程式提供無線傳送(OTA)內容更新的URL。 預設值是用來建立應用程式（取自外部化程式服務）之執行個體的發佈伺服器URL。 請注意，這必須是發佈伺服器執行個體，而非作者（需要驗證）。

您也可以提供影像檔案以用作應用程式縮圖、選取要使用的PhoneGap Build設定，並選取要使用的行動應用程式分析設定。 此影像僅能作為縮圖，在Experience Manager的行動應用程式控制檯中代表您的行動應用程式。

其他（和選用）標籤可用於建立雲端服務，以及將AdobeMobile Services SDK外掛程式整合至您的應用程式。

* 組建：按一下管理設定，然後在這裡設定您的build.phonegap.com組建服務。 然後從下拉式清單，選取新建立的PhoneGap Build雲端服務。
* Analytics：按一下「管理設定」並設定 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 雲端服務。 然後，您就能從下拉式清單中選取新建立的行動服務，以整合至行動應用程式中。

## 使用應用程式範本 {#using-app-templates}

應用程式範本可讓您輕鬆運用開發人員建立的現有設計，以便在AEM中建立新的應用程式。

什麼是應用程式範本？ 將其視為代表應用程式基準或基礎的頁面範本和元件的集合。
根據其他應用程式的範本建立新應用程式時，您會得到一個應用程式，其起點代表在其中建立該應用程式的起點。

您必須擁有現有的行動應用程式範本（或已安裝具有應用程式範本的應用程式），才能使用此功能。

最新AEM應用程式範例套件包含更新版的Geometrixx應用程式，以及應用程式範本。 或者，您也可以安裝 [Starterkit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 也會提供範本。

根據應用程式範本建立新應用程式的步驟：

1. 導覽至AEM Mobile應用程式目錄： &lt;*server-url*>aem/apps.html/content/mobileapps
1. 選取 **建立** 然後選擇 **應用程式** 如下所示

![chlimage_1-158](assets/chlimage_1-158.png)

選取AEM開發人員提供的應用程式範本。 另請參閱 [AEM Mobile應用程式的結構](/help/mobile/phonegap-structure-an-app.md) 以取得開發人員協助。

![chlimage_1-159](assets/chlimage_1-159.png)

視需要填寫您的新應用程式詳細資訊，包括選擇性地變更其縮圖影像。 這些值稍後可以從 **管理應用程式** 圖磚。

![chlimage_1-160](assets/chlimage_1-160.png)

## 后续步骤 {#the-next-steps}

請參閱下列資源，深入瞭解其他撰寫角色：

* [「管理應用程式」動態磚](/help/mobile/phonegap-app-details-tile.md)
* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [匯入現有的混合式應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 其他资源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
