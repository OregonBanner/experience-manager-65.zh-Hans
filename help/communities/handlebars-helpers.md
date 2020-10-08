---
title: SCF Handlebars Helpers
seo-title: SCF Handlebars Helpers
description: Handlebars帮助器方法便于使用SCF
seo-description: Handlebars帮助器方法便于使用SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义](server-customize.md)** |
|---|---|
|  | **[客户端自定义](client-customize.md)** |

Handlebars Helpers（帮助器）是从Handlebars脚本调用的方法，用于方便与SCF组件一起使用。

该实现包括客户端和服务器端定义。 开发者也可以创建定制帮助器。

与AEM Communities一起交付的定制SCF帮助器在客户 [库中定义](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>请务必安装最 [新的Communities功能包](deploy-communities.md#latestfeaturepack)。

## 缩写 {#abbreviate}

返回符合maxWords和maxLength属性的缩写字符串的帮助程序。

要缩写的字符串作为上下文提供。 如果未提供上下文，则返回空字符串。

首先，将上下文裁切为maxLength，然后将上下文切片为单词并缩小为maxWords。

如果safeString设置为true，则返回的字符串为SafeString。

### 参数 {#parameters}

* **上下文**:字符串

   （可选）默认值是空字符串

* **maxLength**:数字

   （可选）默认值是上下文的长度。

* **maxWords**:数字

   （可选）默认值是修剪字符串中的字数。

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

## 内容加载更多 {#content-loadmore}

一个帮助程序，用于在div下添加两个跨距，一个用于全文，另一个用于较少的文本，能够在两个视图之间切换。

### 参数 {#parameters-1}

* **上下文**:字符串

   （可选）默认值是空字符串。

* **numChars**:数字

   （可选）不显示全文时显示的字符数。 默认值为100。

* **moreText**:字符串

   （可选）要显示的文本，表示要显示的文本更多。 默认为“更多”。

* **椭圆文本**:字符串

   （可选）要显示的文本，指示存在隐藏文本。 默认值为“...”。

* **safeString**:布尔值

   （可选）布尔值，指示是否在返回结果之前应用Handlebars.SafeString()。 默认值为false。

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

返回格式化日期字符串的助手。

### 参数 {#parameters-2}

* **上下文**:数字

   （可选）1970年1月1日（新纪元）以后毫秒值的偏移量。 默认为当前日期。

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

## Equals {#equals}

帮助者根据等式条件返回内容。

### 参数 {#parameters-3}

* **lvalue**:字符串

   要比较的左手值。

* **rvalue**:字符串

   要比较的右边值。

### 示例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

一个块帮助程序，它根据字符串分 [隔的模式列表](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) ，测试WCM模式的当前值。

### 参数 {#parameters-4}

* **上下文**:字符串

   （可选）要翻译的字符串。 如果未提供默认值，则此为必需字段。

* **模式**:字符串

   （可选）要测试的WCM模式 [的逗号分隔列表](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) （如果已设置）。

### 示例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

该助手会覆盖Handlebars助手&#39;i18n&#39;。

另请参 [阅在JavaScript代码中国际化字符串](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)。

### 参数 {#parameters-5}

* **上下文**:字符串

   （可选）要翻译的字符串。 如果未提供默认值，则此为必需字段。

* **默认**:字符串

   （可选）要翻译的默认字符串。 如果未提供上下文，则此为必需字段。

* **注释**:字符串

   （可选）翻译提示

### 示例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Include {#include}

帮助程序，用于将组件作为非现有资源包含在模板中。

这允许以编程方式对资源进行自定义，比作为JCR节点添加的资源更容易。 请参 [阅添加或包括社区组件](scf.md#add-or-include-a-communities-component)。

只包含少数几个社区组件。 对于AEM 6.1，可包含的是评 [论](essentials-comments.md)、 [评级](rating-basics.md)[、](reviews-basics.md)评 [论](essentials-voting.md)和投票。

此帮助程序仅适用于服务器端，它提供与JSP脚本 [的cq:include](../../help/sites-developing/taglib.md) 类似的功能。

### 参数 {#parameters-6}

* **上下文**:字符串或对象

   （可选，除非提供相对路径）

   使 `this` 用传递当前上下文。

   使用 `this.id` 在获取资源，以 `id` 呈现请求的resourceType。

* **resourceType**:字符串

   （可选）资源类型将默认为上下文中的资源类型。

* **模板**:字符串

   组件脚本的路径。

* **路径**:字符串

   （必需）资源的路径。 如果路径是相对的，则必须提供上下文，否则返回空字符串。

* **authoringDisabled**:布尔值

   （可选）默认值为false。 仅供内部使用。

### 示例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

这将包括位于+ /comments的新 `this.id` 注释组件。

## IncludeClientLib {#includeclientlib}

包含AEM html客户端库的帮助程序，它可以是js、css或主题库。 对于多个不同类型的包含项，例如js和css，此标记需要在Handlebars脚本中多次使用。

此帮助程序仅在服务器端适用，它提供与JSP脚本 [ui:includeClientLib](../../help/sites-developing/taglib.md) 类似的功能。

### 参数 {#parameters-7}

* **类别**:字符串

   （可选）以逗号分隔的列表客户端库类别。 这将包括给定类别的所有Javascript和CSS库。 主题名称会从请求中提取。

* **主题**:字符串

   （可选）以逗号分隔的列表客户端库类别。 这将包括给定类别的所有与主题相关的库（CSS和JS）。 主题名称会从请求中提取。

* **js**:字符串

   （可选）以逗号分隔的列表客户端库类别。 这将包括给定类别的所有Javascript库。

* **css**:字符串

   （可选）以逗号分隔的列表客户端库类别。 这将包括给定类别的所有CSS库。

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

一个帮助程序，用于显示已经过多少时间到截止点，之后显示常规日期格式。

例如：

* 12小时前
* 7天前

### 参数 {#parameters-8}

* **上下文**:数字

   过去与“现在”比较的时间。 时间表示为从1970年1月1日（纪元）起抵消的毫秒值。

* **daysCustofm**:数字

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

帮助程序，它对HTML元素内容的源字符串进行编码，以帮助防止XSS。

注意：它不是validator，不用于写入属性值。

### 参数 {#parameters-9}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

一种帮助程序，它对源字符串进行编码以写入HTML属性值，以帮助防止XSS。

注意：它不是validator，不用于编写actionalable属性(href、src、事件处理函数)。

### 参数 {#parameters-10}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

一种帮助程序，它对源字符串进行编码以写入JavaScript字符串内容，以帮助防止XSS。

注意：它不是validator，不用于写入任意JavaScript。

### 参数 {#parameters-11}

* **上下文**:对象

   要编码的HTML。

### 示例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

帮助程序，它清理URL以编写为HTML href或srce属性值以帮助防止XSS。

注意：这可能返回空字符串

### 参数 {#parameters-12}

* **上下文**:对象

   要清理的URL。

### 示例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述 {#handlebars-js-basic-overview}

从Handlebars.js文档快速概 [述帮助程序功能](https://handlebarsjs.com/expressions.html):

* Handlebars帮助程序调用是一个简单的标识符 *(帮助* 程序的名称)，后跟零个或多个以空格分隔的参数。
* 参数可以是简单的字符串、数字、布尔或JSON对象，也可以是键值对（散列参数）的可选序列作为最后一个参数。
* 哈希参数中的键必须是简单标识符。
* 哈希参数中的值是Handlebars表达式:简单标识符、路径或字符串。
* Handlebars帮助者 `this`始终可以找到当前的情境。
* 上下文可以是字符串、数字、布尔值或JSON数据对象。
* 可以将嵌套在当前上下文中的对象作为上下文进行传递， `this.url` 如 `this.id` 或（请参阅以下简单和块帮助器示例）。

* 块帮助程序是可以从模板中的任何位置调用的功能。 他们每次都可以调用模板块零次或多次，并具有不同的上下文。 它们包含{{#*name*}}和{{/name}*之*&#x200B;间的上下文。

* Handlebars为名为“options”的助手提供最终参数。 特殊对象“选项”包括

   * 可选专用数据(options.data)
   * 调用的可选键值属性(options.hash)
   * 能够调用自身(options.fn())
   * 能够调用其本身的反向(options.inverse())

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

&lt;ul>&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>发布！&lt;/a>&lt;/li>&lt;/ul>

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

将呈现：&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## 自定义SCF Helpers {#custom-scf-helpers}

必须在服务器端和客户端上实现自定义帮助器，特别是在传递数据时。 对于SCF，当服务器在请求页面时为给定组件生成HTML时，大多数模板都在服务器端编译和呈现。

### 服务器端自定义帮助器 {#server-side-custom-helpers}

要在服务器端实现和注册自定义SCF帮助程序，只需实现Java接 [口TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，将它设为 [OSGi服务](../../help/sites-developing/the-basics.md#osgi) ，并将它作为OSGi捆绑的一部分进行安装。

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
>在登录用户的客户端上重新呈现该组件，如果找不到客户端帮助程序，该组件将消失。

### 客户端自定义帮助器 {#client-side-custom-helpers}

客户端帮助程序是通过调用注册的Handlebars脚本 `Handlebars.registerHelper()`。
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

必须将自定义客户端帮助器添加到自定义客户端库。
clientlib必须：

* 包含依赖项 `cq.social.scf`。
* 加载Handlebars后加载。
* 包 [括](clientlibs.md)。

注意：SCF帮助器的定义请见 `/etc/clientlibs/social/commons/scf/helpers.js`。

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义](server-customize.md)** |
|---|---|
|  | **[客户端自定义](client-customize.md)** |

