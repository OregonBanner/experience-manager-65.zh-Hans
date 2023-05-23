---
title: 使用Media Library進行基本數位資產管理
description: '"[!DNL Experience Manager Assets] 以及適用於資產管理的Media Library。」'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# 使用Media Library進行基本資產管理 {#manage-assets-using-media-library}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager] platform提供管理資產的不同功能。 Media Library可讓使用者將少量資產上傳至存放庫、搜尋並使用網頁中的資產，以及完成資產的簡單資產管理任務。

Media Library是輕量版數位資產管理(DAM)解決方案，免費提供 [!DNL Adobe Experience Manager Sites] 授權。 [!DNL Sites] 是Web內容管理(WCM)產品。 Media Library可搭配所有Experience Manager功能使用。

[!DNL Adobe Experience Manager Assets] 授權可單獨購買。 [!DNL Experience Manager Assets] 可透過企業使用案例、中繼資料、結構描述、搜尋和使用者介面的自訂設定，以及Media Library提供的許多其他功能，輕鬆處理資產。

## 授權需求 {#avail-media-library-license}

擁有以下條件的客戶： [!DNL Sites] 授權有權使用Media Library。 它可搭配的所有元件使用 [!DNL Experience Manager].

Media Library會安裝為Sites的一部分。 除了Sites授權和安裝以外，不需要額外的授權或套件。

## [!DNL Assets] vs.Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 Assets功能是透過以下方式提供： [!DNL Experience Manager] 在單一套件中。 但是，尚未購買Assets授權的使用者無權使用進階DAM功能。 若沒有Assets授權，僅限 [Media Library功能](#use-media-library) 可用。

如果您想防止非預期使用 [!DNL Assets] 您尚未授權的功能，然後移除所有 [!DNL Assets] — 特定工作流程、元件、分類、選項及 [!DNL Assets] 管理員來源 [!DNL Experience Manager]. 這麼做可防止您的使用者不小心使用 [!DNL Assets] 您未授權的功能。

## 使用Media Library {#use-media-library}

Media Library為下列使用案例提供基本DAM功能：

* 建立的網頁，使用 [!DNL Adobe Experience Manager Sites].
* 最適化表單與通訊建立方式： [!DNL Adobe Experience Manager Forms].
* 數位熒幕體驗建立方式： [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 適用於Headless作業的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

若要使用Media Library功能，您可以使用預設值 [!DNL Experience Manager] 使用者介面。 Media Library屬於 [!DNL Experience Manager Sites] 安裝時不需要個別介面或附加元件。 使用現有介面，Media Library使用者便有權完成下列工作：

* 建立資料夾以組織資產。
* 上传资源.
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似性搜尋）資產。
* 在中繼資料欄位中新增值並編輯值，但「智慧標籤」欄位除外，這些欄位可在 [!UICONTROL 基本] 資產的「 」標籤 [!UICONTROL 屬性] 頁面。
* 新增和刪除靜態轉譯。
* 下載資料夾、資產和資產轉譯。
* 建立資產版本。
* 建立和執行資產稽核任務。
* 為資產加上註釋。
* 將資產新增至 [!DNL Sites] 頁面瀏覽內容尋找器。
* 用法 [!DNL Content Fragments].
* 將HTTP REST和GraphQL API用於 [!DNL Content Fragments] 和參照的媒體資產，根據Sites授權。
* Marketing Cloud整合。
* 自訂及擴充資產管理使用者介面。
* 存取查詢產生器(API)以擴充搜尋功能。
* 建立靜態標籤。
* 編寫專案和任務。
* 活動資料流（時間軸）。
* 註釋和註解。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例的履行者 [!DNL Experience Manager Assets]. Media Library授權可讓您使用Media Library僅完成列出的使用案例。 如果未列出使用案例，請勿將其與Media Library授權搭配使用。 如果您有任何疑問，請聯絡Adobe客戶支援。

請注意，您無法使用智慧標籤， [!DNL Asset] 連結， [!DNL Asset] 選擇器、大量標籤、修改資產工作流程或標準 [!DNL Adobe Experience Manager] 存取Media Library的使用者介面，不需 [!DNL Assets] 授權。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5內部部署產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

