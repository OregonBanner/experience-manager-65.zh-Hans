---
title: AEM Mobile On-demand Services的最佳實務
description: 瞭解最佳做法和准則，協助經驗豐富的AEM網站開發人員，協助他們建立行動應用程式範本和元件。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 最佳实践 {#best-practices}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

建置AEM Mobile On-demand Services應用程式與建置直接在Cordova （或PhoneGap） shell中執行的應用程式不同。 開發人員應該熟悉：

* 現成支援的外掛程式以及AEM Mobile特定的外掛程式。

>[!NOTE]
>
>若要深入瞭解外掛程式，請參閱下列資源：
>
>* [在AEM Mobile中使用Cordova外掛程式](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [使用特定於AEM Mobile且啟用Cordova的外掛程式](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* 使用外掛程式功能的範本應以可在瀏覽器中編寫的方式撰寫，而不使用外掛程式橋接器。

   * 例如，請務必等待 *deviceready* 函式之前，先嘗試存取外掛程式的API。

## AEM開發人員指南 {#guidelines-for-aem-developers}

下列指引將協助經驗豐富的AEM網站開發人員，協助他們建立行動應用程式範本和元件：

**建構AEM網站範本以鼓勵重複使用和擴充性**

* 偏好使用多個元件指令碼檔案，而非單一整體式檔案

   * 提供了許多空白的擴充點，例如 *customheaderlibs.html* 和 *customfooterlibs.html*，可讓開發人員變更頁面範本，同時儘可能減少複製核心程式碼的時間
   * 然後可以透過Sling的擴充和自訂範本 *sling：resourceSuperType* 機制

* 範本化語言偏好使用Sightly/HTL而非JSP

   * 使用此功能可鼓勵將程式碼與標籤分離、提供XSS保護內建的功能，並具有更熟悉的語法

**針對裝置上效能最佳化**

* 文章特定的指令碼和樣式表應使用dps-article contentsync範本包含在文章裝載中
* 共用資源應透過dps-HTMLResources contentsync範本，包含由多個文章共用的指令碼和樣式表
* 請勿參考任何會封鎖轉譯器的外部指令碼

>[!NOTE]
>
>您可以深入了解轉譯器封鎖外部指令碼 [此處](https://developers.google.com/speed/docs/insights/BlockingJS).

**相較於Web專屬資料庫，偏好應用程式專屬的使用者端JS和CSS資料庫**

* 為了避免jQuery Mobile等程式庫有額外負荷，而需要處理大量裝置和瀏覽器
* 當範本在應用程式的Webview中執行時，您可以控制應用程式將支援的平台和版本，並瞭解JavaScript將可支援。 例如，與jQuery Mobile和Onsen UI相比，偏好使用Ionic （可能只有CSS）而非Bootstrap。

>[!NOTE]
>
>若要深入瞭解jQuery mobile，請按一下 [此處](https://jquerymobile.com/browser-support/1.4/).

**偏好使用微型程式庫而非完整棧疊程式庫**

* 您的文章所依賴的每個程式庫都會減慢將內容放入裝置玻璃上所需的時間。 使用新的Webview來轉譯每篇文章時，這種速度放緩會加劇，因此必須從頭開始再次初始化每個程式庫
* 如果您的文章不是以SPA （單頁應用程式）建置，則可能不需要包含Angular等完整棧疊程式庫
* 偏好使用較小的單一用途程式庫，以協助新增頁面所需的互動功能，例如 [Fastclick](https://github.com/ftlabs/fastclick) 或 [Velocity.js](https://velocityjs.org)

**將文章裝載的大小最小化**

* 以合理的解析度，使用可能有效涵蓋您支援的最大檢視區的最小資產
* 使用類似以下的工具 *ImageOptim* 移除任何多餘的中繼資料

## 快速入門 {#getting-ahead}

若要進一步瞭解其他兩個角色和職責，請參閱下列資源：

* [管理员](/help/mobile/aem-mobile.md)
* [创作](/help/mobile/aem-mobile-on-demand.md)
