---
title: 擴展搜尋功能
description: 擴充搜尋功能： [!DNL Adobe Experience Manager Assets] 超出預設值。
contentOwner: AG
role: Developer
feature: Search
exl-id: 9e33d1c0-232b-458a-ad6a-f595aa541a5a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 19%

---

# 擴充資產搜尋 {#extending-assets-search}

您可以擴充 [!DNL Adobe Experience Manager Assets] 搜尋功能。 開箱即用 [!DNL Experience Manager Assets] 依字串搜尋資產。

搜尋是透過QueryBuilder介面完成，因此可以使用多個述詞自訂搜尋。 您可以覆蓋下列目錄中的預設述詞集： `/apps/dam/content/search/searchpanel/facets`.

您也可以將其他標籤新增至 [!DNL Assets] 管理面板。

>[!CAUTION]
>
>截至 [!DNL Experience Manager] 6.4，已棄用傳統UI。 Adobe建議使用觸控式UI。 如需自訂資訊，請參閱 [搜尋Facet](/help/assets/search-facets.md).

## 叠加 {#overlaying}

若要覆蓋預先設定的述詞，請複製 `facets` 節點來源 `/libs/dam/content/search/searchpanel` 至 `/apps/dam/content/search/searchpanel/` 或指定其他 `facetURL` 中的屬性 `searchpanel` 設定(預設為 `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`)。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>依預設，目錄結構位於 `/apps` 不存在，請建立它。 確保節點型別與以下節點型別相符 `/libs`.

## 新增標籤 {#adding-tabs}

您可以在中設定搜尋標籤，以新增其他搜尋標籤。 [!DNL Assets] 管理介面。 若要建立其他標籤：

1. 建立資料夾結構 `/apps/wcm/core/content/damadmin/tabs,`如果尚未存在，請複製 `tabs` 節點來源 `/libs/wcm/core/content/damadmin` 並貼上。
1. 視需要建立並設定第二個索引標籤。

   >[!NOTE]
   >
   >當您建立第二個時 `siteadminsearchpanel`，請務必設定 `id` 屬性以防止表單衝突。

## 建立自訂述詞 {#creating-custom-predicates}

[!DNL Assets] 隨附一組預先定義的述詞，可用於自訂「資產共用」頁面。 以這種方式自訂資產共用包含在 [建立和設定「資產共用」頁面](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

除了使用預先存在的述詞之外， [!DNL Experience Manager] 開發人員也可以使用建立自己的述詞 [查詢產生器API](/help/sites-developing/querybuilder-api.md).

建立自訂述詞需要基本的 [Widget框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

最佳實務是複製並調整現有述詞。 述詞範例位於 **/libs/cq/search/components/predicates**.

### 範例：建立簡單的屬性述詞 {#example-build-a-simple-property-predicate}

若要建置屬性述詞：

1. 例如，在專案目錄中建立元件資料夾 **/apps/weretail/components/titlepredicate**.
1. 新增 **content.xml**：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 添加 `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. 为了使组件可用，您需要能够对其进行编辑。要使组件可编辑，请在 CRXDE 中添加主类型 **cq:EditConfig** 的 **cq:editConfig** 节点。为了删除段落，请添加带有单个值 **DELETE** 的多值属性 **cq:actions**。
1. 導覽至您的瀏覽器，並在範例頁面上(例如， **press.html**)切換到設計模式並為述詞段落系統啟用新元件(例如， **left**)。

1. 在 **編輯** 模式，新元件現在可在sidekick中使用(可在 **搜尋** 群組)。 將元件插入 **述詞** 欄並輸入搜尋字詞，例如， **菱形** 並按一下放大鏡以開始搜尋。

   >[!NOTE]
   >
   >搜尋時，請務必準確輸入字詞，包括正確的大小寫。

### 範例：建立簡單的群組述詞 {#example-build-a-simple-group-predicate}

若要建立群組述詞：

1. 例如，在專案目錄中建立元件資料夾 **/apps/weretail/components/picspredicate**.
1. 新增 **content.xml**：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 新增 **titlepredicate.jsp**：

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. 为了使组件可用，您需要能够对其进行编辑。要使组件可编辑，请在 CRXDE 中添加主类型 **cq:EditConfig** 的 **cq:editConfig** 节点。为了删除段落，请添加带有单个值 **DELETE** 的多值属性 **cq:actions**。
1. 導覽至您的瀏覽器，並在範例頁面上(例如， **press.html**)切換到設計模式並為述詞段落系統啟用新元件(例如， **left**)。
1. 在 **編輯** 模式，新元件現在可在sidekick中使用(可在 **搜尋** 群組)。 將元件插入 **述詞** 欄。

## 已安裝的述詞Widget {#installed-predicate-widgets}

下列述詞可作為預先設定的ExtJS Widget使用。

### FulltextPredicate {#fulltextpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 述詞的名稱。 默认为 `fulltext` |
| searchCallback | 函数 | 用於觸發事件搜尋的回呼 `keyup`. 默认为 `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 述詞的名稱。 默认为 `property` |
| propertyName | 字符串 | JCR屬性的名稱。 默认为 `jcr:title` |
| 預設值 | 字符串 | 預填的預設值。 |

### 路徑述詞 {#pathpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 述詞的名稱。 默认为 `path` |
| rootPath | 字符串 | 述詞的根路徑。 默认为 `/content/dam` |
| pathFieldPredicateName | 字符串 | 默认为 `folder` |
| showFlatOption | 布尔值 | 標幟以顯示核取方塊 `search in subfolders`. 預設為true。 |

### DatePredicate {#datepredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 述詞的名稱。 默认为 `daterange` |
| propertyname | 字符串 | JCR屬性的名稱。 默认为 `jcr:content/jcr:lastModified` |
| 預設值 | 字符串 | 預填的預設值 |

### OptionsPredicate {#optionspredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| 标题 | 字符串 | 新增其他最上層標題 |
| predicateName | 字符串 | 述詞的名稱。 默认为 `daterange` |
| propertyname | 字符串 | JCR屬性的名稱。 默认为 `jcr:content/metadata/cq:tags` |
| 收合 | 字符串 | 收合層級。 默认为 `level1` |
| triggerSearch | 布尔值 | 檢查時觸發搜尋的旗標。 預設為false |
| searchCallback | 函数 | 用於觸發搜尋的回呼。 默认为 `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 数字 | 觸發searchCallback之前的逾時。 預設為800毫秒 |

## 自訂搜尋結果 {#customizing-search-results}

在「資產共用」頁面上顯示搜尋結果時，會受選取的鏡頭所控制。 [!DNL Experience Manager Assets] 隨附一組預先定義的鏡頭，可用於自訂「資產共用」頁面。 以這種方式自訂資產共用包含在 [建立和設定資產共用頁面](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

除了使用預先存在的鏡頭， [!DNL Experience Manager] 開發人員也可以建立自己的鏡頭。
