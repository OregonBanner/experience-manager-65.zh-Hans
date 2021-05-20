---
title: SCF Handlebars Helpers
seo-title: SCF Handlebars Helpers
description: Handlebars Helper方法便于与SCF配合使用
seo-description: Handlebars Helper方法便于与SCF配合使用
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---

# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[⇐功能要点](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[客户端自定义⇒](client-customize.md)** |

Handlebars Helpers（帮助程序）是从Handlebars脚本中调用的方法，以便于与SCF组件一起使用。

该实施包括客户端和服务器端定义。 开发人员也可以创建自定义帮助程序。

随AEM Communities提供的自定义SCF帮助器在[客户端库](../../help/sites-developing/clientlibs.md)中定义：

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>请务必安装[最新的Communities功能包](deploy-communities.md#latestfeaturepack)。

## 缩写 {#abbreviate}

一个帮助程序，用于返回符合maxWords和maxLength属性的缩写字符串。

要缩写的字符串将作为上下文提供。 如果未提供上下文，则返回空字符串。

首先，将上下文裁切为maxLength ，然后将上下文切成单词并缩小为maxWords。

如果safeString设置为true，则返回的字符串为SafeString。

### 参数 {#parameters}

* **上下文**:字符串

   （可选）默认为空字符串

* **maxLength**:数值

   （可选）默认值为上下文的长度。

* **maxWords**:数值

   （可选）默认为裁切字符串中的词数。

* **safeString**:布尔值

   （可选）如果为true，则返回Handlebars.SafeString()。 默认值为false。

### 示例 {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

帮助程序在div下添加两个跨区，一个用于全文，另一个用于较少的文本，并能够在两个视图之间切换。

### 参数 {#parameters-1}

* **上下文**:字符串

   （可选）默认为空字符串。

* **numChars**:数值

   （可选）不显示全文时要显示的字符数。 默认值为100。

* **更多文本**:字符串

   （可选）要显示的文本，指示要显示的文本更多。 默认值为“更多”。

* **省略号文本**:字符串

   （可选）要显示的用于指示存在隐藏文本的文本。 默认值为“……”。

* **safeString**:布尔值

   （可选）布尔值，指示在返回结果之前是否应用Handlebars.SafeString()。 默认值为false。

### 示例 {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

一个帮助程序，用于返回格式化的日期字符串。

### 参数 {#parameters-2}

* **上下文**:数值

   （可选）1970年1月1日（新纪元）起的毫秒值偏移。 默认为当前日期。

* **格式**:字符串

   （可选）要应用的日期格式。 默认值为“YYYY-MM-DDTHH:mm:ss.sssZ”，结果显示为“2015-03-18T18:17:13-07:00”

### 示例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 等于 {#equals}

根据条件相等返回内容的助手。

### 参数 {#parameters-3}

* **值**:字符串

   要比较的左侧值。

* **rvalue**:字符串

   要比较的右侧值。

### 示例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

一个块帮助程序，用于根据字符串分隔的模式列表测试[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)的当前值。

### 参数 {#parameters-4}

* **上下文**:字符串

   （可选）要翻译的字符串。 如果未提供默认设置，则此为必需字段。

* **模式**:字符串

   （可选）要测试是否已设置的[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)列表（以逗号分隔）。

### 示例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

这个助手会覆盖Handlebars助手i18n。

另请参阅[在JavaScript代码中国际化字符串](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)。

### 参数 {#parameters-5}

* **上下文**:字符串

   （可选）要翻译的字符串。 如果未提供默认设置，则此为必需字段。

* **默认**:字符串

   （可选）要翻译的默认字符串。 如果未提供上下文，则此为必需字段。

* **注释**:字符串

   （可选）翻译提示

### 示例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包括 {#include}

用于在模板中将组件作为非现有资源包含在内的帮助程序。

这允许以编程方式自定义资源，而对于添加为JCR节点的资源而言，这种自定义方式比可能的更简单。 请参阅[添加或包含社区组件](scf.md#add-or-include-a-communities-component)。

只能包含一些选定的社区组件。 对于AEM 6.1，可包含的是[comments](essentials-comments.md)、[rating](rating-basics.md)、[reviews](reviews-basics.md)和[voting](essentials-voting.md)。

此帮助程序仅适用于服务器端，它提供的功能与JSP脚本的[cq:include](../../help/sites-developing/taglib.md)类似。

### 参数 {#parameters-6}

* **上下文**:字符串或对象

   （可选，除非提供相对路径）

   使用`this`传递当前上下文。

   使用`this.id`在`id`处获取资源，以渲染请求的resourceType。

* **resourceType**:字符串

   （可选）资源类型将默认为来自上下文的资源类型。

* **模板**:字符串

   组件脚本的路径。

* **路径**:字符串

   （必需）资源的路径。 如果路径为相对路径，则必须提供上下文，否则返回空字符串。

* **authoringDisabled**:布尔值

   （可选）默认值为false。 仅供内部使用。

### 示例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

这将在`this.id` + /comments中包含一个新的注释组件。

## IncludeClientLib {#includeclientlib}

一个帮助程序，其中包含AEM html客户端库，该库可以是js、css或主题库。 对于不同类型（例如js和css）的多个包含项，此标记需要在Handlebars脚本中多次使用。

此帮助程序仅适用于服务器端，它提供的功能与JSP脚本的[ui:includeClientLib](../../help/sites-developing/taglib.md)类似。

### 参数 {#parameters-7}

* **类别**:字符串

   （可选）以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript和CSS库。 主题名称将从请求中提取。

* **主题**:字符串

   （可选）以逗号分隔的客户端库类别列表。 这将包括给定类别的所有与主题相关的库（CSS和JS）。 主题名称将从请求中提取。

* **js**:字符串

   （可选）以逗号分隔的客户端库类别列表。 这将包括给定类别的所有Javascript库。

* **css**:字符串

   （可选）以逗号分隔的客户端库类别列表。 这将包含给定类别的所有CSS库。

### 示例 {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Pretty-time {#pretty-time}

一个帮助程序，用于显示已经过去了多少时间到截止点，在此之后将显示常规日期格式。

例如：

* 12小时前
* 7天前

### 参数 {#parameters-8}

* **上下文**:数值

   过去与“现在”相比较的时间。 时间以毫秒值表示，该值从1970年1月1日（新纪元）开始偏移。

* **daysCutfom**:数值

   切换到实际日期前的天数。 默认值为60。

### 示例 {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

帮助程序，可对HTML元素内容的源字符串进行编码，以帮助防御XSS。

注意：它不是验证器，不用于写入属性值。

### 参数 {#parameters-9}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

一种帮助程序，可对源字符串进行编码，以写入HTML属性值，以帮助防止XSS。

注意：这不是验证器，也不用于编写可操作属性（href、src、事件处理程序）。

### 参数 {#parameters-10}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

一种帮助程序，可对源字符串进行编码以写入JavaScript字符串内容，以帮助防御XSS。

注意：这不是验证器，不用于写入任意JavaScript。

### 参数 {#parameters-11}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

一个帮助程序，用于清理URL以作为HTML href或服务属性值写入，以帮助防止XSS。

注意：这可能会返回空字符串

### 参数 {#parameters-12}

* **上下文**:对象

   要整理的URL。

### 示例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述{#handlebars-js-basic-overview}

[Handlebars.js文档](https://handlebarsjs.com/expressions.html)中的帮助程序函数快速概述：

* Handlebars帮助程序调用是一个简单的标识符（帮助程序的&#x200B;*name*），其后跟零个或多个以空格分隔的参数。
* 参数可以是简单的字符串、数字、布尔值或JSON对象，以及作为最后一个参数的可选键值对（哈希参数）序列。
* 哈希参数中的键必须是简单的标识符。
* 哈希参数中的值是Handlebars表达式：简单标识符、路径或字符串。
* 当前上下文`this`始终可供Handlebars帮助者使用。
* 上下文可以是字符串、数字、布尔值或JSON数据对象。
* 可以将嵌套在当前上下文中的对象作为上下文进行传递，例如`this.url`或`this.id`（请参阅以下简单和块帮助器示例）。

* 块帮助程序是可从模板中的任意位置调用的函数。 他们每次都可以使用不同的上下文零次或多次调用模板块。 它们包含{{#*name*}}和{{/*name*}}之间的上下文。

* Handlebars为名为“options”的帮助程序提供了最终参数。 特殊对象“options”包括

   * 可选专用数据(options.data)
   * 调用中的可选键值属性(options.hash)
   * 能够调用自身(options.fn())
   * 能够调用自身的反向(options.inverse())

* 建议从帮助程序返回的HTML字符串内容是SafeString。

### Handlebars.js文档中的简单助手的示例：{#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

将呈现：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>发帖！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js文档中的块帮助程序示例：{#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

将呈现：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>耶胡达&lt;/a>&lt;/li>
&lt;/ul>

## 自定义SCF帮助程序{#custom-scf-helpers}

必须在服务器端和客户端上实施自定义帮助程序，尤其是在传递数据时。 对于SCF，大多数模板都在服务器端编译和渲染，因为服务器在请求页面时会为给定组件生成HTML。

### 服务器端自定义帮助程序{#server-side-custom-helpers}

要在服务器端实施和注册自定义SCF帮助程序，只需实施Java接口[TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，将其设为[OSGi服务](../../help/sites-developing/the-basics.md#osgi)，并将其作为OSGi包的一部分进行安装即可。

例如：

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>还必须为客户端创建为服务器端创建的帮助程序。
>
>组件将在已登录用户的客户端重新呈现，如果未找到客户端帮助程序，则组件会消失。

### 客户端自定义帮助程序{#client-side-custom-helpers}

客户端帮助程序是通过调用`Handlebars.registerHelper()`注册的Handlebars脚本。
例如：

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

必须将自定义客户端帮助程序添加到自定义客户端库。
clientlib必须：

* 包括对`cq.social.scf`的依赖项。
* 加载Handlebars后加载。
* 包含[](clientlibs.md)。

注意：在`/etc/clientlibs/social/commons/scf/helpers.js`中定义了SCF帮助器。

| **[⇐功能要点](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[客户端自定义⇒](client-customize.md)** |
