---
title: 開發大量編輯器
seo-title: Developing the Bulk Editor
description: 標籤可讓內容分類並整理
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---

# 開發大量編輯器{#developing-the-bulk-editor}

本節說明如何開發大量編輯器工具，以及如何擴充產品清單元件（以大量編輯器為基礎）。

## 大量編輯器查詢引數 {#bulk-editor-query-parameters}

使用大量編輯器時，您可以將多個查詢引數新增到URL中，以使用特定設定呼叫大量編輯器。 如果您希望大量編輯器一律搭配特定設定使用（例如，如同在產品清單元件中使用），則您需要修改bulkeditor.jsp （位於/libs/wcm/core/components/bulkeditor）或建立具有特定設定的元件。 使用查詢引數所做的變更不是永久性的。

例如，如果您在瀏覽器的URL中鍵入以下內容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

顯示大量編輯器，但不包含 **根路徑** 欄位為hrp=true會隱藏欄位。 使用引數hrp=false，會顯示欄位（預設值）。

以下是大量編輯器查詢引數的清單：

>[!NOTE]
>
>每個引數都可以有一個長名稱和短名稱。 例如，搜尋根路徑的完整名稱是 `rootPath`，簡短的一點是 `rp`. 如果未定義長名稱，則會從請求中讀取短名稱。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 参数</p> <p>（長名稱/短名稱）<br /> </p> </td>
   <td> 类型 <br /> </td>
   <td> 描述 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 字符串 </td>
   <td> 搜尋根路徑</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 字符串</td>
   <td> 搜尋查詢</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> 布尔值</td>
   <td> 為true時，會啟用內容模式<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 字符串[]</td>
   <td> 搜尋的屬性（colsSelection中核取的值顯示為核取方塊）</td>
  </tr>
  <tr>
   <td> 額外欄位/ec<br /> </td>
   <td> 字符串[]</td>
   <td> 額外的搜尋屬性（顯示在逗號分隔的文字欄位中）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 布尔值</td>
   <td> 為true時，會在頁面載入時執行查詢<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> 字符串[]</td>
   <td> 搜尋的屬性選取範圍（顯示為核取方塊）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布尔值</td>
   <td> 為true時，僅顯示格線，而不顯示搜尋面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> 布尔值</td>
   <td> 為true時，搜尋面板會在載入時收合</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布尔值</td>
   <td> 為true時，隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布尔值</td>
   <td> 為true時，隱藏查詢欄位</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏欄選擇欄位</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> 布尔值</td>
   <td> 為true時，隱藏額外的欄欄位</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏搜尋按鈕</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏儲存按鈕</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏匯出按鈕</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏匯入按鈕</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏格線搜尋結果編號文字</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏格點插入按鈕</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏格點刪除按鈕</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布尔值</td>
   <td> 為true時，會隱藏格線「路徑」欄</td>
  </tr>
 </tbody>
</table>

### 開發以大量編輯器為基礎的元件：產品清單元件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本節提供如何使用大量編輯器的概觀，並說明以大量編輯器為基礎的現有Geometrixx元件：產品清單元件。

產品清單元件可讓使用者顯示和編輯資料表。 例如，您可以使用產品清單元件來代表目錄中的產品。 此資訊會顯示在標準HTML表格中，且任何編輯都會在 **編輯** 對話方塊，其中包含BulkEditor Widget。 (此大量編輯器與在/etc/importers/bulkeditor.html或透過「工具」功能表存取的編輯器完全相同)。 產品清單元件已針對特定、有限的大量編輯器功能進行設定。 可以設定大量編輯器的每個部分（或衍生自大量編輯器的元件）。

使用大量編輯器，您可以新增、修改、刪除、篩選和匯出列、儲存修改和匯入一組列。 每一列都會儲存為「產品清單」元件實體本身的節點。 每個儲存格都是每個節點的屬性。 這是設計選擇，可以輕鬆變更，例如，您可以將節點儲存在存放庫中的其他位置。 查詢servlet的角色是傳回要顯示的節點清單；搜尋路徑被定義為產品清單執行個體。

