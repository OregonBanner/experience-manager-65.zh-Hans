---
title: AEM Mobile設定
seo-title: AEM Mobile SetUp
description: 請依照此頁面設定AEM Mobile，進而允許使用者在AEM中建立和管理內容。 本頁提供整合AEM執行個體與雲端AEM Mobile On-demand Services帳戶和專案的資訊。
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# AEM Mobile設定{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>從AEM 6.2或6.3移轉至AEM 6.5的現有AEM Mobile應用程式客戶，可以從PackageShare下載套件，繼續使用AEM Mobile應用程式。 不過，新安裝的AEM 6.5將不支援AEM Mobile應用程式功能。

若要使用AEM產生AEM Mobile應用程式的內容，您必須將AEM執行個體與雲端型AEM Mobile On-demand Services帳戶和專案整合。

請依照下列步驟設定AEM Mobile，進而允許使用者在AEM中建立和管理內容。

## AEM Mobile布建 {#aem-mobile-provisioning}

若要開始使用AEM Mobile設定，您需要：

* **請求API金鑰**：若要存取On-Demand Services API，您需要要求API金鑰。 若要請求API金鑰，請填妥 [PDF表單](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). 將填妥的表單傳送至Adobe Developer支援： [wwds@adobe.com](mailto:wwds@adobe.com)

* **產生裝置ID和裝置代號**：收到API金鑰後，即可產生裝置ID和裝置Token。 前往 `https://aex.aemmobile.adobe.com` 並執行下列動作：

   * 提供API金鑰
   * 使用您新增至AEM Mobile專案的Adobe ID登入，並擁有下列許可權（請參閱下列建立專案的步驟）

      * 管理>管理專案和使用者
      * 內容>新增與編輯內容、刪除內容、檢視內容、發佈內容

如果滿足所有條件，則會產生裝置ID和裝置代號。

>[!NOTE]
>
>應授予所需的Adobe ID對AEM Mobile專案的存取權。 另請參閱 [AEM Mobile的帳戶管理](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) 在「線上說明」中。

## 建立AEM Mobile專案 {#creating-projects-for-aem-mobile}

建立專案時，您可以針對要定位的任何平台指定設定：iOS、Android、Windows和Desktop Web Viewer。 您指定的許多專案設定都會影響應用程式的行為。

建立專案需要使用具有主要管理員角色的Adobe ID登入On-Demand Services入口網站。 編輯專案需要主要管理員角色或具有的使用者角色 **管理專案和使用者** 許可權。

>[!NOTE]
>
>若要進一步瞭解如何在AEM Mobile中建立專案，請按一下 [此處](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## 設定AEM Mobile聯結器 {#configuring-an-aem-mobile-connector}

AEM設定涉及下列聯結器設定步驟。 AEM Mobile聯結器設定完成後，使用者可以設定使用者群組和許可權。

AEM Mobile On-Demand聯結器可用來將AEM Mobile管理的內容與Adobe Experience Manager Mobile的On-Demand服務繫結。 這可讓內容作者使用AEM工具建立和管理行動應用程式的素材，同時使用AEM Mobile的On-Demand Services，輕鬆散佈行動內容。

>[!NOTE]
>
>這是設定AEM執行個體的一次性步驟。

### 設定AEM Mobile On-demand Services使用者端 {#configuring-aem-mobile-on-demand-services-client}

您必須完成設定步驟，AEM Mobile整合才能正常運作。

1. 前往OSGI服務設定

   1. AEM >工具>作業> Web主控台
   1. 捲動或搜尋 ***Experience Manager Mobile On-demand Services使用者端(之前為Adobe Digital Publishing Solution使用者端)***

1. 編輯 ***Experience ManagerMobile On-demand Services使用者端***

   1. **（必要）** 輸入必填欄位：

      1. 客户端 ID.
      1. 客户端密钥.
   1. **（可選）** 編輯現有值。


1. 保存更改。
1. 以下是設定範例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 設定AEM Mobile On-demand Services雲端服務 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 前往Cloud Services

   1. AEM >工具>部署> [CloudService](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). 捲動或搜尋 ***Adobe Experience Manager Mobile隨選服務***

1. 選取 ***立即設定*** 或 ***顯示設定*** 並選取新增設定圖示

1. 建立新設定

   1. 輸入標題和名稱
   1. 輸入裝置ID
   1. 輸入裝置代號
   1. 選取 ***測試裝置組態*** 驗證輸入的值
   1. 選取確定

## 新增AEM Mobile使用者角色及指派許可權 {#adding-aem-mobile-user-roles-and-assigning-permissions}

建立專案後，您應建立角色並授予使用者存取許可權。 只有主要管理員才能建立及編輯角色。 當您建立角色時，您會為獲指派這些許可權的使用者啟用權能（或許可權）。 例如，您可以建立包含應用程式建置許可權的一個角色，以及包含建立和發佈內容許可權的另一個角色。

在AEM Mobile應用程式開發中，有三個不同的角色：

* 管理员
* 开发人员
* 创作

如需以不同許可權（例如應用程式建置或建立和發佈內容）建立角色的詳細資訊，請按一下 [建立使用者角色並授與存取權](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) (位於AEM Mobile說明)。

>[!NOTE]
>
>管理應用程式內容需要開發人員、內容作者和管理員共同的努力。 作者操作頁面，而這些頁面又以應用程式開發人員產生的範本和元件為基礎。 最後，管理員可策略性地發佈更新的應用程式內容。 設定AEM群組和許可權會定義其在應用程式控制面板或控制中心中的角色。
>
>如需AEM Mobile儀表板的詳細資訊，請按一下 [此處](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

使用不同的許可權建立角色後（例如應用程式建置或建立和發佈內容），請參閱 [**設定您的使用者和使用者群組**](/help/mobile/aem-mobile-configure-users.md) 設定您的使用者和群組，以支援行動應用程式的編寫和管理。

### 其他资源 {#additional-resources}

若要進一步瞭解建立AEM Mobile On-demand Services應用程式的其他兩個角色和責任，請參閱下列資源：

* [針對AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>若要預覽應用程式內容（包括瀏覽頁面和文章），請參閱 [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md).
