---
title: 頁面匯出工具
description: 瞭解如何使用AEM頁面匯出工具。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# 頁面匯出工具{#the-page-exporter}

AEM可讓您將頁面匯出為完整的網頁，包含影像， `.js` 和 `.css` 檔案。

設定後，您透過取代 `html` 替換為 `export.zip` 在URL中。 這會產生封存(zip)檔案，其中包含以html格式呈現的頁面以及參照的資產。 頁面中的所有路徑（例如，影像的路徑）會重新寫入，以指向封存中包含的檔案，或伺服器上的資源。 接著，您就可以從瀏覽器下載封存(zip)檔案。

>[!NOTE]
>
>根據您的瀏覽器和設定，下載內容將為：
>* 封存檔案(`<page-name>.export.zip`)
>* 資料夾(`<page-name>`)；有效地封存檔案已展開


## 匯出頁面 {#exporting-a-page}

下列步驟說明如何匯出頁面，並假設您的網站存在匯出範本。 匯出範本會定義頁面的匯出方式，且是您網站專屬的。 若要建立匯出範本，請參閱 [為您的網站建立頁面匯出程式設定](#creating-a-page-exporter-configuration-for-your-site) 區段。

若要匯出頁面：

1. 導覽至中的必要頁面。 **網站** 主控台。

1. 選取頁面，然後開啟 **屬性** 對話方塊。

1. 選取 **進階** 標籤。

1. 展開 **匯出** 欄位以選取匯出範本。
為您的網站選取所需的範本，然後確認： **確定**.

1. 選取 **儲存並關閉** 以關閉頁面屬性對話方塊。

1. 要求匯出頁面，取代尾碼 `html` 替換為 `export.zip` 在URL中。

   例如：
   * localhost：4502/content/we-retail/language-masters/en.html

   存取：
   * localhost：4502/content/we-retail/language-masters/en.export.zip


1. 將封存檔案下載至您的檔案系統。

1. 如有必要，請在您的檔案系統中解壓縮檔案。 展開後，將會有一個資料夾與所選頁面同名。 此資料夾包含：

   * 子資料夾 `content`，代表一系列子資料夾的根目錄，這些子資料夾反映存放庫中頁面的路徑

      * 在此結構中，有所選頁面的html檔案(`<page-name>.html`)
   * 其他資源(`.js` 檔案， `.css` 檔案、影像等) 會根據匯出範本中的設定來定位


1. 開啟頁面html檔案(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)，以檢查轉譯。

## 為您的網站建立頁面匯出程式設定 {#creating-a-page-exporter-configuration-for-your-site}

頁面匯出工具是根據 [內容同步架構](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). 中可用的設定 **頁面屬性** 對話方塊是定義頁面所需相依性的匯出範本。

觸發頁面匯出時，會參考匯出範本，並動態套用頁面路徑和設計路徑。 然後使用標準Content Sync功能建立zip檔案。

現成可用的AEM安裝包含 `/etc/contentsync/templates/default`.

* 此範本是在存放庫中找不到匯出範本時的後援範本。

* 此 `default` 範本會說明如何設定頁面匯出，以便作為新匯出範本的基礎。

* 若要在瀏覽器中以JSON格式檢視範本的節點結構，請要求下列URL：
   `http://localhost:4502/etc/contentsync/templates/default.json`

建立新頁面匯出工具範本最簡單的方法是：

* 複製 `default` 範本，

* 指派適合您網站的新名稱，

* 然後進行必要的更新。

若要建立全新的範本：

1. 在 **CRXDE Lite**，在下方建立節點 `/etc/contentsync/templates`：

   * `Name`：適合您網站的名稱；例如， `<mysite>`. 選擇頁面匯出程式範本時，名稱會顯示在頁面屬性對話方塊中。

   * `Type`： `nt:unstructured`

2. 在範本節點底下，呼叫這裡 `mysite`，使用下述設定節點建立節點結構。

## 啟用頁面的頁面匯出工具範本 {#activating-a-page-exporter-configuration-for-your-pages}

設定範本後，您需要讓它可供使用：

1. 在CRXDE中導覽至 `/content` 分支。 這可以是個別頁面，或是子樹狀結構的根頁面。

1. 於 `jcr:content` 建立屬性的頁面節點：
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`：範本的路徑；例如： `/etc/contentsync/templates/mysite`

### 頁面匯出工具組態節點 {#page-exporter-configuration-nodes}

範本由節點結構組成，因為它使用 [內容同步架構](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  每個節點都有 `type` 屬性，定義zip檔案建立程式中的特定動作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

下列節點可用來建置匯出範本：

* `page`
頁面節點用於將頁面html複製到zip檔案。 它具有下列特性：

   * 是必要節點。
   * 位於下方 `/etc/contentsync/templates/<mysite>`.
   * 使用屬性定義 `Name`設定為 `page`.
   * 節點型別為 `nt:unstructured`

   此 `page` 節點具有下列屬性：

   * A `type` 使用值設定的屬性 `pages`.

   * 它沒有 `path` 屬性，因為目前的頁面路徑會動態複製到設定。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
rewrite節點會定義如何在匯出的頁面中重新寫入連結。 重寫的連結可以指向zip檔案中包含的檔案，也可以指向伺服器上的資源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
設計節點用於複製用於匯出頁面的設計。 它具有下列特性：

   * 為選用。
   * 位於下方 `/etc/contentsync/templates/<mysite>`.
   * 使用屬性定義 `Name` 設定為 `design`.
   * 節點型別為 `nt:unstructured`.

   此 `design` 節點具有下列屬性：

   * A `type` 屬性已設定為值 `copy`.

   * 它沒有 `path` 屬性，因為目前的頁面路徑會動態複製到設定。


* `generic`
通用節點用於複製clientlibs等資源 
`.js` 或 `.css` 檔案放入zip檔案中。 它具有下列特性：

   * 為選用。
   * 位於下方 `/etc/contentsync/templates/<mysite>`.
   * 沒有特定名稱。
   * 節點型別為 `nt:unstructured`.
   * 具有 `type` 屬性和 `type` 相關屬性。 <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下設定節點會複製 `mysite.clientlibs.js` 檔案放入zip檔案：

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**實作自訂設定**

也可以使用自訂設定。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

若要符合某些特定需求，您可能需要實作 [自訂更新處理常式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以程式匯出頁面 {#programmatically-exporting-a-page}

若要以程式設計方式匯出頁面，您可以使用 [頁面匯出工具](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務可讓您：

* 匯出頁面並寫入HTTP servlet回應。
* 匯出頁面並將壓縮檔儲存在特定位置。

繫結至 `export` 選擇器和 `zip` 擴充功能會使用PageExporter服務。

## 疑难解答 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除 `/var/contentsync` 存放庫中的節點，然後再次傳送匯出請求。
