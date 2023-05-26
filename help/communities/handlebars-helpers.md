---
title: SCF Handlebars助手
seo-title: SCF Handlebars Helpers
description: 便于使用SCF的Handlebars帮助程序方法
seo-description: Handlebars Helper methods to facilitate work with SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# SCF Handlebars助手 {#scf-handlebars-helpers}

| **[⇐ Feature Essentials](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[客户端自定义⇒](client-customize.md)** |

Handlebars帮助程序（帮助程序）是可从Handlebars脚本中调用的方法，以便使用SCF组件。

该实施包括客户端和服务器端定义。 开发人员还可以创建自定义帮助程序。

与AEM Communities一起提供的自定义SCF帮助程序在 [客户端库](../../help/sites-developing/clientlibs.md)：

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>请务必安装 [最新的Communities功能包](deploy-communities.md#latestfeaturepack).

## 缩写 {#abbreviate}

用于返回符合maxWords和maxLength属性的缩写字符串的帮助程序。

要缩写的字符串作为上下文提供。 如果未提供上下文，则返回空字符串。

首先，将上下文裁剪为maxLength，然后将上下文分割为单词，并缩减为maxWords。

如果safeString设置为true，则返回的字符串是SafeString。

### 参数 {#parameters}

* **上下文**：字符串

   （可选）默认值为空字符串

* **maxLength**：数字

   （可选）默认值是上下文的长度。

* **maxWords**：数字

   （可选）默认值为修剪字符串中的字数。

* **安全字符串**：布尔值

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

帮助程序可以在div下添加两个跨区，一个用于全文，另一个用于较少文本，并且能够在两个视图之间切换。

### 参数 {#parameters-1}

* **上下文**：字符串

   （可选）默认值为空字符串。

* **numChars**：数字

   （可选）不显示全文时显示的字符数。 默认值为100。

* **更多文本**：字符串

   （可选）要显示的文本，指示要显示的文本更多。 默认值为“更多”。

* **省略号文本**：字符串

   （可选）要显示的文本，指示存在隐藏文本。 默认值为“……”。

* **安全字符串**：布尔值

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

## 日期实用程序 {#dateutil}

用于返回带格式的日期字符串的帮助程序。

### 参数 {#parameters-2}

* **上下文**：数字

   （可选）从1970年1月1日起偏移的毫秒值（纪元）。 默认值为当前日期。

* **格式**：字符串

   （可选）要应用的日期格式。 默认值为“YYYY-MM-DDTHH”:mm:ss.sssZ”，结果将显示为“2015-03-18T18”:17:13-07:00英寸

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

根据相等条件返回内容的帮助程序。

### 参数 {#parameters-3}

* **值**：字符串

   要比较的左侧值。

* **rvalue**：字符串

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

一个块帮助程序，用于测试当前值 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 以字符串分隔的模式列表。

### 参数 {#parameters-4}

* **上下文**：字符串

   （可选）要翻译的字符串。 如果未提供默认值，则此为必填字段。

* **模式**：字符串

   （可选）逗号分隔的列表 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 以测试是否设置。

### 示例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

此辅助函数覆盖Handlebars辅助函数“i18n”。

另请参阅 [在JavaScript代码中国际化字符串](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### 参数 {#parameters-5}

* **上下文**：字符串

   （可选）要翻译的字符串。 如果未提供默认值，则此为必填字段。

* **默认**：字符串

   （可选）要翻译的默认字符串。 如果未提供上下文，则此为必填字段。

* **注释**：字符串

   （可选）翻译提示

### 示例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包括 {#include}

用于将组件作为非现有资源包含在模板中的辅助函数。

与添加为JCR节点的资源相比，这允许以编程方式更轻松地自定义资源。 参见 [添加或包含社区组件](scf.md#add-or-include-a-communities-component).

只能包括少量Communities组件。 对于AEM 6.1，可包含的内容包括 [评论](essentials-comments.md)， [评级](rating-basics.md)， [审核](reviews-basics.md)、和 [投票](essentials-voting.md).

此帮助程序仅适用于服务器端，它提供的功能与 [cq：include](../../help/sites-developing/taglib.md) 用于JSP脚本。

### 参数 {#parameters-6}

* **上下文**：字符串或对象

   （可选，除非提供相对路径）

   使用 `this` 以传递当前上下文。

   使用 `this.id` 获取资源： `id` 用于呈现所请求的resourceType。

* **resourceType**：字符串

   （可选）资源类型默认为上下文中的资源类型。

* **模板**：字符串

   组件脚本的路径。

* **路径**：字符串

   （必需）资源的路径。 如果路径是相对路径，则必须提供上下文，否则返回空字符串。

* **authoringDisabled**：布尔值

   （可选）默认值为false。 仅供内部使用。

### 示例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

这将在以下位置包括新的注释组件： `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

包含AEM html客户端库的帮助程序，该客户端库可以是js、css或主题库。 对于不同类型的多个包含项（例如js和css），需要在Handlebars脚本中多次使用此标记。

此帮助程序仅适用于服务器端，它提供的功能与 [ui：includeClientLib](../../help/sites-developing/taglib.md) 用于JSP脚本。

### 参数 {#parameters-7}

* **类别**：字符串

   （可选）以逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript和CSS库。 主题名称是从请求中提取的。

* **主题**：字符串

   （可选）以逗号分隔的客户端库类别的列表。 这将包含给定类别的所有主题相关库（CSS和JS）。 主题名称是从请求中提取的。

* **js**：字符串

   （可选）以逗号分隔的客户端库类别的列表。 这将包含给定类别的所有Javascript库。

* **css**：字符串

   （可选）以逗号分隔的客户端库类别的列表。 这将包含给定类别的所有CSS库。

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

## 美妙时光 {#pretty-time}

一个帮助程序，用于显示到达截止点之前经过的时间，超过该时间会显示常规日期格式。

例如：

* 12小时前
* 7天前

### 参数 {#parameters-8}

* **上下文**：数字

   要与“现在”进行比较的过去时间。 时间表示为从1970年1月1日起偏移的毫秒值（纪元）。

* **daysCutoff**：数字

   切换到实际日期之前的天数。 默认值为60。

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

一个帮助程序，用于为HTML元素内容编码源字符串，以帮助防范XSS。

注意：这不是验证器，不用于写入属性值。

### 参数 {#parameters-9}

* **上下文**：对象

   要编码的HTML。

### 示例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

帮助程序对源字符串进行编码，以便写入HTML属性值，帮助防范XSS。

注意：这不是验证器，不用于编写可操作属性（href、src、事件处理程序）。

### 参数 {#parameters-10}

* **上下文**：对象

   要编码的HTML。

### 示例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

一个帮助程序，对用于写入JavaScript字符串内容的源字符串进行编码，以帮助防范XSS。

注意：这不是验证器，不用于写入任意JavaScript。

### 参数 {#parameters-11}

* **上下文**：对象

   要编码的HTML。

### 示例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

一个帮助程序，用于对作为HTMLhref或srce属性值写入的URL进行清理以帮助防范XSS。

注意：这可能返回空字符串

### 参数 {#parameters-12}

* **上下文**：对象

   要清理的URL。

### 示例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述 {#handlebars-js-basic-overview}

* Handlebars帮助程序调用是一个简单标识符(即 *name* )，后面跟零个或多个空格分隔参数。
* 参数可以是简单字符串、数字、布尔值或JSON对象，也可以是键值对（哈希参数）的可选序列作为最后一个参数。
* 哈希参数中的键必须是简单标识符。
* 散列参数中的值是Handlebars表达式：简单标识符、路径或字符串。
* 当前上下文， `this`，始终可供Handlebars帮助程序使用。
* 上下文可以是字符串、数字、布尔值或JSON数据对象。
* 可以将嵌套在当前上下文中的对象作为上下文传递，例如 `this.url` 或 `this.id` （请参阅以下简单帮助程序和块帮助程序的示例）。

* 块帮助程序是从模板中的任何位置调用的函数。 它们每次可使用不同的上下文调用模板块零次或多次。 它们包含以下内容之间的上下文： {{#*name*}} and {{/*name*}}.

* Handlebars为帮助程序提供了一个名为“options”的最终参数。 特殊对象“options”包括

   * 可选专用数据(options.data)
   * 调用中的可选键值属性(options.hash)
   * 能够调用自身(options.fn())
   * 能够调用自身的逆函数(options.inverse())

* 建议从帮助程序返回的HTML字符串内容是SafeString。

### Handlebars.js文档中的简单帮助程序示例： {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

### Handlebars.js文档中的块帮助程序示例： {#an-example-of-a-block-helper-from-handlebars-js-documentation}

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
&lt;li>&lt;a href=&quot;/people/1&quot;>艾伦&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>耶胡达语&lt;/a>&lt;/li>
&lt;/ul>

## 自定义SCF助手 {#custom-scf-helpers}

必须在服务器端和客户端实施自定义帮助程序，尤其是在传递数据时。 对于SCF，大多数模板在服务器端编译和渲染，因为服务器在请求页面时为给定组件生成HTML。

### 服务器端自定义帮助程序 {#server-side-custom-helpers}

要在服务器端实施和注册自定义SCF帮助程序，只需实施Java接口 [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，使其成为 [OSGi服务](../../help/sites-developing/the-basics.md#osgi) 并将其作为OSGi捆绑包的一部分安装。

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
>组件将在登录用户的客户端上重新渲染，如果找不到客户端帮助程序，组件将消失。

### 客户端自定义帮助程序 {#client-side-custom-helpers}

客户端帮助程序是通过调用注册的Handlebars脚本 `Handlebars.registerHelper()`.
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

必须将自定义客户端帮助程序添加到自定义客户端库中。
clientlib必须：

* 包含依赖项 `cq.social.scf`.
* 加载Handlebars后加载。
* 是 [已包括](clientlibs.md).

注意：SCF帮助程序定义于 `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Feature Essentials](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[客户端自定义⇒](client-customize.md)** |
