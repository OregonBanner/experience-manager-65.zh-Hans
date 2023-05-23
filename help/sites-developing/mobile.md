---
title: 建立行動裝置的網站
seo-title: Creating Sites for Mobile Devices
description: 建立行動網站與建立標準網站類似，因為其中也涉及建立範本和元件
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 0%

---

# 建立行動裝置的網站{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

建立行動網站與建立標準網站類似，因為其中也涉及建立範本和元件。 如需建立範本和元件的詳細資訊，請參閱下列頁面： [範本](/help/sites-developing/templates.md)， [元件](/help/sites-developing/components.md) 和 [開發AEM Sites快速入門](/help/sites-developing/getting-started.md). 主要差異在於啟用網站內建的AEM行動裝置功能。 這是透過建立依賴行動頁面元件的範本來達成。

您也應該考慮使用 [回應式設計](/help/sites-developing/responsive.md)，建立可容納多種熒幕大小的單一網站。

若要開始使用，您可以檢視 **We.Retail行動裝置示範網站** AEM中提供的資訊。

若要建立行動網站，請依照下列步驟進行：

1. 建立頁面元件：

   * 設定 `sling:resourceSuperType` 屬性至 `wcm/mobile/components/page`
如此一來，元件就會依賴行動頁面元件。

   * 建立 `body.jsp` 具有專案特定邏輯。

1. 建立頁面範本：

   * 設定 `sling:resourceType` 屬性至新建立的頁面元件。
   * 設定 `allowedPaths` 屬性。

1. 建立網站的設計頁面。
1. 在下方建立網站根目錄頁面 `/content` 節點：

   * 設定 `cq:allowedTemplates` 屬性。
   * 設定 `cq:designPath` 屬性。

1. 在網站根頁面的頁面屬性中，將裝置群組設定在 **行動** 標籤。
1. 使用新範本建立網站頁面。

行動頁面元件( `/libs/wcm/mobile/components/page`)：

* 新增 **行動** 標籤切換至頁面屬性對話方塊。
* 透過其 `head.jsp`，會從請求中擷取目前的行動裝置群組，而且如果找到裝置群組，會使用該群組的 `drawHead()` 包含裝置群組相關模擬器初始元件（僅在製作模式下）與裝置群組轉譯CSS的方法。

>[!NOTE]
>
>行動網站的根頁面必須位於節點階層的層級1，並且建議位於/content節點下方。

## 使用多網站管理員建立行動網站 {#creating-a-mobile-site-with-the-multi-site-manager}

使用多網站管理員(MSM)從標準網站建立行動即時副本。 標準網站會自動轉換為行動網站：行動網站具有行動網站的所有功能（例如在模擬器中編輯），且可以與標準網站同步管理。 請參閱區段 [建立不同頻道的即時副本](/help/sites-administering/msm.md) 在「多網站管理員」頁面中。

## 伺服器端Mobile API {#server-side-mobile-api}

包含行動類別的Java套件包括：

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義MobileConstants。
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  — 定義裝置、DeviceGroup和DeviceGroupList。
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  — 定義DeviceCapability
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  — 定義WurlQueryEngine。
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  — 定義MobileUtil，此函式提供以WCM Mobile為中心的各種公用程式方法。

### 行動元件 {#mobile-components}

此 **We.Retail行動裝置示範網站** 使用下列行動元件，位在底下 `/libs/foundation/components`：

<table>
 <tbody>
  <tr>
   <td>名称</td>
   <td>组</td>
   <td>特性</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>隐藏</td>
   <td> — 頁尾</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>移动设备</td>
   <td> — 根據image foundation元件<br />  — 如果裝置具備此能力，則會轉譯影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>移动设备</td>
   <td> — 根據list foundation元件<br /> - listitem_teaser.jsp會在裝置具備能力時轉譯影像<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>隐藏</td>
   <td> — 根據標誌基礎元件<br />  — 如果裝置具備此能力，則會轉譯影像<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>移动设备</td>
   <td><p> — 與reference foundation元件類似</p> <p> — 將textimage元件對應至mobiletextimage元件，並將影像元件對應至mobileimage元件</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>移动设备</td>
   <td> — 根據textimage foundation元件<br />  — 如果裝置具備此能力，則會轉譯影像</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>隐藏</td>
   <td><p> — 根據topnav foundation元件</p> <p> — 僅轉譯文字</p> </td>
  </tr>
 </tbody>
</table>

