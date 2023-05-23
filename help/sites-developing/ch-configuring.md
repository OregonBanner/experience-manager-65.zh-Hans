---
title: 配置 ContextHub
seo-title: Configuring ContextHub
description: 瞭解如何設定Context中心。
seo-description: Learn how to configure Context Hub.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
source-git-commit: 78ec31362f3aceb5cfc9cc0735bccb88082b8e2d
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# 配置 ContextHub {#configuring-contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 如需ContextHub的詳細資訊，請參閱 [開發人員檔案](/help/sites-developing/contexthub.md). ContextHub取代 [使用者端內容](/help/sites-administering/client-context.md) 在觸控式UI中。

設定 [ContextHub](/help/sites-developing/contexthub.md) 工具列可控制它是否出現在預覽模式中、建立ContextHub存放區，以及使用觸控最佳化UI新增UI模組。

## 停用ContextHub {#disabling-contexthub}

預設情況下，AEM安裝會啟用ContextHub。 可以停用ContextHub以防止其載入js/css和初始化。

<!--
There are two options to disable ContextHub:

* Edit the ContextHub's configuration and check the option **Disable ContextHub**

    1. In the rail click or tap **Tools &gt; Sites &gt; ContextHub**
    1. Click or tap the appropriate **Configuration Container**
    1. Select the **ContextHub Configuration** and click or tap **Edit Selected Element**
    1. Click or tap **Disable ContextHub** and click or tap **Save**

or
-->

* 使用CRXDE Lite設定屬性 `disabled` 至 **true** 在 `/libs/settings/cloudsettings/legacy/contexthub`

