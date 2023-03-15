---
title: 标记库
seo-title: Tag Libraries
description: 通过Granite、CQ和Sling标记库，可访问在模板和组件的JSP脚本中使用的特定函数
seo-description: The Granite, CQ, and Sling tag libraries give you access to specific functions for use in the JSP script of your templates and components
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: de5eb53f6160991ca0718d61afaeed2078a4fa88
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# 标记库{#tag-libraries}

通过Granite、CQ和Sling标记库，可访问在模板和组件的JSP脚本中使用的特定函数。

## Granite标记库 {#granite-tag-library}

Granite标记库包含有用的函数。

在开发Granite UI组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

此外，全球还声明 [Sling库](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

此 `<ui:includeClientLib>` 标记包含AEM html客户端库，可以是js、css或主题库。 对于不同类型的多个包含项（例如js和css），此标记需要在jsp中多次使用。 此标记是一个方便的包装文件，可方便您识别 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 服务接口。

它具有以下属性：

**类别**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript和CSS库。 主题名称是从请求中提取的。

等同于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**主题**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有主题相关库（CSS和JS）。 主题名称是从请求中提取的。

等同于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript库。

等同于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有CSS库。

等同于： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主题**  — 只应包含指示主题库或非主题库的标志。 如果省略，则包含两个集。 仅适用于纯JS或CSS includes（不适用于类别或主题包含）。

此 `<ui:includeClientLib>` 标记可以在jsp中按如下方式使用：

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

要在脚本中使用CQ标记库，脚本必须以下列代码开头：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>当 `/libs/foundation/global.jsp` 文件包含在脚本中，将自动声明taglib。

在开发AEM组件的jsp脚本时，建议在脚本顶部包含以下代码：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它声明sling、CQ和jstl taglibs，并公开由定义的常规使用的脚本对象。 [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) 标记之前。 这会缩短并简化组件的jsp代码。

### &lt;cq:text> {#cq-text}

此 `<cq:text>` 标记是在JSP中输出组件文本的方便标记。

它具有以下可选属性：

**属性**  — 要使用的属性的名称。 该名称相对于当前资源。

**值**  — 用于输出的值。 如果此属性存在，则会覆盖属性属性的使用。

**oldValue**  — 用于差异输出的值。 如果此属性存在，则会覆盖属性属性的使用。

**escapeXml**  — 定义是否应将结果字符串中的&lt;、>、&amp;、&#39;和&quot;字符转换为相应的字符实体代码。 默认值为 false。请注意，转义在可选格式设置之后应用。

**格式**  — 用于设置文本格式的可选java.text.Format。

**noDiff**  — 隐藏差异输出的计算，即使存在差异信息也是如此。

**tagClass**  — 将包围非空输出的元素的CSS类名称。 如果为空，则不会添加任何元素。

**tagName**  — 将包围非空输出的元素的名称。 默认为DIV。

**占位符**  — 在编辑模式下用于空或空文本的默认值，即占位符。 请注意，默认检查在可选格式化和转义之后执行，即按原样写入输出。 默认为：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**默认**  — 用于null或空文本的默认值。 请注意，默认检查在可选格式化和转义之后执行，即按原样写入输出。

以下示例说明 `<cq:text>` 标记可以在JSP中使用：

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

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

此 `<cq:setContentBundle>` 标记会创建i18n本地化上下文并将其存储在 `javax.servlet.jsp.jstl.fmt.localizationContext` 配置变量。

它具有以下属性：

**语言**  — 要检索资源包的区域设置的语言。

**源**  — 应从中获取区域设置的源。 可以将其设置为以下值之一：

* **静态**  — 区域设置取自 `language` 属性（如果可用），否则从服务器默认区域设置。

* **页面**  — 区域设置取自当前页面或资源的语言（如果可用），否则取自 `language` 属性（如果可用），否则从服务器默认区域设置。

* **请求**  — 从请求区域设置( `request.getLocale()`)。

* **自动**  — 区域设置取自 `language` 属性（如果可用），否则从当前页面的语言或资源（如果可用），否则从请求。

如果 `source` 属性未设置：

* 如果 `language` 属性已设置，则 `source` 属性默认为&quot; `static`.

* 如果 `language` 属性未设置， `source` 属性默认为 `auto`.

“内容捆绑包”可以由标准JSTL简单地使用 `<fmt:message>` 标记之间。 按键值查找消息是双重的：

1. 首先，搜索当前渲染的基础资源的JCR属性以获取翻译。 这允许您定义一个简单的组件对话框来编辑这些值。
1. 如果节点不包含与键完全相同的名为的属性，则回退是从sling请求( `SlingHttpServletRequest.getResourceBundle(Locale)`)。 此包的语言或区域设置由 `<cq:setContentBundle>` 标记之前。

此 `<cq:setContentBundle>` 标记可以在jsp中按如下方式使用。

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

此 `<cq:include>` 标记中包含一个资源到当前页面中。

它具有以下属性：

**刷新**

* 一个布尔值，定义是否在包含目标之前刷新输出。

**路径**

* 当前请求处理中包含的资源对象的路径。 如果此路径是相对路径，则会将其附加到当前资源的路径中，该资源的脚本包含给定资源。 必须指定path和resourceType或脚本。

**resourceType**

* 要包含的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的确切路径：在这种情况下，不支持向路径添加参数、选择器和扩展名。
* 如果要包含的资源使用path属性指定，而该属性无法解析为资源，则标记可能会创建路径之外的合成资源对象以及此资源类型。
* 必须指定path和resourceType或脚本。

**脚本**

* 要包含的jsp脚本。 必须指定path和resourceType或脚本。

**ignoreComponentHierarchy**

* 一个布尔值，用于控制是否应忽略组件层次结构以实现脚本解析。 如果为true，则只考虑搜索路径。

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

是否应该使用 `<%@ include file="myScript.jsp" %>` 或 `<cq:include script="myScript.jsp" %>` 是否包含脚本？

* 此 `<%@ include file="myScript.jsp" %>` 指令通知JSP编译器将完整文件包含到当前文件中。 就好像所包含文件的内容被直接粘贴到原始文件中。
* 使用 `<cq:include script="myScript.jsp">` 标签中，文件在运行时包含。

是否应该使用 `<cq:include>` 或 `<sling:include>`？

* 在开发AEM组件时，Adobe建议您使用 `<cq:include>`.
* `<cq:include>` 允许您在使用script属性时直接按名称包含脚本文件。 这考虑到了组件和资源类型继承，并且通常比使用选择器和扩展严格遵守Sling的脚本解析更简单。

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自AEM 5.6之后已被弃用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 应改用。

此 `<cq:includeClientLib>` 标记包含AEM html客户端库，它可以是js、css或主题库。 对于不同类型的多个包含项（例如js和css），此标记需要在jsp中多次使用。 此标记是一个方便的包装文件，可方便您识别 `com.day.cq.widget.HtmlLibraryManager` 服务接口。

它具有以下属性：

**类别**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript和CSS库。 主题名称是从请求中提取的。

等同于： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**主题**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有主题相关库（CSS和JS）。 主题名称是从请求中提取的。

等同于： `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript库。

等同于： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  — 逗号分隔的客户端库类别的列表。 这将包含给定类别的所有CSS库。

等同于： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主题**  — 只应包含指示主题库或非主题库的标志。 如果省略，则包含两个集。 仅适用于纯JS或CSS includes（不适用于类别或主题包含）。

此 `<cq:includeClientLib>` 标记可以在jsp中按如下方式使用：

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

### &lt;cq:defineObjects> {#cq-defineobjects}

此 `<cq:defineObjects>` 标记公开以下定期使用的脚本对象，以供开发人员引用。 它还会公开由定义的对象 [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) 标记之前。

**componentContext**

* 请求的当前组件上下文对象(com.day.cq.wcm.api.components.ComponentContext接口)。

**组件**

* 当前资源的当前AEM组件对象(com.day.cq.wcm.api.components.Component interface)。

**currentdesign**

* 当前页面的当前设计对象(com.day.cq.wcm.api.designer.Design界面)。

**当前页面**

* 当前AEM WCM页面对象(com.day.cq.wcm.api.Page接口)。

**当前样式**

* 当前单元格的当前样式对象(com.day.cq.wcm.api.designer.Style接口)。

**设计者**

* 用于访问设计信息的设计器对象(com.day.cq.wcm.api.designer.Designer界面)。

**editContext**

* AEM组件的编辑上下文对象(com.day.cq.wcm.api.components.EditContext接口)。

**pageManager**

* 用于页面级别操作的页面管理器对象(com.day.cq.wcm.api.PageManager界面)。

**pageProperties**

* 当前页面的页面属性对象(org.apache.sling.api.resource.ValueMap)。

**属性**

* 当前资源的属性对象(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 资源页的设计对象(com.day.cq.wcm.api.designer.Design界面)。

**resourcePage**

* 资源页面对象(com.day.cq.wcm.api.Page接口)。
* 它具有以下属性：

**请求名称**

* 继承自sling

**响应名称**

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

**editContextname**

* 特定于wcm

**propertiesName**

* 特定于wcm

**pageManagerName**

* 特定于wcm

**currentPagename**

* 特定于wcm

**resourcePageName**

* 特定于wcm

**pagePropertiesName**

* 特定于wcm

**组件名称**

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
>当 `/libs/foundation/global.jsp` 文件包含在脚本中， `<cq:defineObjects />` 标记会自动包含在内。

### &lt;cq:requestURL> {#cq-requesturl}

此 `<cq:requestURL>` 标记将当前请求URL写入JspWriter。 两个标记 [ `<cq:addParam>`](#amp-lt-cq-addparam) 和 [ `<cq:removeParam>`](#amp-lt-cq-removeparam) 并可用于此标记正文中，以在写入当前请求URL之前对其进行修改。

它允许您使用各种参数创建指向当前页面的链接。 例如，它使您能够转换请求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用 `addParam` 或 `removeParam` 仅更改给定参数的出现次数，所有其他参数不受影响。

`<cq:requestURL>` 没有任何属性。

示例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

此 `<cq:addParam>` 标记会将具有给定名称和值的请求参数添加到封闭 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 标记之前。

它具有以下属性：

**name**

* 要添加的参数的名称

**选定**

* 要添加参数的值

**示例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

此 `<cq:removeParam>` 标记会从结尾处移除具有给定名称和值的请求参数 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 标记之前。 如果未提供值，则会删除具有给定名称的所有参数。

它具有以下属性：

**name**

* 要删除的参数名称

示例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling标记库 {#sling-tag-library}

Sling标记库包含有用的Sling函数。

在脚本中使用Sling标记库时，脚本必须以下列代码开头：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>当 `/libs/foundation/global.jsp` 文件包含在脚本中，将自动声明sling taglib。

### &lt;sling:include> {#sling-include}

此 `<sling:include>` 标记中包含一个资源到当前页面中。

它具有以下属性：

**刷新**

* 一个布尔值，定义是否在包含目标之前刷新输出。

**resource**

* 要包含在当前请求处理中的资源对象。 必须指定资源或路径。 如果同时指定这两个参数，则优先使用资源。

**路径**

* 当前请求处理中包含的资源对象的路径。 如果此路径是相对路径，则会将其附加到当前资源的路径中，该资源的脚本包含给定资源。 必须指定资源或路径。 如果同时指定这两个参数，则优先使用资源。

**resourceType**

* 要包含的资源的资源类型。 如果设置了资源类型，则路径必须是资源对象的确切路径：在这种情况下，不支持向路径添加参数、选择器和扩展名。
* 如果要包含的资源使用path属性指定，而该属性无法解析为资源，则标记可能会创建路径之外的合成资源对象以及此资源类型。

**replaceSelectors**

* 调度时，选择器将替换为此属性的值。

**addSelectors**

* 调度时，将此属性的值添加到选择器中。

**replaceSuffix**

* 在调度时，后缀将替换为此属性的值。

>[!NOTE]
>
>资源的分辨率和随附的脚本 `<sling:include>` 标记与普通sling URL解析相同。 默认情况下，选择器、扩展名等。 来自当前请求的也用于包含的脚本。 它们可以通过标记属性进行修改：例如 `replaceSelectors="foo.bar"` 允许您覆盖选择器。

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

### &lt;sling:defineObjects> {#sling-defineobjects}

此 `<sling:defineObjects>` 标记公开以下定期使用的脚本对象，以供开发人员引用：

**slingRequest**

* SlingHttpServletRequest对象，提供对HTTP请求标头信息的访问 — 扩展标准HttpServletRequest — 并提供对特定Sling事物（如资源、路径信息、选择器等）的访问。

**slingResponse**

* SlingHttpServletResponse对象，为服务器创建的HTTP响应提供访问权限。 这当前与其扩展的HttpServletResponse相同。**请求**
* 标准JSP请求对象，它是一个纯HttpServletRequest。**响应**
* 标准JSP响应对象，它是一个纯HttpServletResponse。

**resourceResolver**

* 当前ResourceResolver对象。 它与slingRequest.getResourceResolver()相同

。**sling**

* SlingScriptHelper对象，包含脚本的方便方法，主要是sling.include(&#39;/some/other/resource&#39;)，用于在响应中包含其他资源(例如 嵌入标头html代码片段)和sling.getService(foo.bar.Service.class)，以检索Sling中提供的OSGi服务（类表示法，具体取决于脚本语言）。

**resource**

* 要处理的当前资源对象，具体取决于请求的URL。 它与slingRequest.getResource()相同。

**当前节点**

* 如果当前资源指向JCR节点（这通常在Sling中为），则允许直接访问Node对象。 否则，不会定义此对象。

**log**

* 提供一个SLF4J记录器，用于从脚本中记录到Sling日志系统，例如 log.info（“正在执行我的脚本”）。

* 它具有以下属性：

**请求名称**

**响应名称**

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

此 [JavaServer Pages标准标记库](https://www.oracle.com/technetwork/java/index-jsp-135995.html) 包含许多有用的标准标记。 核心、格式和函数taglib由 `/libs/foundation/global.jsp` 如以下代码片段所示。

### /libs/foundation/global.jsp的提取 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

导入后 `/libs/foundation/global.jsp` 文件（如前所述），您可以使用 `c`， `fmt` 和 `fn` 用于访问这些taglib的前缀。 JSTL的官方文档位于 [Java EE 5教程 — JavaServer Pages Standard标记库](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
