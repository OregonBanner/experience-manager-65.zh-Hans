---
title: 扩展Adobe Experience Manager Assets的搜索功能
description: 将Adobe Experience Manager资产的搜索功能扩展到默认值之外。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 扩展资产搜索 {#extending-assets-search}

您可以扩展 [!DNL Adobe Experience Manager Assets] 搜索功能。 开箱即用，按字 [!DNL Experience Manager Assets] 符串搜索资产。

搜索通过QueryBuilder界面完成，因此可以使用多个谓词自定义搜索。 您可以在以下目录中叠加默认的谓词集： `/apps/dam/content/search/searchpanel/facets`.

您还可以向管理员面板添加其他 [!DNL Assets] 选项卡。

>[!CAUTION]
>
>自6. [!DNL Experience Manager] 4起，已弃用经典UI。 有关公告，请参 [阅已弃用和已删除的功能](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html)。 Adobe建议使用触屏优化UI。 有关自定义，请参阅 [搜索彩块化](/help/assets/search-facets.md)。

## 叠加 {#overlaying}

要叠加预配置的谓词，请将节点从复 `facets` 制到配置中，或在配 `/libs/dam/content/search/searchpanel` 置中指定其他 `/apps/dam/content/search/searchpanel/` 属性(默认为 `facetURL``searchpanel``/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`to)。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>默认情况下，/下的目录结 `apps` 构不存在，需要创建。 确保节点类型与／下的节点类型匹配 `libs`。

## 添加选项卡 {#adding-tabs}

您可以通过在AEM资产管理员中配置其他搜索选项卡来添加这些选项卡。 要创建其他选项卡，请执行以下操作：

1. 如果文件夹结 `/apps/wcm/core/content/damadmin/tabs,`构尚不存在，请创建该结构，然后从中复 `tabs` 制并粘 `/libs/wcm/core/content/damadmin` 贴该结构。
1. 根据需要创建和配置第二个选项卡。

   >[!NOTE]
   >
   >创建第二个表 `siteadminsearchpanel`单时，请务必设置一 `id` 个属性以防止表单冲突。

## 创建自定义谓词 {#creating-custom-predicates}

[!DNL Assets] 附带一组预定义谓词，可用于自定义资产共享页面。 以这种方式自定义资产共享在创建和配 [置资产共享页面中有介绍](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)。

除了使用预先存在的谓词，AEM开发人员还可以使用 [查询Builder API创建自己的谓词](/help/sites-developing/querybuilder-api.md)。

创建自定义谓词需要有关构件框架的 [基本知识](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)。

最佳实践是复制现有谓词并对其进行调整。 示例谓词位于 **/libs/cq/search/components/谓词中**。

### 示例：构建简单属性谓词 {#example-build-a-simple-property-predicate}

要构建属性谓词，请执行以下操作：

1. 在项目目录中创建组件文件夹，例如 **/apps/geometrixx/components/titlepredicate**。
1. 添 **加content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 将 `titlepredicate.jsp`.

   ```xml
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
1. 导航到浏览器，在示例页面(例如， **press.html**)上切换到设计模式，为谓词段落系统启用新组件(例如， **left**)。

1. 在“ **编辑** ”模式中 **，新组件现在可在Sidekick中使用(在“搜索”组中** 找到)。 将组件插入谓 **词列** ，然后键入搜索词(例如， **Diamond** )，然后单击放大镜以开始搜索。

   >[!NOTE]
   >
   >搜索时，请务必准确键入术语，包括正确的大小写。

### 示例：构建简单的用户组谓词 {#example-build-a-simple-group-predicate}

要构建用户组谓词，请执行以下操作：

1. 在项目目录中创建组件文件夹，例如 **/apps/geometrixx/components/picspredicate。**
1. 添 **加content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 添 **加titlepredicate.jsp**:

   ```xml
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
1. 导航到浏览器，在示例页面(例如， **press.html**)上切换到设计模式，为谓词段落系统启用新组件(例如， **left**)。
1. 在“ **编辑** ”模式中 **，新组件现在可在Sidekick中使用(在“搜索”组中** 找到)。 将组件插入谓 **词列** 。

## 已安装的谓词构件 {#installed-predicate-widgets}

以下谓词可用作预配置的ExtJS构件。

### 全文谓词 {#fulltextpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 谓词的名称。 默认为 `fulltext` |
| searchCallback | 函数 | 回调以在事件上触发搜索 `keyup`。 默认为 `CQ.wcm.SiteAdmin.doSearch` |

### 属性谓词 {#propertypredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 谓词的名称。 默认为 `property` |
| propertyName | 字符串 | JCR属性的名称。 默认为 `jcr:title` |
| defaultValue | 字符串 | 预填充的默认值。 |

### 路径谓词 {#pathpredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 谓词的名称。 默认为 `path` |
| rootPath | 字符串 | 谓词的根路径。 默认为 `/content/dam` |
| pathFieldPredicateName | 字符串 | 默认为 `folder` |
| showFlatOption | 布尔型 | 显示复选框的标记 `search in subfolders`。 默认设置为 true。 |

### 日期谓词 {#datepredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| predicateName | 字符串 | 谓词的名称。 默认为 `daterange` |
| propertyname | 字符串 | JCR属性的名称。 默认为 `jcr:content/jcr:lastModified` |
| defaultValue | 字符串 | 预填充的默认值 |

### 选项谓词 {#optionspredicate}

| 属性 | 类型 | 描述 |
|---|---|---|
| 页面 | 字符串 | 添加其他顶部标题 |
| predicateName | 字符串 | 谓词的名称。 默认为 `daterange` |
| propertyname | 字符串 | JCR属性的名称。 默认为 `jcr:content/metadata/cq:tags` |
| 折叠 | 字符串 | 折叠级别。 默认为 `level1` |
| triggerSearch | 布尔型 | 用于在选中时触发搜索的标记。 默认为false |
| searchCallback | 函数 | 回调以触发搜索。 默认为 `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 数字 | 触发searchCallback之前的超时。 默认为800毫秒 |

## 自定义搜索结果 {#customizing-search-results}

在“资源共享”页面上显示搜索结果受所选镜头的约束。 AEM资产附带一组预定义的镜头，可用于自定义资产共享页面。 以这种方式自定义资产共享在创建和配 [置资产共享页面中有介绍](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)。

除了使用预先存在的镜头外，AEM开发人员还可以创建他们自己的镜头。
