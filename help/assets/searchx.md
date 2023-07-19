---
title: 扩展搜索功能
description: 扩展搜索功能 [!DNL Adobe Experience Manager Assets] 超出默认值。
contentOwner: AG
role: Developer
feature: Search
exl-id: 9e33d1c0-232b-458a-ad6a-f595aa541a5a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 19%

---

# 扩展资源搜索 {#extending-assets-search}

您可以扩展 [!DNL Adobe Experience Manager Assets] 搜索功能。 开箱即用， [!DNL Experience Manager Assets] 按字符串搜索资产。

搜索通过QueryBuilder界面完成，因此可以使用多个谓词自定义搜索。 可以在以下目录中覆盖缺省谓词集： `/apps/dam/content/search/searchpanel/facets`.

您还可以将其他选项卡添加到 [!DNL Assets] “管理”面板。

>[!CAUTION]
>
>截至 [!DNL Experience Manager] 6.4，已弃用经典UI。 Adobe建议使用触屏优化UI。 有关自定义信息，请参阅 [搜索Facet](/help/assets/search-facets.md).

## 叠加 {#overlaying}

要覆盖预配置的谓词，请复制 `facets` 节点来源 `/libs/dam/content/search/searchpanel` 到 `/apps/dam/content/search/searchpanel/` 或指定另一个 `facetURL` 中的属性 `searchpanel` 配置(默认为 `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`)。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>默认情况下，目录结构位于 `/apps` 不存在，因此请创建它。 确保节点类型与以下节点类型匹配 `/libs`.

## 添加选项卡 {#adding-tabs}

您可以通过在以下位置配置其他搜索选项卡： [!DNL Assets] 管理界面。 要创建其他选项卡，请执行以下操作：

1. 创建文件夹结构 `/apps/wcm/core/content/damadmin/tabs,`如果该文件尚不存在，则复制 `tabs` 节点来源 `/libs/wcm/core/content/damadmin` 然后粘上。
1. 根据需要创建和配置第二个选项卡。

   >[!NOTE]
   >
   >当您创建第二个 `siteadminsearchpanel`，请务必设置 `id` 属性以防止表单冲突。

## 创建自定义谓词 {#creating-custom-predicates}

[!DNL Assets] 随附一组预定义谓词，可用于自定义资产共享页面。 通过此方式自定义资产共享包含在 [创建和配置“资产共享”页面](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

除了使用预先存在的谓词之外， [!DNL Experience Manager] 开发人员还可以使用创建自己的谓词 [查询生成器API](/help/sites-developing/querybuilder-api.md).

创建自定义谓词需要具备以下基本知识： [Widget框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

最佳实践是复制并调整现有谓词。 示例谓词位于 **/libs/cq/search/components/predicates**.

### 示例：构建简单属性谓词 {#example-build-a-simple-property-predicate}

要构建属性谓词，请执行以下操作：

1. 例如，在项目目录中创建组件文件夹 **/apps/weretail/components/titlepredicate**.
1. 添加 **content.xml**：

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
1. 导航到浏览器，并在示例页面上导航(例如， **press.html**)切换到设计模式并为谓词段落系统启用新组件(例如， **left**)。

1. In **编辑** 模式，新组件现在可在sidekick中使用(可在 **搜索** 组)。 将组件插入 **谓词** 列并键入搜索词，例如， **菱形** 然后单击放大镜开始搜索。

   >[!NOTE]
   >
   >搜索时，请确保键入正确的术语，包括正确的大小写。

### 示例：构建简单的组谓词 {#example-build-a-simple-group-predicate}

要构建组谓词，请执行以下操作：

1. 例如，在项目目录中创建组件文件夹 **/apps/weretail/components/picspredicate**.
1. 添加 **content.xml**：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 添加 **titlepredicate.jsp**：

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
   
           // Create a unique group ID; will return for example, "1_group".
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
1. 导航到浏览器，并在示例页面上导航(例如， **press.html**)切换到设计模式并为谓词段落系统启用新组件(例如， **left**)。
1. In **编辑** 模式，新组件现在可在sidekick中使用(可在 **搜索** 组)。 将组件插入 **谓词** 列。

## 已安装的谓词小组件 {#installed-predicate-widgets}

以下谓词可用作预配置的ExtJS小组件。

### 全文谓词 {#fulltextpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicatename | 字符串 | 谓词的名称。 默认为 `fulltext` |
| searchCallback | 函数 | 用于触发事件搜索的回调 `keyup`. 默认为 `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicatename | 字符串 | 谓词的名称。 默认为 `property` |
| propertyName | 字符串 | JCR属性的名称。 默认为 `jcr:title` |
| defaultvalue | 字符串 | 预填充的默认值。 |

### 路径谓词 {#pathpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicatename | 字符串 | 谓词的名称。 默认为 `path` |
| rootPath | 字符串 | 谓词的根路径。 默认为 `/content/dam` |
| pathFieldPredicateName | 字符串 | 默认为 `folder` |
| showFlatOption | 布尔值 | 用于显示复选框的标记 `search in subfolders`. 默认为true。 |

### DatePredicate {#datepredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicatename | 字符串 | 谓词的名称。 默认为 `daterange` |
| 属性名称 | 字符串 | JCR属性的名称。 默认为 `jcr:content/jcr:lastModified` |
| defaultvalue | 字符串 | 预填充的默认值 |

### OptionsPredicate {#optionspredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| 标题 | 字符串 | 添加其他顶部标题 |
| predicatename | 字符串 | 谓词的名称。 默认为 `daterange` |
| 属性名称 | 字符串 | JCR属性的名称。 默认为 `jcr:content/metadata/cq:tags` |
| 折叠 | 字符串 | 折叠级别。 默认为 `level1` |
| triggerSearch | 布尔值 | 用于在检查时触发搜索的标志。 默认为false |
| searchCallback | 函数 | 用于触发搜索的回调。 默认为 `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 数字 | 触发searchCallback之前的超时。 默认为800毫秒 |

## 自定义搜索结果 {#customizing-search-results}

资产共享页面上搜索结果的显示受所选镜头控制。 [!DNL Experience Manager Assets] 附带一组预定义镜头，可用于自定义资产共享页面。 通过此方式自定义资产共享包含在 [创建和配置资产共享页面](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

除了使用预先存在的镜片外， [!DNL Experience Manager] 开发商也可以自己制造镜头。
