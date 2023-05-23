---
title: 建構應用程式
seo-title: Structure an App
description: 請依照本頁面的說明操作，瞭解如何建立應用程式的結構。 本頁面說明如何建構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 建構應用程式{#structure-an-app}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM Mobile專案涉及多樣化的內容型別集，包括頁面、JavaScript和CSS使用者端資料庫、可重複使用的AEM元件、Content Sync設定和PhoneGap應用程式殼層內容。 讓您的新AEM Mobile應用程式以 [入門套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 是讓所有不同型別的內容進入我們建議結構的好方法，以便在長期內降低可移植性和可維護性。

## 頁面內容 {#page-content}

應用程式的頁面應該全都位於/content/mobileapps下方，以便AEM Mobile主控台可辨識這些頁面。

![chlimage_1-52](assets/chlimage_1-52.png)

根據AEM慣例，應用程式的第一個頁面應該會重新導向至其中一個子頁面，做為應用程式的預設語言(在Geometrixx和Starter Kit案例中均為「en」)。 頂層地區設定頁面通常會繼承自foundation &#39;splash-page&#39;元件(/libs/mobileapps/components/splash-page)，該元件會負責支援安裝Over-the-Air Content Sync更新所需的初始化(contentInit程式碼位於/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 範本和元件 {#templates-and-components}

應用程式的範本和元件程式碼應位於/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 依照慣例，您應該將範本和元件程式碼放在/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 已經在AEM中操作過Site的開發人員應該熟悉此模式。 通常會接著執行，因為/apps/預設會被鎖定以匿名存取發佈執行個體。 因此，您的原始JSP程式碼會向潛在攻擊者隱藏。

應用程式特定的範本可設定為僅透過使用顯示。 `allowedPaths` 屬性節點，並將其值設為&#39;/content/mobileapps(/)。&amp;ast；)？&#39;  — 或是某些更具體的專案（如果範本僅可用於單一應用程式的話）。 此 `allowedParents` 和 `allowedChildren` 屬性也可以用來根據建立新頁面的位置，對作者可以使用哪些範本進行非常精細的控制。

從頭開始建立新應用程式頁面元件時，建議將其設為 `sling:resourceSuperType` 屬性變更為&#39;mobileapps/components/angular/ng-page&#39;。 這會將您的頁面設定為以單頁應用程式進行製作和呈現，並讓您覆蓋元件可能需要變更的任何.jsp檔案。 由於ng-page完全不包含任何UI架構，因此開發人員通常最終會覆蓋（至少）「template.jsp」(覆蓋自/libs/mobileapps/components/angular/ng-page/template.jsp)。

希望運用AngularJS的可編寫頁面元件具有同等功能 `sling:resourceSuperType` 元件位於/libs/mobileapps/components/angular/ng-component ，可透過相同方式加以覆蓋及自訂。

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

對於使用者端程式庫，開發人員有一些選項可供選擇，以便將程式庫放在存放庫中。 以下模式僅供參考，並非硬性要求。

如果您的使用者端程式碼可以獨立運作，且與應用程式的特定元件無關（這表示它可以在其他應用程式中重複使用），建議您將其儲存於/etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. 另一方面，如果clientlib專屬於單一應用程式，您可以巢狀內嵌為應用程式設計節點的子節點；/etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs。 此clientlib的類別不應由其他程式庫使用，而應視需要用來內嵌其他程式庫。 遵循此模式可讓開發人員無須在每次將使用者端程式庫新增至應用程式時都新增新的Content Sync設定，而只需更新應用程式設計clientlib的「embeds」屬性。 例如，檢視/content/phonegap/geometrixx-outdoors/en/jcr：content/pge-app/app-config/clientlibs-all中的clientlibs-all Content Sync設定Geometrixx。

如果您的使用者端程式碼與特定元件緊密結合，請將該程式碼放入巢狀使用者端程式庫中/apps/中元件位置的下方，並將其類別內嵌至應用程式的「設計」clientlib。

## PhoneGap設定 {#phonegap-configuration}

每個AEM Mobile應用程式都包含一個目錄，其中託管PhoneGap使用的設定檔案 [命令列介面](https://github.com/phonegap/phonegap-cli) 和 [PhoneGap Build](https://build.phonegap.com/) 將您的網頁內容轉換為可執行的應用程式。 舉例來說，在Geometrixx範例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content)位於殼層的一部分；這是由於其中僅包含無法直接更新的內容而做出的設計決定，例如處理裝置API和應用程式本身設定的外掛程式。

在此目錄中，您也會找到 [Cordova鉤點](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) ，可用來安裝外掛程式、將資源檔案置於其平台特定位置，以及其他應在建置中執行的動作。 注意：除了在建置中下載每個外掛程式外，您也可以遵循「廚房水槽」應用程式的模式，並且 [包含外掛程式原始碼](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 與其他應用程式專案搭配使用。

## 后续步骤 {#the-next-steps}

瞭解應用程式的結構後，請參閱 [使用App Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md).