>[!NOTE]
>
>[由於AEM 6.4中的存放庫重組，](/help/sites-deploying/repository-restructuring.md) ContextHub設定的位置已從變更 `/etc/cloudsettings` 至：
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`


## 顯示和隱藏ContextHub UI {#showing-and-hiding-the-contexthub-ui}

設定AdobeGranite ContextHub OSGi服務以顯示或隱藏 [ContextHub UI](/help/sites-authoring/ch-previewing.md) （在您的頁面上）。 此服務的PID為 `com.adobe.granite.contexthub.impl.ContextHubImpl.`

若要設定服務，您可以使用 [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或使用 [存放庫中的JCR節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)：

* **Web主控台：** 若要顯示UI，請選取「顯示UI」屬性。 若要隱藏UI，請清除「隱藏UI」屬性。
* **JCR節點：** 若要顯示UI，請設定布林值 `com.adobe.granite.contexthub.show_ui` 屬性至 `true`. 若要隱藏UI，請將屬性設定為 `false`.

顯示ContextHub UI時，它只會顯示在AEM作者執行個體的頁面上。 UI未出現在發佈執行個體的頁面上。

## 新增ContextHub UI模式和模組 {#adding-contexthub-ui-modes-and-modules}

設定在「預覽」模式下顯示在ContextHub工具列中的UI模式和模組：

* UI模式：相關模組群組
* 模組：從存放區公開內容資料並允許作者操作內容的Widget

UI模式會在工具列左側顯示為一系列圖示。 選取後，UI模式的模組會顯示在右側。

![chlimage_1-319](assets/chlimage_1-319.png)

圖示是來自的參照 [Coral UI圖示程式庫](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### 新增UI模式 {#adding-a-ui-mode}

新增UI模式至群組相關的ContextHub模組。 建立UI模式時，您會提供顯示在ContextHub工具列中的標題和圖示。

1. 在Experience Manager邊欄上，按一下或點選「工具>網站>內容中心」。
1. 按一下或點選預設的設定容器。
1. 按一下或點選「Context Hub設定」。
1. 按一下或點選「建立」按鈕，然後按一下或點選「Context Hub UI模式」。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 提供下列屬性的值：

   * UI模式標題：識別UI模式的標題
   * 模式圖示：的選取器 [Coral UI圖示](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) 使用，例如 `coral-Icon--user`
   * 啟用：選取此選項可在ContextHub工具列中顯示UI模式

1. 按一下或點選「儲存」。

### 新增使用者介面模組 {#adding-a-ui-module}

將ContextHub UI模組新增至UI模式，使其顯示在ContextHub工具列中以預覽頁面內容。 新增UI模組時，您會建立已向ContextHub註冊的模組型別例項。 若要新增UI模組，您必須知道關聯模組型別的名稱。

AEM提供基礎UI模組型別以及數個範例UI模組型別，您可以據此建立UI模組。 下表提供每個專案的簡短說明。 如需有關開發自訂UI模組的資訊，請參閱 [建立ContextHub UI模組](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

UI模組屬性包含詳細設定，您可以在其中提供模組特定屬性的值。 您可以提供JSON格式的詳細設定。 表格中的模組型別欄提供每個UI模組型別所需JSON程式碼相關資訊的連結。

| 模組型別 | 描述 | 存储 |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 通用UI模組型別 | 在UI模組屬性中設定 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | 顯示瀏覽器的相關資訊 | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 顯示日期和時間資訊 | 日期時間 |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | 顯示使用者端裝置 | 模擬器 |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | 顯示使用者端的經緯度，以及地圖上的位置。 可讓您變更位置。 | 地理位置 |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | 顯示裝置的熒幕方向（橫向或縱向） | 模擬器 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | 顯示頁面標籤的相關統計資料 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | 顯示目前使用者的設定檔資訊，包括authorizableID、displayName和familyName。 您可以變更displayName和familyName的值。 | 侧面像 |

1. 在Experience Manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選您要新增UI模組的設定容器。
1. 按一下或輸入您要新增UI模組的ContextHub設定。
1. 按一下或點選您要新增UI模組的UI模式。
1. 按一下或點選「建立」按鈕，然後按一下或點選「ContextHub UI模組（一般）」。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 提供下列屬性的值：

   * UI模組標題：識別UI模組的標題
   * 模組型別：模組型別
   * 啟用：選取此選項可在ContextHub工具列中顯示UI模組

1. （選用）若要覆寫預設存放區設定，請輸入JSON物件以設定UI模組。
1. 按一下或點選「儲存」。

## 建立ContextHub存放區 {#creating-a-contexthub-store}

建立Context Hub存放區以儲存使用者資料，並視需要存取資料。 ContextHub存放區是根據已註冊的存放區候選者。 建立存放區時，您需要存放區候選註冊所在的storeType值。 (請參閱 [建立自訂商店候選者](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### 詳細存放區設定 {#detailed-store-configuration}

當您設定存放區時，Detail Configuration屬性可讓您提供存放區特定屬性的值。 此值是根據 `config` 商店的引數 `init` 函式。 因此，您是否需要提供此值和值的格式取決於存放區。

「詳細資料設定」屬性的值為 `config` JSON格式的物件。

### 示例存储候选 {#sample-store-candidates}

AEM提供下列可供您作為存放區基礎的範例存放區候選項。

| 存放區型別 | 描述 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 儲存已解析和未解析的ContextHub區段。 自動從ContextHub SegmentManager擷取區段 |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 儲存目前解析的區段。 偵聽ContextHub SegmentManager服務以自動更新存放區 |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | 儲存瀏覽器位置的經緯度。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | 儲存瀏覽器位置的目前日期、時間和季節 |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 定義許多裝置的屬性和功能，並偵測目前的使用者端裝置 |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | 從JSONP服務擷取並儲存資料 |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 儲存目前使用者的設定檔資料 |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | 儲存使用者端的相關資訊，例如裝置資訊、瀏覽器型別和視窗方向 |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | 儲存頁面標籤和標籤計數 |

1. 在Experience Manager邊欄上，按一下或點選「工具>網站> ContextHub」。
1. 按一下或點選預設設定容器。
1. 按一下或點選「 Contexthub設定」
1. 若要新增商店，請按一下或點選「建立」圖示，然後按一下或點選「 ContexHub商店設定」。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 提供基本設定屬性的值，然後按一下或點選「下一步」：

   * **設定標題：** 識別商店的標題
   * **存放區型別：** 存放區所依據之存放區候選專案的storeType屬性值
   * **必填：** 選取
   * **已啟用：** 選取以啟用存放區

1. （可選）若要覆寫預設存放區設定，請在「詳細資料設定(JSON)」方塊中輸入JSON物件。
1. 按一下或點選「儲存」。

## 範例：使用JSONP服務  {#example-using-a-jsonp-service}

此範例說明如何設定存放區以及在UI模組中顯示資料。 在此範例中，jsontest.com網站的MD5服務會作為存放區的資料來源。 此服務會傳回指定字串的MD5雜湊代碼，格式為JSON。

contexthub.generic-jsonp存放區已設定為儲存服務呼叫的資料 `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. 此服務會傳回以下資料，這些資料會顯示在UI模組中：

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### 建立contexthub.generic-jsonp存放區 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp範例存放區候選可讓您從JSONP服務或傳回JSON資料的Web服務擷取資料。 對於此存放區候選者，請使用存放區設定來提供要使用的JSONP服務的詳細資訊。

