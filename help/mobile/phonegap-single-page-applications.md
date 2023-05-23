---
title: 单页面应用程序
seo-title: Single Page Applications
description: 請依照本頁面的說明了解單頁應用程式，亦即，您可以建立與案頭或行動應用程式執行方式相同的應用程式。
seo-description: Follow this page to learn about single page applications, that is, you can create an application that performs identically to a desktop or mobile application.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# 单页面应用程序{#single-page-applications}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

[單頁應用程式](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已達到關鍵數量，被廣泛視為使用Web技術建立無縫體驗的最有效模式。 遵循SPA模式，您可以建立與案頭或行動應用程式執行方式相同的應用程式，但因其以開放式Web標準為基礎，而涵蓋多種裝置平台和外型規格。

一般而言，SPA的效能較傳統以頁面為基礎的網站來得好，因為這類網站通常會載入完整的HTML頁面 **僅一次** （包括CSS、JS和支援的字型內容），然後只載入每次應用程式中發生狀態變更時所需的專案。 此狀態變更的必要條件可能因所選技術集合而異，但通常包括單一HTML片段以取代現有的「檢視」，以及執行JS程式碼區塊以連線新檢視並執行任何可能必要的使用者端範本轉譯。 此狀態變更的速度可以透過支援範本快取機制進一步改善，甚至可在使用Adobe PhoneGap時離線存取範本內容。

AEM 6.1支援透過AEM應用程式建置和管理SPA。 本文將介紹SPA背後的概念及其運用方式 [AngularJS](https://angularjs.org/) 將您的品牌帶到App Store和Google Play。

## AEM應用程式中的SPA {#spa-in-aem-apps}

AEM應用程式中的單頁應用程式架構可提供AngularJS應用程式的高效能，同時讓作者（或其他非技術人員）透過傳統上為管理網站而保留的觸控最佳化、拖放編輯器環境，建立和管理應用程式的內容。 已經有使用AEM建立的網站？ AEM應用程式可讓您輕鬆重複使用內容、元件、工作流程、資產和許可權。

## AngularJS應用程式模組 {#angularjs-application-module}

AEM應用程式可為您處理大部分AngularJS設定，包括整合應用程式的頂層模組。 依預設，此模組名為「AEMAngularApp」，負責產生此模組的指令碼可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp找到（和覆蓋）。

應用程式初始化的一部分包括指定應用程式所依賴的AngularJS模組。 您的應用程式使用的模組清單由位於/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的指令碼指定，並且可以由您自己的應用程式的頁面元件覆蓋，以提取您的應用程式所需的任何其他AngularJS模組。 例如，將上述指令碼與Geometrixx實作(位於/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)進行比較。

為了支援應用程式中不同狀態之間的導覽，angular — 應用程式 — 模組指令碼會逐一瀏覽頂層應用程式頁面的所有下級頁面，以產生一組「路由」，並設定Angular$routeProvider服務上的每個路徑。 如需實際運用中的範例，請檢視angular應用程式範例產生的Geometrixx Outdoors — 應用程式 — 模組指令碼： （連結需要本機例項） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

在挖掘產生的AEMAngularApp時，您會找到一系列指定的路由，如下所示：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述範例特別說明將引數作為路徑的一部分傳遞的範例。 在此範例中，我們指出當請求符合指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/：id)的路徑時，應由home/products.template.html範本處理，並使用「contentphonegapgeometrixoutdoorsenhomeproducts」控制器。

templateUrl屬性指定請求此路由時要載入的範本。 此範本將包含已包含在頁面上的AEM元件的HTML，以及連線應用程式使用者端所需的任何AngularJS指令。 如需Geometrixx元件中AngularJS指示詞的範例，請檢視swipe-carousel的template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 頁面控制項 {#page-controllers}

用Angular自己的話說，「控制器是用於擴大Angular範圍的JavaScript建構函式。」 ([source](https://docs.angularjs.org/guide/controller))AEM App中的每個頁面都會自動連線至控制器，而控制器可由任何指定 `frameworkType` 之 `angular`. 以ng-text元件為例(/libs/mobileapps/components/angular/ng-text)，包括cq：template節點，每次將這個元件新增至頁面時，都會包含這個重要屬性。

如需更複雜的控制器範例，請開啟ng-template-page controller.jsp指令碼(位於/apps/geometrixx-outdoors-app/components/angular/ng-template-page)。 特別值得關注的是它在執行時產生的javascript程式碼，其呈現方式如下：

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

在上述範例中，您會注意到我們使用的引數來自 `$routeParams` 服務，然後將其植入我們的JSON資料儲存所在的目錄結構中。 處理SKU `id` 透過這種方式，我們得以提供單一產品範本，可針對可能數千種不同的產品呈現產品資料。 這是一種更具擴充性的模式，需要（潛在）大型產品資料庫中每個專案的個別路由。

此外還有兩個元件在運作：ng-product會使用從上方擷取的資料來擴大範圍 `$http` 呼叫。 此頁面上也有一個ng-image，這反過來也會擴大其從回應中擷取之值的範圍。 憑藉Angular的 `$http` 服務時，每個元件會耐心等候，直到請求完成且完成其所建立的Promise為止。

## 后续步骤 {#the-next-steps}

瞭解單頁應用程式後，請參閱 [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md).
