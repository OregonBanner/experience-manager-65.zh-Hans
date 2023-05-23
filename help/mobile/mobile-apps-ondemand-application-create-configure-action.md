---
title: 應用程式建立和設定動作
seo-title: Application Create and Configuration Actions
description: 建立應用程式通常是建立和管理AEM Mobile On-Demand內容的第一步。 請詳閱本頁以瞭解更多資訊。
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# 應用程式建立和設定動作{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

## 建立隨選應用程式 {#creating-an-on-demand-application}

建立應用程式通常是建立和管理AEM Mobile On-Demand內容的第一步，並且通常在AEM管理員層級執行。 它代表可在行動裝置上檢視的內容殼層，可隨時顯示作者建立的內容，例如文章、影像、集合等。

您可在控制面板或AEM Mobile控制中心中檢視應用程式的詳細資訊。

>[!NOTE]
>
>「控制面板」是一系列實用的動態磚，可提供應用程式內容、中繼資料和AEM Mobile On-Demand連線狀態的概述。
>
>另請參閱 [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 以取得詳細資訊。

**若要建立隨選應用程式：**

1. 選取 **行動** 從側邊欄移除。
1. 選取 **應用程式** 從「導覽」。
1. 按一下 **建立** 並選取 **應用程式** 從下拉式清單。
1. 選擇行動應用程式範本並按一下 **下一個**.
1. 輸入應用程式屬性，例如 **標題**， **名稱**， **說明**.
1. 单击&#x200B;**下一步**。
1. 如果已知，請輸入雲端設定詳細資料，否則請按一下 **建立**.
1. 按一下 **完成** 以在目錄中檢視新的AEM Mobile應用程式。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>此程式可讓您在AEM中建立應用程式例項。

## 使用應用程式範本 {#using-app-templates}

應用程式範本可讓您輕鬆運用開發人員建立的現有設計，以便在AEM中建立新的應用程式。

什麼是應用程式範本？ 將其視為代表應用程式基準或基礎的頁面範本和元件的集合。
根據其他應用程式的範本建立新應用程式時，您會得到一個應用程式，其起點代表在其中建立該應用程式的起點。

您必須擁有現有的行動應用程式範本（或已安裝具有應用程式範本的應用程式），才能使用此功能。

### 下一步 {#the-next-step}

從應用程式儀表板建立隨選應用程式後，下一步是將應用程式與雲端設定建立關聯。

另請參閱 [將應用程式與雲端設定建立關聯](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 以取得更多詳細資料。

### 快速入門 {#getting-ahead}

在您熟悉建立隨選應用程式，並將該應用程式與雲端設定建立關聯後，請參閱 [內容管理動作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**內容管理動作** 涉及下列內容的建立和管理：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [針對AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