此 [init](/help/sites-developing/contexthub-api.md#init-name-config) 的功能 `ContextHub.Store.JSONPStore` Javascript類別會定義 `config` 初始化此存放區候選的物件。 此 `config` 物件包含 `service` 物件，其中包含有關JSONP服務的詳細資訊。 若要設定商店，請提供 `service` JSON格式的物件，作為Detail Configuration屬性值。

若要儲存jsontest.com網站MD5服務的資料，請遵循下列程式： [建立ContextHub存放區](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) 使用下列屬性：

* **設定標題：** md5
* **存放區型別：** contexthub.generic-jsonp
* **必填：** 選取
* **已啟用：** 選取
* **详细配置 (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### 新增md5資料的UI模組 {#adding-a-ui-module-for-the-md-data}

將UI模組新增至ContextHub工具列，以顯示儲存在範例md5存放區中的資料。 在此範例中，contexthub.base模組用於產生下列UI模組：

![chlimage_1-323](assets/chlimage_1-323.png)

請遵循下列步驟： [新增使用者介面模組](#adding-a-ui-module) 將UI模組新增至現有的UI模式，例如範例Perona UI模式。 對於UI模組，請使用以下屬性值：

* **UI模組標題：** MD5
* **模組型別：** contexthub.base
* **详细配置 (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## 偵錯ContextHub {#debugging-contexthub}

可以啟用ContextHub的偵錯模式以進行疑難排解。 偵錯模式可以透過ContextHub設定或透過CRXDE啟用。

### 透過設定 {#via-the-configuration}

編輯ContextHub的設定並核取選項 **偵錯**

1. 在導軌中，按一下或點選 **「工具」>「網站」>「ContextHub」**
1. 按一下或點選預設值 **設定容器**
1. 選取 **ContextHub設定** 並按一下或點選 **編輯選取的元素**
1. 按一下或點選 **偵錯** 並按一下或點選 **儲存**

### 透過CRXDE {#via-crxde}

使用CRXDE Lite設定屬性 `debug` 至 **true** 在：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>對於仍位於其舊有路徑下方的ContextHub設定，設定 `debug property` 是 `/libs/settings/cloudsettings/legacy/contexthub`.

### 靜音模式 {#silent-mode}

無訊息模式會隱藏所有偵錯資訊。 與一般偵錯選項不同（可為每個ContextHub設定單獨設定），無訊息模式是全域設定，其優先於ContextHub設定層級的任何偵錯設定。

這對於您根本不想要任何偵錯資訊的發佈執行個體非常有用。 由於這是全域設定，因此可透過OSGi啟用。

1. 開啟 **Adobe Experience Manager Web主控台設定** 於 `http://<host>:<port>/system/console/configMgr`
1. 搜尋 **AdobeGranite ContextHub**
1. 按一下設定 **AdobeGranite ContextHub** 編輯其屬性
1. 核取選項 **靜音模式** 並按一下 **儲存**

## 升級後復原ContextHub設定 {#recovering-contexthub-configurations-after-upgrading}

當 [升級至AEM](/help/sites-deploying/upgrade.md) 會執行，ContextHub設定會備份並儲存在安全位置。 在升級期間，會安裝預設ContextHub設定，取代現有設定。 您必須進行備份，才能保留您所做的任何變更或新增。

ContextHub設定儲存在名為的資料夾中 `contexthub` 在下列節點下：

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

升級後，備份會儲存在名為的資料夾中 `contexthub` 在名為的節點底下：

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` 或
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

此 `yyyymmdd` 節點名稱的一部分是執行升級的日期。

若要復原您的ContextHub設定，請使用CRXDE Lite從以下複製代表您的存放區、UI模式和UI模組的節點 `default-pre-upgrade_yyyymmdd_xxxxxx` 節點變更為以下：

* `/conf/global/settings/cloudsettings` 或
* `/conf/<tenant>/settings/cloudsettings`
