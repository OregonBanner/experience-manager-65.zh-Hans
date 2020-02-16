---
title: 标签库
seo-title: 标签库
description: Granite、CQ和Sling标签库允许您访问特定函数，以用于模板和组件的JSP脚本
seo-description: Granite、CQ和Sling标签库允许您访问特定函数，以用于模板和组件的JSP脚本
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 标签库{#tag-libraries}

Granite、CQ和Sling标签库允许您访问特定函数，以便在模板和组件的JSP脚本中使用。

## Granite标签库 {#granite-tag-library}

Granite标签库包含有用的函数。

在开发Granite UI组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全局还声明 [Sling库](/help/sites-developing/taglib.md#sling-tag-library)。

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

标 `<ui:includeClientLib>` 记包括AEM html客户端库，它可以是js、css或主题库。 对于不同类型的多个包含项（例如js和css），此标记需要在jsp中多次使用。 此标签是服务界面周围的便 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 利包装器。

它具有以下属性：

**类别** -以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript和CSS库。 主题名称从请求中提取。

等效于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**theme** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有主题相关库（CSS和JS）。 主题名称从请求中提取。

等效于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript库。

等效于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有CSS库。

等效于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主题** -应包含仅指示主题或非主题库的标志。 如果省略，则包括这两个集。 仅适用于纯JS或CSS包含（不适用于类别或主题包含）。

标 `<ui:includeClientLib>` 记可在jsp中使用如下：

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

## CQ标签库 {#cq-tag-library}

CQ标签库包含有用的函数。

要在脚本中使用CQ标签库，脚本必须以下代码开头：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>当该文 `/libs/foundation/global.jsp` 件包含在脚本中时，将自动声明taglib。

在开发AEM组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它声明sling、CQ和jstl标签，并公开由标签定义的常规使用的脚本对 [`<cq:defineObjects />`](#amp-lt-cq-defineobjects) 象。 这缩短了并简化了组件的jsp代码。

### <cq:text> {#cq-text}

该标 `<cq:text>` 签是一个便捷的标签，它输出JSP中的组件文本。

它具有以下可选属性：

**property** —— 要使用的属性的名称。 该名称相对于当前资源。

**value** —— 用于输出的值。 如果此属性存在，则它将覆盖属性属性的使用。

**oldValue** —— 用于diff输出的值。 如果此属性存在，则它将覆盖属性属性的使用。

**escapeXml** —— 定义生成字符串中的字符&lt;、>、&amp;、&#39;和&quot;是否应转换为相应的字符实体代码。 默认值为 false。请注意，转义在可选格式设置之后应用。

**format** —— 用于设置文本格式的可选java.text.Format。

**noDiff** —— 抑制差异输出的计算，即使存在差异信息也是如此。

**tagClass** —— 将在非空输出周围的元素的CSS类名称。 如果为空，则不添加任何元素。

**tagName** —— 将在非空输出周围的元素的名称。 默认为DIV。

**占位符** -用于编辑模式（即占位符）中空文本或空文本的默认值。 请注意，默认检查是在可选格式设置和转义之后执行的，即按原样写入输出。 默认为：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** —— 用于null或空文本的默认值。 请注意，默认检查是在可选格式设置和转义之后执行的，即按原样写入输出。

一些示例如 `<cq:text>` 何在JSP中使用标记：

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

### <cq:setContentBundle> {#cq-setcontentbundle}

标 `<cq:setContentBundle>` 签创建i18n本地化上下文并将其存储在配置 `javax.servlet.jsp.jstl.fmt.localizationContext` 变量中。

它具有以下属性：

**语言** -要检索资源包的区域设置语言。

**source** —— 应从中获取区域设置的源。 它可以设置为以下值之一：

* **static** —— 区域设置从属性（如果可用）取 `language` 代，否则从服务器默认区域设置取代。

* **page** —— 区域设置取自当前页面或资源的语言（如果可用），否则取自属性（如果可用），否则取 `language` 自服务器默认区域设置。

* **request** —— 区域设置从请求区域设置( `request.getLocale()`)获取。

* **auto** —— 区域设置从属性（如果可用）取 `language` 代，否则从当前页面或资源的语言（如果可用）取代，否则从请求取代。

如果未 `source` 设置属性：

* 如果设 `language` 置了属性，则属 `source` 性默认为“” `static`。

* 如果未 `language` 设置属性，则属 `source` 性默认为 `auto`。

“内容捆绑”只能由标准JSTL标记使 `<fmt:message>` 用。 按键查找消息的过程分为两种：

1. 首先，搜索当前呈现的基础资源的JCR属性以查找翻译。 这允许您定义一个简单的组件对话框来编辑这些值。
1. 如果节点不包含与键名完全相似的属性，则回退是从sling请求( `SlingHttpServletRequest.getResourceBundle(Locale)`)加载资源包。 此包的语言或区域设置由标签的语言和源属性定 `<cq:setContentBundle>` 义。

标 `<cq:setContentBundle>` 记可以在jsp中如下使用。

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

### <cq:include> {#cq-include}

标记 `<cq:include>` 包含当前页面中的资源。

它具有以下属性：

**冲**

* 一个布尔值，用于定义是否在包括目标之前刷新输出。

**路径**

* 要包含在当前请求处理中的资源对象的路径。 如果此路径是相对的，则会将其附加到其脚本包含给定资源的当前资源的路径中。 必须指定path和resourceType或script。

**resourceType**

* 要包含的资源的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的精确路径：在这种情况下，不支持向路径添加参数、选择器和扩展。
* 如果要包含的资源使用无法解析到资源的路径属性进行指定，则标记可以在路径和此资源类型之外创建合成资源对象。
* 必须指定path和resourceType或script。

**脚本**

* 要包含的jsp脚本。 必须指定path和resourceType或script。

**ignoreComponentHierarchy**

* 一个布尔值，它控制是否应忽略组件层次结构以实现脚本分辨率。 如果为true，则只考虑搜索路径。

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

您应使用或 `<%@ include file="myScript.jsp" %>` 包含 `<cq:include script="myScript.jsp" %>` 脚本吗？

* 该指 `<%@ include file="myScript.jsp" %>` 令通知JSP编译器将一个完整文件包含到当前文件中。 就像所包含文件的内容直接粘贴到原始文件中一样。
* 使用标 `<cq:include script="myScript.jsp">` 签时，文件在运行时包含在内。

您应该使用 `<cq:include>` 还是 `<sling:include>`?

* 在开发AEM组件时，Adobe建议您使用 `<cq:include>`。
* `<cq:include>` 允许您在使用script属性时直接按脚本文件的名称包含脚本文件。 这考虑了组件和资源类型继承，并且通常比使用选择器和扩展严格遵守Sling的脚本分辨率更简单。

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自AEM 5.6起已弃用。 [ 而应 `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 该使用。

标 `<cq:includeClientLib>` 记包括AEM html客户端库，它可以是js、css或主题库。 对于不同类型的多个包含项（例如js和css），此标记需要在jsp中多次使用。 此标签是服务界面周围的便 `com.day.cq.widget.HtmlLibraryManager` 利包装器。

它具有以下属性：

**类别** -以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript和CSS库。 主题名称从请求中提取。

等效于： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**theme** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有主题相关库（CSS和JS）。 主题名称从请求中提取。

等效于：writeThemeInclude `com.day.cq.widget.HtmlLibraryManager#`

**js** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript库。

等效于： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** —— 以逗号分隔的客户端库类别列表。 这将包括给定类别的所有CSS库。

等效于： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主题** -应包含仅指示主题或非主题库的标志。 如果省略，则包括这两个集。 仅适用于纯JS或CSS包含（不适用于类别或主题包含）。

标 `<cq:includeClientLib>` 记可在jsp中使用如下：

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

### <cq:defineObjects> {#cq-defineobjects}

该标 `<cq:defineObjects>` 签公开了以下常用脚本对象，这些对象可由开发人员引用。 它还公开由标签定义的对 [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) 象。

**componentContext**

* 请求的当前组件上下文对象(com.day.cq.wcm.api.components.ComponentContext接口)。

**组件**

* 当前资源的当前AEM组件对象(com.day.cq.wcm.api.components.Component接口)。

**currentDesign**

* 当前页面的当前设计对象(com.day.cq.wcm.api.designer.Design界面)。

**currentPage**

* 当前AEM WCM页面对象(com.day.cq.wcm.api.Page界面)。

**currentStyle**

* 当前单元格的当前样式对象(com.day.cq.wcm.api.designer.Style界面)。

**设计师**

* 用于访问设计信息的设计器对象(com.day.cq.wcm.api.designer.Designer界面)。

**editContext**

* AEM组件的编辑上下文对象(com.day.cq.wcm.api.components.EditContext界面)。

**pageManager**

* 页面级操作的页面管理器对象(com.day.cq.wcm.api.PageManager界面)。

**pageProperties**

* 当前页面的页面属性对象(org.apache.sling.api.resource.ValueMap)。

**属性**

* 当前资源的属性对象(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 资源页面的设计对象(com.day.cq.wcm.api.designer.Design界面)。

**resourcePage**

* 资源页面对象(com.day.cq.wcm.api.Page界面)。
* 它具有以下属性：

**requestName**

* 继承自sling

**responseName**

* 继承自sling

**resourceName**

* 继承自sling

**nodeName**

* 继承自sling

**logName**

* 继承自sling

**resourceResolverName**

* 继承自sling

**slingName**

* 继承自sling

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
>当文 `/libs/foundation/global.jsp` 件包含在脚本中时，标记 `<cq:defineObjects />` 会自动包含在内。

### <cq:requestURL> {#cq-requesturl}

标 `<cq:requestURL>` 记将当前请求URL写入JspWriter。 这两个标 [ 记和 `<cq:addParam>`](#amp-lt-cq-addparam) ，可在此标记的正 [`<cq:removeParam>`](#amp-lt-cq-removeparam) 文中使用，在编写当前请求URL之前修改它。

它允许您创建包含可变参数的指向当前页面的链接。 例如，它允许您转换请求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用或仅 `addParam` 更改给 `removeParam` 定参数的出现，则所有其他参数都不受影响。

`<cq:requestURL>` 没有任何属性。

示例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

标 `<cq:addParam>` 记将具有给定名称和值的请求参数添加到封闭标 [`<cq:requestURL>`](#amp-lt-cq-requesturl) 记中。

它具有以下属性：

**名称**

* 要添加的参数的名称

**value**

* 要添加的参数的值

**示例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

标 `<cq:removeParam>` 签从封闭标签中删除具有给定名称和值的请求 [ 参 `<cq:requestURL>`](#amp-lt-cq-requesturl) 数。 如果未提供值，则删除所有具有给定名称的参数。

它具有以下属性：

**名称**

* 要删除的参数的名称

示例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling标签库 {#sling-tag-library}

Sling标签库包含有帮助的Sling函数。

在脚本中使用Sling标签库时，脚本必须以以下代码开头：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>当该文 `/libs/foundation/global.jsp` 件包含在脚本中时，sling taglib会自动声明。

### <sling:include> {#sling-include}

标记 `<sling:include>` 包含当前页面中的资源。

它具有以下属性：

**冲**

* 一个布尔值，用于定义是否在包括目标之前刷新输出。

**资源**

* 要包含在当前请求处理中的资源对象。 必须指定资源或路径。 如果同时指定了这两个值，则资源优先。

**路径**

* 要包含在当前请求处理中的资源对象的路径。 如果此路径是相对的，则会将其附加到其脚本包含给定资源的当前资源的路径中。 必须指定资源或路径。 如果同时指定了这两个值，则资源优先。

**resourceType**

* 要包含的资源的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的精确路径：在这种情况下，不支持向路径添加参数、选择器和扩展。
* 如果要包含的资源使用无法解析到资源的路径属性进行指定，则标记可以在路径和此资源类型之外创建合成资源对象。

**replaceSelectors**

* 调度时，选择器将替换为此属性的值。

**addSelectors**

* 调度时，此属性的值将添加到选择器中。

**replaceSuffix**

* 调度时，后缀将替换为此属性的值。

>[!NOTE]
>
>标记中包含的资源和脚本的分辨 `<sling:include>` 率与普通sling URL分辨率相同。 默认情况下，选择器、扩展等。 从当前请求开始，也将用于包含的脚本。 可以通过标记属性来修改它们：例如， `replaceSelectors="foo.bar"` 允许您覆盖选择器。

示例:

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

### <sling:defineObjects> {#sling-defineobjects}

标 `<sling:defineObjects>` 签公开以下常用脚本对象，这些对象可由开发人员引用：

**slingRequest**

* SlingHttpServletRequest对象提供对HTTP请求头信息的访问——扩展标准HttpServletRequest —— 并提供对Sling特定内容（如资源、路径信息、选择器等）的访问。

**slingResponse**

* SlingHttpServletResponse对象，提供对服务器创建的HTTP响应的访问。 当前与它扩展的HttpServletResponse相同。**请求**
* 标准JSP请求对象，它是纯HttpServletRequest。**响应**
* 标准JSP响应对象，它是纯HttpServletResponse。

**resourceResolver**

* 当前ResourceResolver对象。 它与slingRequest.getResourceResolver()相同

.**sling**

* 一个SlingScriptHelper对象，包含脚本的简便方法，主要是sling.include(&#39;/some/other/resource&#39;)，用于在此响应中包含其他资源的响应(例如， 嵌入标题html片段)和sling.getService(foo.bar.Service.class)，以检索Sling（类表示法，具体取决于脚本语言）中提供的OSGi服务。

**资源**

* 要处理的当前资源对象，具体取决于请求的URL。 它与slingRequest.getResource()相同。

**currentNode**

* 如果当前资源指向JCR节点（Sling中通常为此情况），则这允许直接访问Node对象。 否则，不定义此对象。

**日志**

* 提供SLF4J记录器，用于从脚本中登录到Sling日志系统，例如 log.info（&quot;执行我的脚本&quot;）。

* 它具有以下属性：

**requestName**

**responseName**

**nodeName**

logName **resourceResolverName**

**slingName**

**示例:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL标签库 {#jstl-tag-library}

[JavaServer Pages标准标签库包含许多有用的标签和标准标签](https://www.oracle.com/technetwork/java/index-jsp-135995.html) 。 核心、格式和函数主题由以下代 `/libs/foundation/global.jsp` 码片断中所示定义。

### /libs/foundation/global.jsp的Extract {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

在如前所述 `/libs/foundation/global.jsp` 导入文件后，您可以使用、和前 `c`缀 `fmt` 访问这 `fn` 些标语。 JSTL的官方文档可在 [Java EE 5教程- javaServer Pages标准标签库中找到](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)。