產品清單元件的原始程式碼可在存放庫中的/apps/geometrixx/components/productlist取得，並且由幾個部分組成，例如所有AEM元件：

* HTML呈現：呈現會在JSP檔案(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP會讀取目前「產品清單」元件的子節點，並將每個子節點顯示為HTML表格的一列。
* 「編輯」對話方塊，您可在其中定義「大量編輯器」設定。 設定對話方塊以符合元件的需求：可用的欄以及在格線或搜尋時可能執行的動作。 另請參閱 [大量編輯器設定屬性](#bulk-editor-configuration-properties) 以取得所有設定屬性的資訊。

以下是對話方塊子節點的XML表示法：

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### 大量編輯器設定屬性 {#bulk-editor-configuration-properties}

可設定大量編輯器的每個部分。 下表列出大量編輯器的所有組態屬性。

<table>
 <tbody>
  <tr>
   <td>属性名称</td>
   <td>定义</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>搜尋根路徑</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>搜索查询</td>
  </tr>
  <tr>
   <td>內容模式</td>
   <td>True表示啟用內容模式：在jcr：content節點上讀取屬性，而不是在搜尋結果節點上讀取屬性</td>
  </tr>
  <tr>
   <td>欄值</td>
   <td>搜尋的屬性（colsSelection中核取的值顯示為核取方塊）</td>
  </tr>
  <tr>
   <td>額外欄位</td>
   <td>額外的搜尋屬性（以逗號分隔的文字欄位顯示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>若為True，則在頁面載入時執行查詢</td>
  </tr>
  <tr>
   <td>欄選取</td>
   <td>搜尋的屬性選取範圍（顯示為核取方塊）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True表示只顯示格線而不顯示搜尋面板（別忘了將initialSearch設為true）</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True表示依預設摺疊搜尋面板</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td>隱藏查詢引數</td>
   <td>隱藏查詢欄位</td>
  </tr>
  <tr>
   <td>隱藏內容模式</td>
   <td>隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>隱藏欄選取欄位</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>隱藏額外欄位</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>隱藏搜尋按鈕</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>隱藏儲存按鈕</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>隱藏匯出按鈕</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>隱藏匯入按鈕</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>隱藏格線搜尋結果編號文字</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>隱藏格點插入按鈕</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>隱藏格線刪除按鈕</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>隱藏格線「路徑」欄</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>查詢servlet的路徑</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>匯出servlet的路徑</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>匯入servlet的路徑</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>插入列時新增到節點的資源型別</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>儲存按鈕Widget設定</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>搜尋按鈕Widget設定</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>匯出按鈕Widget設定</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>匯入按鈕Widget設定</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>搜尋面板Widget設定</td>
  </tr>
  <tr>
   <td>格線</td>
   <td>格線Widget設定</td>
  </tr>
  <tr>
   <td>儲存</td>
   <td>存放區設定</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>格線欄模型設定</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>rootPath widget config</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams Widget設定</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode Widget設定</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection Widget設定</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols Widget設定</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>欄中繼資料設定。 可能的屬性包括（套用至欄中的所有儲存格）： <br />
    <ul>
     <li>cellStyle： html樣式 </li>
     <li>cellCls： css類別 </li>
     <li>readOnly： true表示無法變更值 </li>
     <li>checkbox： true可將欄的所有儲存格定義為核取方塊（true/false值） </li>
     <li>forcedPosition：整數值，指定資料行必須放置在格線中的位置（介於0和資料行數目–1之間）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 欄中繼資料設定 {#columns-metadata-configuration}

您可以為每個欄設定：

* 顯示屬性：html樣式、CSS類別和唯讀

* 核取方塊
* 強制位置

CSS和唯讀欄

大量編輯器有三種欄設定：

* 儲存格CSS類別名稱(cellCls)：新增至已設定欄之每個儲存格的CSS類別名稱。
* 儲存格樣式(cellStyle)：新增至已設定欄之每個儲存格的HTML樣式。
* 唯讀(readOnly)：已設定欄的每個儲存格都會設定為唯讀。

設定必須定義為下列設定：

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

以下範例可在productlist元件(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)中找到：

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**复选框**

如果核取方塊設定屬性設為true，欄中的所有儲存格都會呈現為核取方塊。 核取方塊會傳送 **true** 至伺服器儲存servlet， **false** 否則。 在頁首功能表中，您也可以 **全選** 或 **全部不選**. 如果選取的標題是核取方塊欄的標題，則會啟用這些選項。

在前一個範例中，選取欄僅包含核取方塊，如checkbox=&quot;true&quot;。

**強制位置**

強制位置中繼資料forcedPosition可讓您指定欄在格線中的放置位置：0是第一個位置，而 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1是最後一個位置。 任何其他值将被忽略。 

在前一個範例中，選取欄是第一欄，如forcedPosition=&quot;0&quot;。

### 查詢Servlet {#query-servlet}

依預設，查詢servlet可在以下位置找到： `/libs/wcm/core/components/bulkeditor/json.java`. 您可以設定其他路徑來擷取資料。

查詢servlet的運作方式如下：它接收GQL查詢和要傳回的欄、計算結果，並將結果以JSON資料流的形式傳回大量編輯器。

在產品清單元件案例中，傳送至查詢servlet的兩個引數如下：

* 查詢： &quot;path：/content/geometrixx/en/customers/jcr：content/par/productlist Cube&quot;
* 欄位： &quot;Selection、ProductId、ProductName、Color、CatalogCode、SellingSku&quot;

而傳回的JSON資料流如下：

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

每個點選都會對應一個節點及其屬性，並在格線中顯示為一列。

您可以擴充查詢servlet以傳回複雜的繼承模型，或傳回儲存在特定邏輯位置的節點。 查詢servlet可用於執行任何型別的複雜計算。 然後，網格會顯示儲存庫中數個節點的彙總列。 在這種情況下，這些列的修改和儲存必須由「儲存Servlet」管理。

### 儲存Servlet {#save-servlet}

在大量編輯器的預設設定中，每一列都是一個節點，而且此節點的路徑會儲存在列記錄中。 大量編輯器會透過jcr路徑保持列和節點之間的連結。 當使用者編輯格線時，會建立所有修改的清單。 當使用者點按 **儲存**，系統就會傳送POST查詢至具有更新屬性值的每個路徑。 這是Sling概念的基礎，如果每個儲存格都是節點的屬性，則運作良好。 但是，如果實施查詢servlet來執行繼承計算，則此模型無法運作，因為查詢servlet傳回的屬性可以從另一個節點繼承。

「儲存servlet」概念是修改不會直接發佈到每個節點，而是發佈到執行儲存工作的servlet。 此servlet可分析修改並將屬性儲存在正確的節點上。

每個更新的屬性都會以下列格式傳送至servlet：

* 引數名稱： &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   範例： /content/geometrixx/en/products/jcr：content/par/productlist/1258674859000/SellingSku

* 值： &lt;value>

   示例: 12123

此servlet需要知道catalogCode屬性的儲存位置。

預設的「儲存servlet」實作可在/libs/wcm/bulkeditor/save/POST.jsp取得，並用於產品清單元件。 它會從請求中取得所有引數(使用 &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> 格式化)，並在使用JCR API的節點上寫入屬性。 如果節點不存在，它也會建立節點（網格插入列）。

不應使用預設程式碼，因為它會重新實作伺服器的原生功能(POST於 &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>)，因此只是建置將管理屬性繼承模型的「儲存servlet」的良好起點。
