---
title: 行動應用程式的頁面範本
description: 請詳閱本頁以進一步瞭解頁面範本。 您為應用程式建立的頁面元件是根據/libs/mobileapps/components/angular/ng-page元件。
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2671'
ht-degree: 0%

---

# 行動應用程式的頁面範本 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

## 行動應用程式的頁面範本 {#page-templates-for-mobile-apps-1}

您為應用程式建立的頁面元件是根據/libs/mobileapps/components/angular/ng-page元件([在本機伺服器上以CRXDE Lite開啟](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此元件包含下列元件繼承或覆寫的JSP指令碼：

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

使用判斷應用程式的名稱 `applicationName` 屬性，並透過pageContext加以公開。

包含head.jsp和body.jsp。

### head.jsp {#head-jsp}

寫出 `<head>` 應用程式頁面的元素。

如果您想要覆寫應用程式的檢視區中繼屬性，這是您覆寫的檔案。

根據最佳實務，應用程式會將使用者端程式庫的css部分包含在標題中，而JS則包含在結尾處&lt; `body>` 元素。

### body.jsp {#body-jsp}

angular視是否偵測到wcmMode (！= WCMMode.DISABLED)，以判斷開啟頁面以供撰寫還是作為已發佈頁面。

**作者模式**

在製作模式中，每個個別頁面會個別呈現。 angular不會處理頁面之間的路由，也不會使用ng-view載入包含頁面元件的部分範本。 相反地，頁面範本(template.jsp)的內容會透過包含在伺服器端 `cq:include` 標籤之間。

此策略可啟用作者功能（例如在段落系統、Sidekick、設計模式等中新增和編輯元件） 在不修改的情況下運作。 依賴使用者端轉譯的頁面（例如應用程式的頁面）在AEM編寫模式中無法正常運作。

請注意，template.jsp include會包裝在 `div` 元素包含 `ng-controller` 指令。 此結構可啟用DOM內容與控制器的連結。 因此，雖然在使用者端轉譯的頁面會失敗，但這麼做可正常運作的個別元件（請參閱下文元件一節）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**發佈模式**

在發佈模式中（例如使用Content Sync匯出應用程式時），所有頁面都會變成單頁應用程式(SPA)。 (若要瞭解SPA，請使用Angular教學課程，尤其是 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

SPA中只有一個HTML頁面(包含 `<html>` 元素)。 此頁面稱為「版面配置範本」。 在Angular術語中，這是「……在我們的應用程式中所有檢視都通用的範本」。 將此頁面視為「頂層應用程式頁面」。 按照慣例，頂層應用程式頁面為 `cq:Page` 最接近根的應用程式節點（且不是重新導向）。

由於應用程式的實際URI在發佈模式下不會變更，因此從此頁面參考外部資產必須使用相對路徑。 因此，提供特殊的影像元件，在轉譯影像以進行匯出時，會將此頂層頁面列入考量。

作為SPA，此配置範本頁面只會產生具有ng-view指示詞的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

angular路由服務會使用此元素來顯示應用程式中每個頁面的內容，包括目前頁面的可授權內容（包含在template.jsp中）。

body.jsp檔案包含空白的header.jsp和footer.jsp。 如果您想要在每個頁面上提供靜態內容，可以在應用程式中覆寫這些指令碼。

最後，javascript clientlibs會包含在底部 &lt;body> 元素，其中包含伺服器上產生的兩個特殊JS檔案： *&lt;page name=&quot;&quot;>*.angular-app-module.js和 *&lt;page name=&quot;&quot;>*.angular-app-controllers.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此指令碼會定義應用程式的Angular模組。 此指令碼的輸出會連結至範本的其餘元件透過 `html` 元素，包含下列屬性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此屬性會指示Angular此DOM元素的內容應連結至下列模組。 此模組會將檢視(在AEM中，這些會是cq：Page資源)與對應的控制器連結。

此模組也會定義名為的頂層控制器 `AppController` 會公開 `wcmMode` 變數，並設定從中擷取Content Sync更新裝載的URI。

最後，此模組會逐一檢視每個下級頁面（包括其本身），並呈現每個頁面的路由片段的內容(透過angular-route-fragment.js選擇器和擴充功能)，包括作為Angular\$routeProvider的設定專案。 換言之，\$routeProvider會告知應用程式當要求指定路徑時要轉譯的內容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此指令碼會產生JavaScript片段，該片段必須採用以下形式：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此程式碼向$routeProvider (定義於angular-app-module.js.jsp中)指出「/&lt;path>&#39;將由位於的資源處理 `templateUrl`，並連線至 `controller` （我們接下來會介紹此功能）。

如有必要，您可以覆寫此指令碼以處理更複雜的路徑，包括含有變數的路徑。 在AEM隨附的/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp指令碼中可以看到這方面的範例：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器在\$scope中連線變數，使其顯示在檢視中。 angular-app-controllers.js.jsp指令碼遵循angular-app-module.js.jsp所述的模式，即它會逐一瀏覽每個下級頁面（包括其本身），並輸出每個頁面定義的控制器片段(透過controller.js.jsp)。 它定義的模組稱為 `cqAppControllers` 和必須列為頂層應用程式模組的相依性，才能使用頁面控制器。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp指令碼會為每個頁面產生控制器片段。 此控制器片段採用下列形式：

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

請注意 `data` 變數會獲派Angular傳回的promise `$http.get` 方法。 如果需要，此頁面中包含的每個元件都可以(透過其angular.json.jsp指令碼)提供一些.json內容，並在解析時處理此請求的內容。 行動裝置上的要求非常快速，因為它只會存取檔案系統。

若要讓元件以這種方式成為控制器的一部分，應擴充/libs/mobileapps/components/angular/ng-component元件並包含 `frameworkType: angular` 屬性。

### template.jsp {#template-jsp}

template.jsp最初是在body.jsp一節中介紹的，它只包含頁面的parsys。 在發佈模式中，此內容會直接參考(在 &lt;page-path>.template.html)，並透過\$routeProvider上設定的templateUrl載入SPA。

此指令碼中的parsys可設定為接受任何型別的元件。 但是，在處理為傳統網站(而不是SPA)建立的元件時，必須謹慎。 例如，foundation影像元件只有在頂層應用程式頁面上才能正常運作，因為它的設計目的並非參照應用程式內的資產。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此指令碼只會輸出頂層Angular應用程式模組的Angular相依性。 angular-app-module.js.jsp會參考該模型。

### header.jsp {#header-jsp}

將靜態內容放在應用程式頂端的指令碼。 此內容包含在頂層頁面中，不在ng-view的範圍之內。

### footer.jsp {#footer-jsp}

將靜態內容放在應用程式底部的指令碼。 此內容包含在頂層頁面中，不在ng-view的範圍之內。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆寫此指令碼以包含您的JavaScript clientlibs。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆寫此指令碼以包含您的CSS clientlibs。

## 應用程式元件 {#app-components}

應用程式元件不僅必須在AEM例項（發佈或作者）上運作，而且必須在應用程式內容透過Content Sync匯出至檔案系統時運作。 因此，元件必須包括下列特性：

* PhoneGap應用程式中的所有資產、範本和指令碼都必須相對參照。
* 如果AEM執行個體以製作或發佈模式運作，連結的處理方式會有所不同。

### 相對資產 {#relative-assets}

PhoneGap應用程式中任何指定資產的URI不僅會因平台而異，在應用程式的每次安裝時也會是唯一的。 例如，記下在iOS模擬器中執行之應用程式的下列URI：

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

請注意路徑中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

身為PhoneGap開發人員，您關注的內容位於www目錄下方。 若要存取應用程式資產，請使用相對路徑。

為了解決複雜的問題，PhoneGap應用程式會使用單頁應用程式(SPA)模式，讓基本URI （雜湊除外）永不變更。 因此，您參考的每個資產、範本或指令碼 **必須相對於您的頂層頁面。** 最上層頁面會藉由下列方式初始化Angular路由與控制器： `*<name>*.angular-app-module.js` 和 `*<name>*.angular-app-controllers.js`. 此頁面應該是離存放庫根目錄*不*延伸sling：redirect的最近頁面。

有數種協助程式方法可用於處理相對路徑：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

若要檢視其使用範例，請開啟位於/libs/mobileapps/components/angular的mobileapps來源。

### 链接 {#links}

連結必須使用 `ng-click="go('/path')"` 函式以支援所有WCM模式。 此函式取決於範圍變數的值，以正確判斷連結動作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

時間 `$scope.wcmMode == true` 我們會以一般方式處理每個導覽事件，因此會變更URL的路徑和/或頁面部分。

或者，如果 `$scope.wcmMode == false`，則每個導覽事件都會導致URL的雜湊部分變更，而此URL會由Angular的ngRoute模組在內部解析。

### 元件指令碼詳細資料 {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

偵測到編輯模式時，此指令碼會顯示元件內容或適當的預留位置。

#### template.jsp {#template-jsp-1}

template.jsp指令碼會呈現元件的標籤。 如果有問題的元件是由從AEM擷取的JSON資料所驅動(例如「ng-text」：/libs/mobileapps/components/angular/ng-text/template.jsp)，則此指令碼將負責使用頁面的控制器範圍所公開的資料來連線標籤。

不過，效能需求有時會規定不執行任何使用者端範本（亦即資料繫結）。 在此情況下，只需在伺服器端轉譯元件的標籤，且該標籤會包含在頁面範本內容中。

#### overhead.jsp {#overhead-jsp}

在由JSON資料驅動的元件中(例如「ng-text」：/libs/mobileapps/components/angular/ng-text)，overhead.jsp可用來從template.jsp移除所有Java程式碼。 然後會從template.jsp中引用它，並且在請求中公開的任何變數都可供使用。 此策略鼓勵將邏輯與呈現方式分離，並限制從現有元件衍生出新元件時，必須複製和貼上的程式碼數量。

#### controller.js.jsp {#controller-js-jsp-1}

如AEM頁面範本中所述，每個元件都可以輸出JavaScript片段，以使用 `data` Promise。 依照Angular慣例，控制器只應用於指派變數至範圍。

#### angular.json.jsp {#angular-json-jsp}

此指令碼會以片段形式包含在全頁面的「&lt;page-name>針對每個延伸ng-page的頁面匯出的。angular.json&#39;檔案。 在此檔案中，元件開發人員可以公開元件所需的任何JSON結構。 在「ng-text」範例中，此結構僅包含元件的文字內容，以及指出元件是否包含RTF文字的標幟。

Geometrixx戶外應用程式產品元件是更複雜的範例(/apps/geometrixx-outdoors-app/components/angular/ng-product)：

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI資產下載內容 {#contents-of-the-cli-assets-download}

從Apps主控台下載CLI資產，以針對特定平台最佳化，然後使用PhoneGap命令列整合(CLI) API建置應用程式。 您儲存至本機檔案系統的ZIP檔案內容具有下列結構：

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

這是隱藏的目錄，視您目前的作業系統設定而定，您可能無法看見。 您應設定作業系統，以便在您計畫修改其中包含的應用程式掛接時顯示此目錄。

#### .cordova/hooks/ {#cordova-hooks}

此目錄包含 [CLI鉤點](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Hooks目錄中的資料夾包含node.js指令碼，這些指令碼會在建置期間的確切時間點執行。

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目錄包含 `copy_AMS_Conifg.js` 檔案。 此指令碼會複製設定檔案，以支援Adobe Mobile Services分析資料的收集。

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

after-prepare目錄包含 `copy_resource_files.js` 檔案。 此指令碼會將許多圖示和啟動畫面影像複製到平台專屬的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目錄包含 `install_plugins.js` 檔案。 此指令碼會逐一檢視Cordova外掛程式識別碼清單，目前尚無法安裝所偵測到的識別碼。

此策略並不要求您每次Maven時都套件和安裝外掛程式至AEM `content-package:install` 命令會執行。 將檔案簽入SCM系統的替代策略需要重複的套件和安裝活動。

#### .cordova/鉤點/其他鉤點 {#cordova-hooks-other-hooks}

視需要包含其他鉤點。 可使用下列鉤點（如Phonegap範例hello world應用程式所提供）：

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### 平台/ {#platforms}

在您執行 `phonegap run <platform>` 指令。 目前， `<platform>` 可以是 `ios` 或 `android`.

為特定平台建立應用程式後，會建立對應的目錄，且目錄中包含平台專屬的應用程式程式程式碼。

#### 外掛程式/ {#plugins}

外掛程式目錄會由 `.cordova/hooks/before_platform_add/install_plugins.js` 檔案執行之後 `phonegap run <platform>` 命令。 目錄最初是空的。

#### www/ {#www}

www目錄包含實施應用程式外觀和行為的所有網頁內容(HTML、JS和CSS檔案)。 除了下述例外情況外，此內容源自AEM，並透過Content Sync匯出至其靜態形式。

#### www/config.xml {#www-config-xml}

此 [PhoneGap檔案](https://docs.phonegap.com) 將此檔案稱為「全域設定檔案」。 config.xml包含許多應用程式屬性，例如應用程式名稱、應用程式「偏好設定」(例如iOS Webview是否允許捲動)以及 *僅限* 已由PhoneGap Build使用。

config.xml檔案是AEM中的靜態檔案，會透過Content Sync依原樣匯出。

#### www/index.html {#www-index-html}

index.html檔案會重新導向至應用程式的起始頁面。

config.xml檔案包含 `content` 元素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在 [PhoneGap檔案](https://docs.phonegap.com)，此元素會說明為「選擇性」 &lt;content> 元素會定義應用程式在頂層web assets目錄中的起始頁面。 預設值為index.html，通常顯示在專案的頂層www目錄中。」

如果沒有index.html檔案，PhoneGap Build會失敗。 因此，包含此檔案。

#### www/res {#www-res}

res目錄包含啟動畫面影像和圖示。 此 `copy_resource_files.js` 指令碼會在「 」期間將檔案複製到其平台特定位置 `after_prepare` 建置階段。

#### www/etc {#www-etc}

依照慣例，在AEM中，/etc節點包含靜態clientlib內容。 etc目錄包含Topcoat、AngularJS和ng-clientlibsallGeometrixx庫。

#### www/apps {#www-apps}

apps目錄包含與啟動顯示畫面相關的程式碼。 AEM應用程式啟動顯示頁面的唯一特徵是，它會在使用者不互動的情況下初始化應用程式。 因此，應用程式的clientlib內容（CSS和JS）會降到最低，以最大化效能。

#### www/content {#www-content}

內容目錄包含應用程式的其餘網頁內容。 內容可以包含但不限於下列檔案：

* HTML頁面內容(直接在AEM中編寫)
* 與AEM元件相關聯的影像資產
* 伺服器端指令碼產生的JavaScript內容
* 說明頁面或元件內容的JSON檔案

#### www/package.json {#www-package-json}

package.json檔案是資訊清單檔案，其列出了 **完整** 內容同步下載包含。 此檔案也包含產生內容同步裝載的時間戳記(`lastModified`)。 向AEM請求應用程式的部分更新時，會使用此屬性。

#### www/package-update.json {#www-package-update-json}

如果此裝載是整個應用程式的下載，此資訊清單會包含檔案的確切清單，如下所示 `package.json`.

不過，如果此裝載為部分更新， `package-update.json` 僅包含此特定裝載中包含的檔案。
