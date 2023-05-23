---
title: 擴充Asset Editor
description: 瞭解如何使用自訂元件延伸Asset Editor的功能。
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 13%

---

# 擴充Asset Editor {#extending-asset-editor}

Asset Editor是點按透過Asset Share找到的資產時開啟的頁面，可讓使用者編輯資產的各個方面，例如中繼資料、縮圖、標題和標籤。

有關使用預先定義的編輯元件來設定編輯器的詳情，請參閱 [建立和設定Asset Editor頁面](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

除了使用現有的編輯器元件外， [!DNL Adobe Experience Manager] 開發人員也可以建立自己的元件。

## 建立資產編輯器範本 {#creating-an-asset-editor-template}

Geometrixx中包含下列範例頁面：

* Geometrixx範例頁面： `/content/geometrixx/en/press/asseteditor.html`
* 範例範本： `/apps/geometrixx/templates/asseteditor`
* 範例頁面元件： `/apps/geometrixx/components/asseteditor`

### 設定Clientlib {#configuring-clientlib}

[!DNL Assets] 元件使用WCM edit clientlib的擴充功能。 clientlibs通常會載入 `init.jsp`.

與預設clientlib載入(在核心的 `init.jsp`)，和 [!DNL Assets] 範本必須具備下列條件：

* 範本必須包含 `cq.dam.edit` clientlib (而非 `cq.wcm.edit`)。

* clientlib 还必须包含在禁用的 WCM 模式中（例如，在&#x200B;**发布**&#x200B;时加载）才能渲染谓词、操作和镜头。

在大多數情況下，複製現有的範例 `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`)應該可以滿足這些需求。

### 設定JS動作 {#configuring-js-actions}

部分 [!DNL Assets] 元件需要中定義的JS函式 `component.js`. 將此檔案複製到您的元件目錄並加以連結。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

此範例會在中載入此JavaScript來源 `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)。

### 其他樣式表 {#additional-style-sheets}

部分 [!DNL Assets] 元件使用Widget資料庫。 若要在內容內容內容中正確呈現，必須載入其他樣式表。 標籤動作元件還需要一個。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx樣式表 {#geometrixx-style-sheet}

範例頁面元件要求所有選取器開頭為 `.asseteditor` 之 `static.css` (`/etc/designs/geometrixx/static.css`)。 最佳實務：全部複製 `.asseteditor` 選取器至您的樣式表，並視需要調整規則。

### FormChooser：最終載入資源的調整 {#formchooser-adjustments-for-eventually-loaded-resources}

Asset Editor會使用「表單選擇器」，只要將表單選擇器和表單路徑新增至資產的URL，即可讓您編輯相同表單頁面上的資源（在此例中是資產）。

例如：

* 普通表單頁面： [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 資產已載入表單頁面： [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

中的範例控制代碼 `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`)執行下列動作：

* 它們會偵測資產是否已載入，或是否必須顯示純格式。
* 如果載入資產，則會停用WCM模式，因為parsys只能在純表單頁面上編輯。
* 如果資產已載入，使用者會使用其標題，而非表單頁面上的標題。

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

在HTML部分中，使用之前的標題集（資產或頁面標題）：

```html
<title><%= title %></title>
```

## 建立簡單的表單欄位元件 {#creating-a-simple-form-field-component}

此範例說明如何建立可顯示和顯示已載入資產中繼資料的元件。

1. 在專案目錄中建立元件資料夾，例如， `/apps/geometrixx/components/samplemeta`.
1. 新增 `content.xml` 包含以下程式碼片段：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 新增 `samplemeta.jsp` 包含以下程式碼片段：

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. 为了使组件可用，您需要能够对其进行编辑。若要讓元件可編輯，請在CRXDE Lite中新增節點 `cq:editConfig` 主要型別 `cq:EditConfig`. 为了删除段落，请添加带有单个值 `cq:actions` 的多值属性 `DELETE`。

1. 導覽至您的瀏覽器，並在範例頁面上(例如， `asseteditor.html`)切換至設計模式，並為段落系統啟用新元件。

1. 在&#x200B;**编辑**&#x200B;模式中，新组件（例如，**示例元数据**）现在可在 Sidekick 中使用（位于&#x200B;**资产编辑器**&#x200B;组中）。插入组件。要能够存储元数据，必须将其添加到元数据表单中。

## 修改中繼資料選項 {#modifying-metadata-options}

您可以修改中可用的名稱空間。 [中繼資料表單](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

目前可用的中繼資料定義於 `/libs/dam/options/metadata`：

* 此目錄中的第一個層級包含名稱空間。
* 每個名稱空間內的專案代表中繼資料，例如本機部分專案中的結果。
* 中繼資料內容包含型別和多值選項的資訊。

這些選項可以在下列位置被覆寫： `/apps/dam/options/metadata`：

1. 複製目錄來源 `/libs` 至 `/apps`.

1. 移除、修改或新增專案。

>[!NOTE]
>
>如果您新增名稱空間，必須在您的存放庫/CRX中註冊它們。 否則，提交中繼資料表單將會導致錯誤。
