---
title: 标记库
seo-title: 标记库
description: Granite、CQ和Sling标记库允许您访问特定函数，以便在模板和组件的JSP脚本中使用
seo-description: Granite、CQ和Sling标记库允许您访问特定函数，以便在模板和组件的JSP脚本中使用
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: de5eb53f6160991ca0718d61afaeed2078a4fa88
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 0%

---

# 标记库{#tag-libraries}

Granite、CQ和Sling标记库允许您访问特定函数，以在模板和组件的JSP脚本中使用。

## Granite标记库 {#granite-tag-library}

Granite标记库包含有用的函数。

在开发Granite UI组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全局还声明了[Sling库](/help/sites-developing/taglib.md#sling-tag-library)。

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeclientlib> {#ui-includeclientlib}

`<ui:includeClientLib>`标记包含AEM html客户端库，该客户端库可以是js、css或主题库。 对于不同类型（例如js和css）的多个包含项，此标记需要在jsp中多次使用。 此标记是` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`服务接口的方便包装器。

它具有以下属性：

**类别**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有Javascript和CSS库。 主题名称将从请求中提取。

等同于：`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**主题**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有与主题相关的库（CSS和JS）。 主题名称将从请求中提取。

等同于：`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有Javascript库。

等同于：`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  — 以逗号分隔的客户端库类别列表。这将包含给定类别的所有CSS库。

等同于：`com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主题**  — 应包含仅指示主题库或非主题库的标记。如果忽略，则包含这两个集。 仅适用于纯JS或CSS包含项（不适用于类别或主题包含项）。

`<ui:includeClientLib>`标记可在jsp中使用如下：

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## CQ标记库 {#cq-tag-library}

CQ标记库包含有用的函数。

要在脚本中使用CQ标记库，脚本必须以以下代码开头：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>当`/libs/foundation/global.jsp`文件包含在脚本中时，将自动声明taglib。

在开发AEM组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它声明了sling、CQ和jstl taglibs，并公开了由[ `<cq:defineObjects />`](#amp-lt-cq-defineobjects)标记定义的常规脚本对象。 这可缩短并简化组件的jsp代码。

### &lt;cq:text> {#cq-text}

`<cq:text>`标记是一个方便的标记，用于在JSP中输出组件文本。

它具有以下可选属性：

**属性**  — 要使用的属性的名称。该名称相对于当前资源。

**value**  — 用于输出的值。如果存在此属性，则会覆盖属性属性的使用。

**oldValue**  — 用于差异输出的值。如果存在此属性，则会覆盖属性属性的使用。

**escXml**  — 定义是否应将结果字 &lt;>符串中的字符、&amp;、“和”转换为相应的字符实体代码。默认值为 false。请注意，转义在可选格式后应用。

**format**  — 可选的java.text.Format，用于设置文本格式。

**noDiff**  — 禁止计算差异输出，即使存在差异信息也是如此。

**tagClass**  — 将包围非空输出的元素的CSS类名称。如果为空，则不会添加任何元素。

**tagName**  — 将包围非空输出的元素的名称。默认为DIV。

**占位符**  — 在编辑模式（即占位符）中用于null或空文本的默认值。请注意，默认检查在可选格式和转义之后执行，即按原样写入输出。 默认为：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**默认**  — 用于空或空文本的默认值。请注意，默认检查在可选格式和转义之后执行，即按原样写入输出。

如何在JSP中使用`<cq:text>`标记的一些示例：

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setcontentbundle> {#cq-setcontentbundle}

`<cq:setContentBundle>`标记会创建i18n本地化上下文并将其存储在`javax.servlet.jsp.jstl.fmt.localizationContext`配置变量中。

它具有以下属性：

**语言**  — 用于检索资源包的区域设置语言。

**source**  — 应从中获取区域设置的源。它可以设置为以下值之一：

* **静态**  — 区域设置从属性(如果可 `language` 用)中获取，否则从服务器默认区域设置中获取。

* **page**  — 区域设置采用当前页面或资源的语言（如果可用），否则采用属性(如果可 `language` 用)，否则采用服务器默认区域设置。

* **request**  — 区域设置是从请求区域设置( `request.getLocale()`)中获取的。

* **自动**  — 区域设置从属性(如果可 `language` 用)获取，否则从当前页面或资源的语言（如果可用）获取，或从请求获取。

如果未设置`source`属性：

* 如果设置了`language`属性，则`source`属性将默认为“ `static`”。

* 如果未设置`language`属性，则`source`属性将默认为`auto`。

标准JSTL `<fmt:message>`标记只能使用“内容包”。 按键查找消息的方式有两种：

1. 首先，搜索当前呈现的基础资源的JCR属性以查找转换。 这允许您定义一个简单的组件对话框来编辑这些值。
1. 如果节点不包含与键完全相同的名称属性，则回退是从sling请求(`SlingHttpServletRequest.getResourceBundle(Locale)`)加载资源包。 此包的语言或区域设置由`<cq:setContentBundle>`标记的语言和源属性定义。

`<cq:setContentBundle>`标记可在jsp中按如下方式使用。

对于定义其语言的页面：

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

对于用户个性化页面：

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

`<cq:include>`标记将资源包含到当前页面中。

它具有以下属性：

**刷新**

* 一个布尔值，用于定义是否在包含目标之前刷新输出。

**路径**

* 要包含在当前请求处理中的资源对象的路径。 如果此路径是相对的，则会将其附加到脚本包含给定资源的当前资源的路径中。 必须指定path和resourceType或脚本。

**resourceType**

* 要包含的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的确切路径：在这种情况下，不支持向路径添加参数、选择器和扩展。
* 如果要包含的资源是使用路径属性指定的，而路径属性不能解析为资源，则标记可以创建路径外的合成资源对象和此资源类型。
* 必须指定path和resourceType或脚本。

**脚本**

* 要包含的jsp脚本。 必须指定path和resourceType或脚本。

**ignoreComponentHierarchy**

* 一个布尔值，用于控制是否应忽略组件层次结构以进行脚本解析。 如果为true，则仅遵守搜索路径。

**示例:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

是否应使用`<%@ include file="myScript.jsp" %>`或`<cq:include script="myScript.jsp" %>`来包含脚本？

* `<%@ include file="myScript.jsp" %>`指令通知JSP编译器将一个完整文件包含到当前文件中。 就好像所包含文件的内容被直接粘贴到原始文件中一样。
* 使用`<cq:include script="myScript.jsp">`标记时，文件将包含在运行时。

您应使用`<cq:include>`还是`<sling:include>`?

* 开发AEM组件时，Adobe建议您使用`<cq:include>`。
* `<cq:include>` 允许您在使用script属性时直接按名称包含脚本文件。这会考虑组件和资源类型继承，并且通常比严格遵循使用选择器和扩展的Sling脚本解析更简单。

### &lt;cq:includeclientlib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自AEM 5.6起已弃用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 应改用。

`<cq:includeClientLib>`标记包含AEM html客户端库，该客户端库可以是js、css或主题库。 对于不同类型（例如js和css）的多个包含项，此标记需要在jsp中多次使用。 此标记是`com.day.cq.widget.HtmlLibraryManager`服务接口的方便包装器。

它具有以下属性：

**类别**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有Javascript和CSS库。 主题名称将从请求中提取。

等同于：`com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**主题**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有与主题相关的库（CSS和JS）。 主题名称将从请求中提取。

等同于：`com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  — 以逗号分隔的客户端库类别列表。这将包括给定类别的所有Javascript库。

等同于：`com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  — 以逗号分隔的客户端库类别列表。这将包含给定类别的所有CSS库。

等同于：`com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主题**  — 应包含仅指示主题库或非主题库的标记。如果忽略，则包含这两个集。 仅适用于纯JS或CSS包含项（不适用于类别或主题包含项）。

`<cq:includeClientLib>`标记可在jsp中使用如下：

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineobjects> {#cq-defineobjects}

`<cq:defineObjects>`标记会公开以下经常使用的脚本对象，开发人员可以引用这些对象。 它还会公开由[ `<sling:defineObjects>`](#amp-lt-sling-defineobjects)标记定义的对象。

**componentContext**

* 请求的当前组件上下文对象(com.day.cq.wcm.api.components.ComponentContext接口)。

**组件**

* 当前资源的当前AEM组件对象(com.day.cq.wcm.api.components.Component接口)。

**currentDesign**

* 当前页面的当前设计对象(com.day.cq.wcm.api.designer.Design界面)。

**currentPage**

* 当前AEM WCM页面对象(com.day.cq.wcm.api.Page接口)。

**currentStyle**

* 当前单元格的当前样式对象(com.day.cq.wcm.api.designer.Style接口)。

**设计器**

* 用于访问设计信息(com.day.cq.wcm.api.designer.Designer界面)的designer对象。

**editContext**

* AEM组件的编辑上下文对象(com.day.cq.wcm.api.components.EditContext接口)。

**pageManager**

* 页面级操作的页面管理器对象(com.day.cq.wcm.api.PageManager界面)。

**pageProperties**

* 当前页面的页面属性对象(org.apache.sling.api.resource.ValueMap)。

**属性**

* 当前资源的属性对象(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 资源页面的设计对象(com.day.cq.wcm.api.designer.Design界面)。

**resourcePage**

* 资源页面对象(com.day.cq.wcm.api.Page接口)。
* 它具有以下属性：

**requestName**

* 从sling继承

**responseName**

* 从sling继承

**resourceName**

* 从sling继承

**nodeName**

* 从sling继承

**logName**

* 从sling继承

**resourceResolverName**

* 从sling继承

**slingName**

* 从sling继承

**componentContextName**

* 特定于wcm

**editContextName**

* 特定于wcm

**propertiesName**

* 特定于wcm

**pageManagerName**

* 特定于wcm

**currentPageName**

* 特定于wcm

**resourcePageName**

* 特定于wcm

**pagePropertiesName**

* 特定于wcm

**componentName**

* 特定于wcm

**designerName**

* 特定于wcm

**currentDesignName**

* 特定于wcm

**resourceDesignName**

* 特定于wcm

**currentStyleName**

* 特定于wcm

**示例**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>当脚本中包含`/libs/foundation/global.jsp`文件时，将自动包含`<cq:defineObjects />`标记。

### &lt;cq:requesturl> {#cq-requesturl}

`<cq:requestURL>`标记将当前请求URL写入JspWriter。 两个标记[ `<cq:addParam>`](#amp-lt-cq-addparam)和[ `<cq:removeParam>`](#amp-lt-cq-removeparam)可在此标记正文中使用，以在写入之前修改当前请求URL。

它允许您使用不同参数创建指向当前页面的链接。 例如，它允许您转换请求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用`addParam`或`removeParam`只会更改给定参数的出现情况，所有其他参数都不会受到影响。

`<cq:requestURL>` 没有任何属性。

示例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addparam> {#cq-addparam}

`<cq:addParam>`标记会向封闭的[ `<cq:requestURL>`](#amp-lt-cq-requesturl)标记中添加具有给定名称和值的请求参数。

它具有以下属性：

**name**

* 要添加的参数的名称

**选定**

* 要添加的参数的值

**示例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeparam> {#cq-removeparam}

`<cq:removeParam>`标记会从封闭的[ `<cq:requestURL>`](#amp-lt-cq-requesturl)标记中删除具有给定名称和值的请求参数。 如果未提供值，则删除所有具有给定名称的参数。

它具有以下属性：

**name**

* 要删除的参数的名称

示例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling标记库 {#sling-tag-library}

Sling标记库包含有用的Sling函数。

当您在脚本中使用Sling标签库时，脚本必须以以下代码开头：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>当脚本中包含`/libs/foundation/global.jsp`文件时，将自动声明sling taglib。

### &lt;sling:include> {#sling-include}

`<sling:include>`标记将资源包含到当前页面中。

它具有以下属性：

**刷新**

* 一个布尔值，用于定义是否在包含目标之前刷新输出。

**资源**

* 要包含在当前请求处理中的资源对象。 必须指定资源或路径。 如果同时指定了这两者，则资源优先。

**路径**

* 要包含在当前请求处理中的资源对象的路径。 如果此路径是相对的，则会将其附加到脚本包含给定资源的当前资源的路径中。 必须指定资源或路径。 如果同时指定了这两者，则资源优先。

**resourceType**

* 要包含的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的确切路径：在这种情况下，不支持向路径添加参数、选择器和扩展。
* 如果要包含的资源是使用路径属性指定的，而路径属性不能解析为资源，则标记可以创建路径外的合成资源对象和此资源类型。

**replaceSelectors**

* 调度时，选择器将被替换为此属性的值。

**addSelectors**

* 调度时，此属性的值会添加到选择器中。

**replaceSuffix**

* 调度时，后缀会被此属性的值替换。

>[!NOTE]
>
>`<sling:include>`标记中包含的资源和脚本的分辨率与普通sling URL分辨率相同。 默认情况下，选择器、扩展等 当前请求中的还将用于已包含的脚本。 可以通过标记属性修改它们：例如，`replaceSelectors="foo.bar"`允许覆盖选择器。

示例：

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineobjects> {#sling-defineobjects}

`<sling:defineObjects>`标记会公开以下经常使用的脚本对象，开发人员可以引用这些对象：

**slingRequest**

* SlingHttpServletRequest对象，提供对HTTP请求标头信息的访问 — 扩展标准HttpServletRequest — 并提供对特定于Sling的内容（如资源、路径信息、选择器等）的访问。

**slingResponse**

* SlingHttpServletResponse对象，提供对服务器创建的HTTP响应的访问权限。 此参数当前与从中扩展的HttpServletResponse相同。**请求**
* 标准JSP请求对象，它是纯HttpServletRequest。**响应**
* 标准JSP响应对象，它是纯HttpServletResponse。

**resourceResolver**

* 当前ResourceResolver对象。 它与slingRequest.getResourceResolver()相同

.**sling**

* SlingScriptHelper对象，包含脚本的便利方法，主要是sling.include(&#39;/some/other/resource&#39;)，用于在此响应中包含其他资源的响应(例如 嵌入标头html代码段)和sling.getService(foo.bar.Service.class)，以检索Sling（类表示法，具体取决于脚本语言）中提供的OSGi服务。

**资源**

* 要处理的当前资源对象，具体取决于请求的URL。 它与slingRequest.getResource()相同。

**currentNode**

* 如果当前资源指向JCR节点（Sling中通常为此情况），则允许直接访问Node对象。 否则，此对象将未定义。

**日志**

* 提供SLF4J日志记录器，用于从脚本(例如 log.info（&quot;正在执行我的脚本&quot;）。

* 它具有以下属性：

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**示例:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL标记库 {#jstl-tag-library}

[JavaServer Pages标准标记库](https://www.oracle.com/technetwork/java/index-jsp-135995.html)包含许多有用的标准标记。 核心、格式和函数标签由`/libs/foundation/global.jsp`定义，如以下代码片段中所示。

### /libs/foundation/global.jsp的提取 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

按照之前所述导入`/libs/foundation/global.jsp`文件后，可以使用`c`、`fmt`和`fn`前缀访问这些标签。 JSTL的官方文档位于[The Java EE 5 Tutorial - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)。