#### 建立行動元件 {#creating-a-mobile-component}

AEM行動架構可讓您開發對發出請求的裝置敏感的元件。 下列程式碼範例說明如何在元件jsp中使用AEM行動API，尤其是如何：

* 從請求取得裝置：
   `Device device = slingRequest.adaptTo(Device.class);`

* 取得裝置群組：
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 取得裝置群組功能：
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 取得裝置屬性（原始功能索引鍵/值來自WURFL資料庫）：
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 取得裝置使用者代理程式：
   `String userAgent = device.getUserAgent();`

* 從目前頁面取得裝置群組清單（作者指派給網站的裝置群組）：
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 檢查裝置群組是否支援影像
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
或

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>在jsp中， `slingRequest` 可透過 `<sling:defineObjects>` 標籤和 `currentPage` 透過 `<cq:defineObjects>` 標籤之間。

### 模拟器 {#emulators}

模擬器式撰寫功能為作者提供了建立適用於行動使用者端之內容頁面的方式。 行動內容製作遵循與原位WYSIWYG編輯相同的原則。 為了讓作者能在行動裝置上感知頁面外觀，系統會使用裝置模擬器編輯行動內容頁面。

行動裝置模擬器以一般模擬器架構為基礎。 如需更多詳細資訊，請參閱 [模擬器](/help/sites-developing/emulators.md) 頁面。

裝置模擬器會在頁面上顯示行動裝置，而一般的編輯（parsys、元件）會發生在裝置的畫面內。 裝置模擬器取決於為網站設定的裝置群組。 可以為裝置群組指派數個模擬器。 內容頁面上隨即會提供所有模擬器。 依預設，會顯示指派給場地第一個裝置群組的第一個模擬器。 模擬器可透過頁面頂端的模擬器輪播或Sidekick的編輯按鈕進行切換。

**建立模擬器**

若要建立模擬器，請參閱 [建立自訂行動模擬器](/help/sites-developing/emulators.md) 區段。

**行動模擬器的主要特性**

* 裝置群組由一個或多個模擬器組成：裝置群組設定頁面（例如/etc/mobile/groups/touch）包含 `emulators` 下的屬性 `jcr:content` 節點。
注意：雖然同一模擬器可能屬於數個裝置群組，但這不太合理。

* 透過裝置群組的設定對話方塊， `emulators` 屬性是以所需模擬器的路徑設定。 例如：`/libs/wcm/mobile/components/emulators/iPhone4`。

* 模擬器元件(例如 `/libs/wcm/mobile/components/emulators/iPhone4`)擴充基本行動模擬器元件( `/libs/wcm/mobile/components/emulators/base`)。

