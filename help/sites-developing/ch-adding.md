---
title: 將ContextHub新增至頁面並存取存放區
description: 將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub Javascript程式庫
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 將ContextHub新增至頁面並存取存放區 {#adding-contexthub-to-pages-and-accessing-stores}

將ContextHub新增至您的頁面，以啟用ContextHub功能並連結至ContextHub Javascript程式庫。

ContextHub Javascript API可讓您存取ContextHub管理的內容資料。 本頁面簡要說明用於存取及操控內容資料的API的主要功能。 請依照API參考檔案的連結檢視詳細資訊和程式碼範例。

## 將ContextHub新增至頁面元件 {#adding-contexthub-to-a-page-component}

若要啟用ContextHub功能並連結至ContextHub Javascript程式庫，請包含 `contexthub` 中的元件 `head` 區段。 頁面元件的HTL程式碼應類似於以下範例：

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

請注意，您還需要設定ContextHub工具列是否出現在「預覽」模式中。 另請參閱 [顯示和隱藏ContextHub UI](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## 關於ContextHub存放區 {#about-contexthub-stores}

使用ContextHub存放區來儲存內容資料。 ContextHub提供下列型別的存放區，這些存放區是所有存放區型別的基礎：

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [工作階段存放區](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

所有存放區型別都是 [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) 類別。 如需建立新存放區型別的相關資訊，請參閱 [建立自訂商店](ch-extend.md#creating-custom-store-candidates). 如需有關範例存放區型別的資訊，請參閱 [範例ContextHub存放區候選者](ch-samplestores.md).

### 持續性模式 {#persistence-modes}

Context Hub存放區會使用下列其中一種持續性模式：

* **本機：** 使用HTML5 localStorage來儲存資料。 本機儲存空間會跨工作階段儲存在瀏覽器上。
* **工作階段：** 使用HTML5 sessionStorage來儲存資料。 工作階段存放區會在瀏覽器工作階段期間持續存在，並可供所有瀏覽器視窗使用。
* **Cookie：** 使用瀏覽器原生支援的Cookie來儲存資料。 Cookie資料會以HTTP請求傳送至伺服器，或從伺服器傳送。
* **Window.name：** 使用window.name屬性來儲存資料。
* **記憶體：** 使用Javascript物件來儲存資料。

根據預設，Context Hub會使用本機持續性模式。 如果瀏覽器不支援或允許HTML5 localStorage，則會使用工作階段持續性。 如果瀏覽器不支援或允許HTML5 sessionStorage，則會使用Window.name持續性。

### 存储数据 {#store-data}

在內部，以樹狀結構儲存資料，可將值新增為主要型別或複雜物件。 當您將複雜物件加入至儲存區時，物件屬性會從資料樹狀結構中分支。 例如，下列複雜物件會新增至名為location的空白存放區：

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

存放區資料的樹狀結構可透過下列方式概念化：

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

樹狀結構會將存放區中的資料專案定義為索引鍵/值配對。 在上述範例中，索引鍵 `/number` 與值對應 `321`，和索引鍵 `/data/country` 與值對應 `Switzerland`.

### 操控物件 {#manipulating-objects}

ContextHub提供 [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) 用於操控Javascript物件的類別。 在您將Javascript物件新增至存放區之前，或是從存放區取得之後，可以使用此類別的函式來操控這些物件。

此外， [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) class提供將物件序列化為字串，以及將字串還原序列化為物件的函式。 此類別用於處理JSON資料，以支援本身不包含 `JSON.parse` 和 `JSON.stringify` 函式。

## 與ContextHub存放區互動 {#interacting-with-contexthub-stores}

使用 [`ContextHub`](contexthub-api.md#ui-event-constants) Javascript物件以取得儲存區做為Javascript物件。 取得存放區物件後，您就可以操作其中包含的資料。 使用 [`getAllStores`](contexthub-api.md#getallstores) 或 [`getStore`](contexthub-api.md#getstore-name) 函式以取得存放區。

### 存取存放區資料 {#accessing-store-data}

此 [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript類別會定義數個函式，以便與存放區資料互動。 以下函式儲存和擷取物件中包含的多個資料專案：

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

個別資料專案會儲存為一組索引鍵/值配對。 若要儲存和擷取值，請指定對應的索引鍵：

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

請注意，自訂商店候選者可以定義其他函式，以提供對商店資料的存取權。

>[!NOTE]
>
>ContextHub預設不會知道發佈伺服器上目前使用的登入，並且ContextHub會將此類使用者視為「匿名」。
>
>您可以載入設定檔存放區，讓ContextHub知道登入的使用者。 請參閱 [在此提供GitHub的範常式式碼](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### ContextHub事件 {#contexthub-eventing}

ContextHub包括事件架構，可讓您自動對儲存事件做出反應。 每個存放區物件都包含 [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) 物件，可作為商店的 [`eventing`](contexthub-api.md#eventing) 屬性。 使用 [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) 或 [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) 將Javascript函式繫結至存放區事件的函式。

## 使用Context Hub操作Cookie {#using-context-hub-to-manipulate-cookies}

Context Hub Javascript API為處理瀏覽器Cookie提供跨瀏覽器支援。 此 [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) 名稱空間會定義建立、操作和刪除Cookie的多個函式。

## 決定已解析的ContextHub區段 {#determining-resolved-contexthub-segments}

ContextHub區段引擎可讓您決定要在目前前後關聯中解析哪些註冊的區段。 使用的getResolvedSegments函式 [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) 類別以擷取已解析的區段。 然後，使用 `getName` 或 `getPath` 的功能 [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) 要測試區段的類別。

### ContextHub 区段 {#contexthub-segments}

ContextHub區段會安裝在 `/conf/<site>/settings/wcm/segments` 節點。

以下區段會隨 [wknd教學課程網站。](getting-started.md)

* 夏天
* 冬季

用於解析這些區段的規則概述如下：

* 首先 [地理位置](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) 存放區是用來判斷使用者的緯度。
* 然後，的月份資料專案 [surferinfo存放區](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) 會決定該緯度的季節。

>[!WARNING]
>
>提供的已安裝區段可作為參考設定，協助您為專案建立自己的專用設定，因此不應直接使用。

## 偵錯ContextHub {#debugging-contexthub}

偵錯ContextHub有許多選項，包括產生記錄檔。 另請參閱 [設定ContextHub以取得詳細資訊。](ch-configuring.md#logging-debug-messages-for-contexthub)

## 請參閱ContextHub架構概觀 {#see-an-overview-of-the-contexthub-framework}

ContextHub提供 [診斷頁面](ch-diagnostics.md) 您可以在這裡看到ContextHub架構的概觀。
