---
title: 建立文章匯出設定
seo-title: Creating Article Export Configuration
description: 請依照本頁面的說明了解如何從Adobe Experience Manager (AEM)匯出內容以上傳至AEM Mobile。
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 建立文章匯出設定{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**先决条件**:
>
>在瞭解如何建立和修改共用資源之前，請參閱 [內容同步](/help/mobile/mobile-ondemand-contentsync.md) 以瞭解基本概念。

AEM Mobile使用者會使用Content Sync將即時內容匯出至靜態內容，以供行動應用程式使用，此匯出會在內容從AEM Mobile上傳至Mobile On-Demand Services時發生。

屬性 ***dps-exportTemplate*** 以上表格所述，會定義應用程式匯出設定的路徑。 設定此屬性以建立和修改共用資源。

下列資源說明如何從Adobe Experience Manager (AEM)匯出內容以上傳至AEM Mobile。

文章包含需要匯出和上傳的內容。 部分內容可在文章之間共用。

使用 [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) 將內容收集在一起並建立 ***共用資源*** 封裝。

ContentSync設定位於 **&lt;dps-exporttemplate>/dps-article>** 應設定為匯出內容以及裝置上靜態呈現屬性所需的文章。

>[!CAUTION]
>
>只有具備下列條件時，您才可以執行下列步驟來檢視範例共用資源：
>
>* 已安裝範例內容
>* 執行AEM執行個體
>* 沒有已設定的自訂內容或其他連線埠
>


若要檢視範例共用資源，請參閱下列步驟：

1. 在您的AEM伺服器上開啟CRXDE Lite。
1. 瀏覽至此路徑 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以檢視範例共用資源。

   您可以檢視建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>當文章內容變更時，應將文章上傳或匯出至AEM Mobile On-demand Services。