* 設定裝置群組時，可選取擴充基本行動模擬器的每個元件。 因此，可以輕鬆建立或擴充自訂模擬器。
* 在編輯模式下的請求時間，會使用模擬器實作來轉譯頁面。
* 當頁面的範本依賴於行動頁面元件時，模擬器功能會自動整合在頁面中(透過 `head.jsp` （包括行動頁面元件）。

### 设备组 {#device-groups}

行動裝置群組會根據裝置功能提供行動裝置區段。 裝置群組提供在製作執行個體上進行模擬器式製作以及在發佈執行個體上正確呈現內容所需的資訊：一旦作者將內容新增至行動頁面並發佈，即可在發佈執行個體上請求頁面。 在那裡，內容頁面會使用其中一個已設定的裝置群組呈現，而不是模擬器編輯檢視。 裝置群組的選擇是根據 [行動裝置偵測](#devicedetection). 然後，相符的裝置群組會提供必要的樣式資訊。

裝置群組在下方定義為內容頁面 `/etc/mobile/devices` 並使用 **行動裝置群組** 範本。 裝置群組範本可作為設定範本，以內容頁面的形式定義裝置群組。 其主要特性包括：

* 位置: `/libs/wcm/mobile/templates/devicegroup`
* 允許的路徑： `/etc/mobile/groups/*`
* 页面组件: `wcm/mobile/components/devicegroup`

#### 將裝置群組指派至您的網站 {#assigning-device-groups-to-your-site}

建立行動網站時，您必須將裝置群組指派給網站。 AEM根據裝置的HTML和JavaScript轉譯功能，提供三個裝置群組：

* **功能** 手機，適用於Sony Ericsson W800等功能裝置，支援基本HTML，但不支援影像和JavaScript。
* **Smart** 手機，適用於Blackberry等裝置，支援基本HTML和影像，但不支援JavaScript。

* **觸控** 手機，適用於iPad等裝置，並完全支援HTML、影像、JavaScript和裝置旋轉。

因為模擬器可以與裝置群組相關聯（請參閱區段） [建立裝置群組](#creating-a-device-group))，將裝置群組指派至網站可讓作者在與裝置群組相關聯的模擬器之間選取，以編輯頁面。

若要將裝置群組指派給您的網站：

1. 在您的瀏覽器中，前往 **Siteadmin** 主控台。
1. 在下方開啟行動網站的根頁面 **網站**.
1. 開啟頁面屬性。
1. 選取 **行動** 標籤：

   * 定義裝置群組。
   * 单击&#x200B;**确定**。

>[!NOTE]
>
>為網站定義裝置群組後，網站的所有頁面都會繼承這些群組。

#### 设备组筛选器 {#device-group-filters}

裝置群組篩選器會定義判斷裝置是否屬於群組的功能型條件。 建立裝置群組時，您可以選取用來評估裝置的篩選器。

在執行階段，當AEM收到來自裝置的HTTP要求時，與群組關聯的每個篩選器都會將裝置功能與特定條件進行比較。 當裝置具備篩選器所需的所有功能時，即視為屬於群組。 從WURFL™資料庫擷取功能。

裝置群組可使用零個或多個篩選器進行功能偵測。 此外，篩選器也可以與多個裝置群組一起使用。 AEM提供預設篩選條件，判斷裝置是否具備為群組選取的功能：

* CSS
* JPG和PNG影像
* JavaScript
* 裝置旋轉

如果裝置群組未使用篩選器，則為該群組設定的選取功能是裝置唯一需要的功能。

如需詳細資訊，請參閱 [建立裝置群組篩選器](/help/sites-developing/groupfilters.md).

#### 建立裝置群組 {#creating-a-device-group}

當AEM安裝的群組不符合您的要求時，請建立裝置群組。

1. 在您的瀏覽器中，前往 **工具** 主控台。
1. 在下方建立新頁面 **工具** > **行動** > **裝置群組**. 在 **建立頁面** 對話方塊：

   * 作為 **標題** 輸入 `Special Phones`.

   * 作為 **名稱** 輸入 `special`.

   * 選取 **行動裝置群組範本**.
   * 单击&#x200B;**创建**。

1. 在CRXDE中，新增 **static.css** 包含下列裝置群組樣式的檔案： `/etc/mobile/groups/special` 節點。

1. 開啟 **特殊電話** 頁面。
1. 若要設定裝置群組，請按一下 **編輯** 按鈕旁邊 **設定**.
於 **一般** 標籤：

   * **標題**：行動裝置群組的名稱。
   * **說明**：群組的說明。
   * **User-Agent**：相符裝置的使用者代理字串。 它是選用的，可以是規則運算式。 示例: `BlackBerryZ10`
   * **功能**：定義群組是否可處理影像、CSS、JavaScript或裝置旋轉。
   * **最小熒幕寬度**&#x200B;和&#x200B;**高度**
   * **停用模擬器**：在內容編輯期間啟用/停用模擬器。

   於 **模擬器** 標籤：

   * **模擬器**：選取指派給此裝置群組的模擬器。

   於 **篩選器** 標籤：

   * 若要新增篩選器，請按一下「新增專案」 ，然後從下拉式清單中選取篩選器。
   * 篩選器會依照其顯示順序進行評估。 當裝置不符合篩選條件時，系統不會評估清單上的後續篩選器。



1. 单击确定。

行動裝置群組設定對話方塊如下所示：

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 每個裝置群組的自訂CSS {#custom-css-per-device-group}

如前所述，您可以將自訂CSS與裝置群組頁面建立關聯，很像設計頁面的CSS。此CSS用於影響作者和發佈時裝置群組特定頁面內容的呈現。然後會自動包含此CSS：

* 在此裝置群組使用的每個模擬器的製作執行個體上的頁面中。
* 在發佈執行個體的頁面中（如果請求的使用者代理符合此特定裝置群組中的行動裝置）。

## 伺服器端裝置偵測 {#server-side-device-detection}

使用篩選器和裝置規格庫來判斷執行HTTP要求的裝置功能。

### 開發裝置群組篩選器 {#develop-device-group-filters}

建立裝置群組篩選器，以定義一組裝置功能需求。 建立您需要的篩選器，以鎖定所需的裝置功能群組。

設計篩選器以便使用它們的組合來定義功能群組。 通常，不同裝置群組的功能會重疊。 因此，您可能會使用具有多個裝置群組定義的篩選器。

建立篩選器後，您可以在群組設定中使用它。

如需詳細資訊，請前往 [建立裝置群組篩選器](/help/sites-developing/groupfilters.md).

### 使用WURFL™資料庫 {#using-the-wurfl-database}

AEM使用的 [WURFL](https://wurfl.sourceforge.net/)根據裝置的使用者代理程式，™取資料庫以查詢裝置功能，例如熒幕解析度或javascript支援。

WURFL™資料庫的XML程式碼表示為以下的節點 `/var/mobile/devicespecs` 透過剖析 `wurfl.xml`檔案位於 `/libs/wcm/mobile/devicespecs/wurfl.xml.` 展開至節點會在 `cq-mobile-core` 組合包已啟動。

裝置功能會儲存為節點屬性，而節點代表裝置模型。 您可以使用查詢來擷取裝置或使用者代理程式的功能。

隨著WURFL™資料庫不斷演化，您可能需要加以自訂或取代。 若要更新行動裝置資料庫，您有以下選項：

* 如果您有允許此使用的授權，請以最新版本取代檔案。 請參閱安裝其他WURFL資料庫。
* 使用AEM中可用的版本，並設定符合使用者代理程式字串並指向現有WURFL™裝置的regexp。 另請參閱 [新增規則運算式型使用者代理程式比對](#adding-a-regexp-based-user-agent-matching).

#### 測試使用者代理程式與WURFL™功能的對應 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

當裝置存取您的行動網站時，AEM會偵測該裝置、根據其功能將其對應至裝置群組，並傳送對應至裝置群組的頁面檢視。 相符的裝置群組提供必要的樣式資訊。 可以在「行動使用者代理程式測試」頁面測試對應：

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 安裝其他WURFL™資料庫 {#installing-a-different-wurfl-database}

與AEM一起安裝的截斷WURFL™資料庫是早於2011年8月30日的版本。 如果您的WURFL版本是在2011年8月30日之後發行，請確定您的使用符合授權規範。

若要安裝WURFL™資料庫：

1. 在CRXDE Lite中建立下列資料夾： `/apps/wcm/mobile/devicespecs`
1. 將WURFL™檔案複製到資料夾。
1. 將檔案重新命名為 `wurfl.xml`.

AEM會自動剖析 `wurfl.xml` 檔案並更新下列節點 `/var/mobile/devicespecs`.

>[!NOTE]
>
>啟用完整的WURFL™資料庫時，剖析和啟動可能需要幾分鐘的時間。 您可以觀看記錄檔以取得進度資訊。

#### 新增規則運算式型使用者代理程式比對 {#adding-a-regexp-based-user-agent-matching}

將使用者代理程式新增為/apps/wcm/mobile/devicespecs/wurfl/regexp底下的規則運算式，以指向現有的WURFL™裝置型別。

1. 在 **CRXDE Lite**，在/apps/wcm/mobile/devicespecs/regexp下建立節點，例如apple_ipad_ver1。
1. 將下列屬性新增至節點：

   * **regexp**：定義使用者代理的規則運算式，例如： 。&#42;Mozilla。&#42;iPad.&#42;AppleWebKit。&#42;Safari。&#42;
   * **deviceId**：在wurfl.xml中定義的裝置ID，例如： apple_ipad_ver1

上述設定會使使用者代理程式符合提供之規則運算式的裝置對應至apple_ipad_ver1 WURFL™裝置ID （如果存在）。

## 使用者端裝置偵測 {#client-side-device-detection}

本節說明如何使用AEM的裝置使用者端偵測，以最佳化頁面呈現或向使用者端提供替代網站版本。

AEM支援以裝置使用者端偵測為基礎 `BrowserMap`. `BrowserMap` 在AEM中作為使用者端程式庫提供，位於 `/etc/clientlibs/browsermap`.

`BrowserMap` 提供您三種策略，可用於為使用者端提供替代網站，其使用順序如下：

1. [替代連結](#providing-alternate-links)
1. [裝置群組特定URL](#definingdevicegroupspecificurl)
1. [以選取器為基礎的URL](#defining-selector-based-urls)

>[!NOTE]
>
>如需使用者端資料庫整合的詳細資訊，請參閱 [使用使用者端HTML程式庫](/help/sites-developing/clientlibs.md) 區段。

### 提供替代連結 {#providing-alternate-links}

此 `PageVariantsProvider` OSGi服務能夠為屬於同一系列的網站產生替代連結。 為了設定服務要考慮的網站，請 `cq:siteVariant` 節點必須新增至 `jcr:content` 網站根目錄的節點。

此 `cq:siteVariant` 節點必須具備下列屬性：

* `cq:childNodesMapTo`  — 決定子節點將對應至連結元素的屬性；建議以此方式組織網站內容，使根節點的子節點代表全域網站的語言變體的根(例如 `/content/mysite/en`， `/content/mysite/de`)，則為的值 `cq:childNodesMapTo` 應為 `hreflang`；
* `cq:variantDomain`  — 指出內容 `Externalizer` 網域將用於產生頁面變體絕對URL；如果未設定此值，則頁面變體將使用相對連結產生；
* `cq:variantFamily`  — 指出此網站屬於哪個網站系列；相同網站的多重灌置特定代表應屬於相同系列；
* `media`  — 儲存連結元素的media屬性值；建議使用 `BrowserMap` 已註冊 `DeviceGroups`，以便 `BrowserMap` 程式庫會自動將使用者端轉送到網站的正確變體。

#### PageVariantsProvider和Externalizer {#pagevariantsprovider-and-externalizer}

當 `cq:variantDomain` 屬性 `cq:siteVariant` 節點不是空的， `PageVariantsProvider` 服務將使用此值作為設定的網域來產生絕對連結。 `Externalizer` 服務。 請務必設定 `Externalizer` 服務，以反映您的設定。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

### 定義裝置群組特定URL {#defining-a-device-group-specific-url}

如果您不想使用替代連結，您可以為每個連結設定全域URL `DeviceGroup`. 建議您建立自己的使用者端程式庫，其中包含 `browsermap.standard` 使用者端程式庫，但重新定義裝置群組。

BrowserMap的設計方式可讓您透過建立同名的新裝置群組並新增至來覆寫裝置群組定義。 `BrowserMap` 自訂使用者端資料庫中的物件。

>[!NOTE]
>
>如需詳細資訊，請閱讀 [自訂瀏覽器地圖](#creatingacustomisedbrowsermap) 區段。

### 定義以選取器為基礎的URL {#defining-selector-based-urls}

如果先前未使用任何機制來指示替代位置 `BrowserMap`，然後是將使用 `DeviceGroups` 將新增至 `URL`s，在這種情況下，您應該提供自己的將處理請求的servlet。

例如，裝置瀏覽 `www.example.com/index.html` 識別為 `smartphone` 由BrowserMap轉送至 `www.example.com/index.smartphone.html.`

### 在您的頁面上使用BrowserMap {#using-browsermap-on-your-pages}

若要在頁面中使用標準BrowserMap使用者端程式庫，您必須包含 `/libs/wcm/core/browsermap/browsermap.jsp` 檔案使用 `cq:include`標籤的位置 `head` 區段。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

除了新增 `BrowserMap` 您的中的使用者端資源庫 `JSP` 檔案時，您也必須新增 `cq:deviceIdentificationMode` 字串屬性設定為 `client-side` 至 `jcr:content` 網站根目錄下的節點。

### 覆寫BrowserMap的預設行為 {#overriding-browsermap-s-default-behaviour}

如果您想要自訂 `BrowserMap`  — 覆寫 `DeviceGroups` 或新增更多探查 — 然後您應該建立自己的使用者端程式庫，並在其中嵌入 `browsermap.standard`使用者端資源庫。

此外，您必須手動呼叫 `BrowserMap.forwardRequest()` 中的方法 `JavaScript` 程式碼。

>[!NOTE]
>
>如需使用者端資料庫整合的詳細資訊，請參閱 [使用使用者端HTML程式庫](/help/sites-developing/clientlibs.md) 區段。

建立自訂後 `BrowserMap` client library （客戶庫），我們建議採取下列方法：

1. 建立 `browsermap.jsp` 應用程式中的檔案

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. 包含 `broswermap.jsp` 檔案。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 從特定頁面排除瀏覽器地圖 {#excluding-browsermap-from-certain-pages}

如果您想從不需要使用者端偵測的部分頁面中排除BrowserMap資料庫，可以新增要求屬性：

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

這將使 `/libs/wcm/core/browsermap/browsermap.jsp` 指令碼，可將meta標籤新增至將製作 `BrowserMap` 不執行任何偵測：

```xml
<meta name="browsermap.enabled" content="false">
```

### 測試網站的特定版本 {#testing-a-specific-version-of-a-web-site}

通常，BrowserMap指令碼會一律將訪客重新導向至最適合的網站版本，通常會在需要時將訪客重新導向至案頭或行動網站。

您可以強制任何請求的裝置，以測試網站的特定版本，方法是新增 `device` 引數至您的URL。 下列URL將會轉譯Geometrixx Outdoors網站的行動版本。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>此 `wcmmode` 引數已設為 `disabled` 以模擬發佈執行個體的行為。

覆寫的裝置值會儲存在Cookie中，因此您可以在不新增 `device` 引數至 `URL`.

因此，您需要呼叫相同的 `URL` 使用 `device` 設定為 `browser` 以便返回網站的案頭版本。

>[!NOTE]
>
>BrowserMap會將覆寫的裝置值儲存在名為的Cookie中 `BMAP_device`. 刪除此Cookie將確保CQ會根據您目前的裝置（例如桌上型電腦或行動裝置）提供適當版本的網站。

## 行動請求處理 {#mobile-request-processing}

AEM會依下列方式處理屬於觸控裝置群組的行動裝置所發出的請求：

1. iPad傳送要求至AEM發佈執行個體，例如 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM會判斷請求頁面的網站是否為行動網站（透過檢查第一層頁面是否為） `/content/geometrixx_mobile` 延伸行動頁面元件)。 如果是：
1. AEM會根據請求標頭中的使用者代理程式查詢裝置功能。
1. AEM將裝置功能對應至裝置群組並設定 `touch` 做為裝置群組選擇器。
1. AEM會將請求重新導向至 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM會將回應傳送至iPad：

   * `products.touch.html` 會以一般方式轉譯，而且可快取。
   * 演算元件會使用選取器來調整簡報。
   * AEM會自動將行動選擇器新增至頁面中的所有內部連結。

### 统计数据 {#statistics}

您可以取得行動裝置向AEM伺服器提出之要求數目的相關統計資料。 可劃分的要求數目：

* 依裝置群組與裝置
* 每年、月與日

若要檢視統計資料，請執行下列動作：

1. 前往 **工具** 主控台。
1. 開啟 **裝置統計資料** 下方頁面 **工具** > **行動**.
1. 按一下連結，即可檢視特定年、月或日的統計資料。

此 **統計資料** 頁面如下所示：

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>此 **統計資料** 頁面會在行動裝置首次存取AEM並偵測到時建立。 在此之前，無法使用。

如果您需要在統計資料中產生專案，可以依照下列步驟進行：

1. 使用行動裝置或模擬器(例如Firefox上的https://chrispederick.com/work/user-agent-switcher/)。
1. 停用編寫模式，例如在編寫執行個體上請求行動頁面：
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

此 **統計資料** 頁面現已可用。

### 「將連結傳送至朋友」連結的支援頁面快取 {#supporting-page-caching-for-send-link-to-a-friend-links}

行動頁面通常可在Dispatcher上快取，因為呈現給裝置群組的頁面會在頁面URL中透過裝置群組選擇器來區分，例如 `/content/mobilepage.touch.html`. 絕不會快取沒有選擇器的行動頁面請求，因為在此情況下，裝置偵測會運作，最後會重新導向至相符的裝置群組（或該事項的「nomatch」）。 透過裝置群組選擇器呈現的行動頁面是由連結重寫程式處理，重寫程式會重寫頁面內的所有連結，使其也包含裝置群組選擇器，以防止在每次點按已符合資格的頁面時，都重新執行裝置偵測。

因此，您可能會遇到下列情況：

使用者Alice被重新導向至 `coolpage.feature.html`，並將該URL傳送給朋友Bob，後者透過位於 `touch` 裝置群組。

若 `coolpage.feature.html` 從前端快取提供服務，AEM沒有機會分析請求以找出行動選擇器不符合新的使用者代理，並且Bob取得錯誤的表示。

若要解決此問題，您可以在頁面上包含簡單的選取UI，讓一般使用者可以覆寫AEM選取的裝置群組。 在上述範例中，頁面上的連結（或圖示）可讓一般使用者切換至 `coolpage.touch.html` 如果他認為他的裝置足夠好。
