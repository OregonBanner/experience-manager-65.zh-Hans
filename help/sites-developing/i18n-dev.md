---
title: 国际化UI字符串
seo-title: 国际化UI字符串
description: Java和Javascript API使您能将字符串国际化
seo-description: Java和Javascript API使您能将字符串国际化
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 国际化UI字符串 {#internationalizing-ui-strings}

Java和Javascript API使您能够在以下类型的资源中国际化字符串：

* Java源文件。
* JSP脚本。
* 客户端库或页面源中的Javascript。
* 对话框和组件配置属性中使用的JCR节点属性值。

有关国际化和本地化流程的概述，请参阅国际 [化组件](/help/sites-developing/i18n.md)。

## Java和JSP代码中的字符串国际化 {#internationalizing-strings-in-java-and-jsp-code}

Java `com.day.cq.i18n` 包允许您在UI中显示本地化字符串。 类提 `I18n` 供了从AEM `get` 词典检索本地化字符串的方法。 方法的唯一必需参 `get` 数是英语中的字符串文本。 英语是UI的默认语言。 以下示例将单词本地化 `Search`:

`i18n.get("Search");`

英语中的字符串标识与通常的国际化框架不同，在国际化框架中，ID标识字符串，并在运行时用于引用该字符串。 使用英文字符串文本具有以下优点：

* 代码易于理解。
* 默认语言中的字符串始终可用。

### 确定用户语言 {#determining-the-user-s-language}

有两种方法可确定用户喜欢的语言：

* 对于经过身份验证的用户，从用户帐户的首选项中确定语言。
* 所请求页面的区域设置。

用户帐户的语言属性是首选方法，因为它更可靠。 但是，用户必须登录才能使用此方法。

#### 创建I18n java对象 {#creating-the-i-n-java-object}

I18n类提供两个构造函数。 您如何确定用户的首选语言决定了要使用的构造函数。

要以用户帐户中指定的语言显示字符串，请使用以下构造函数（导入后） `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

构造函数使 `SlingHTTPRequest` 用检索用户的语言设置。

要使用页面区域设置确定语言，您首先需要获取所请求页面语言的ResourceBundle:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 国际化字符串 {#internationalizing-a-string}

使用对 `get` 象的方法 `I18n` 来国际化字符串。 方法唯一必需的参 `get` 数是要国际化的字符串。 该字符串与Translator词典中的字符串相对应。 get方法查找字典中的字符串并返回当前语言的翻译。

方法的第一个参 `get` 数必须符合以下规则：

* 该值必须是字符串文本。 类型的变量 `String` 不可接受。
* 字符串文本必须在单行上表示。
* 该字符串区分大小写。

```xml
i18n.get("Enter a search keyword");
```

#### 使用翻译提示 {#using-translation-hints}

指定国际 [化字符串的翻译提示](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) ，以区分词典中重复的字符串。 使用方法的第二个可选参 `get` 数提供翻译提示。 翻译提示必须与词典中项的“注释”属性完全匹配。

例如，词典包含字符串两 `Request` 次：一次是动词，一次是名词。 以下代码包含翻译提示作为方法中的参数 `get` :

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 在局部化句子中包含变量 {#including-variables-in-localized-sentences}

将变量包含在本地化字符串中，以便在句子中构建上下文含义。 例如，登录Web应用程序后，主页显示消息“欢迎返回管理员”。 收件箱中有2条邮件。” 页面上下文决定用户名和消息数。

[在词典中](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)，变量在字符串中表示为带括号的索引。 将变量的值指定为方法的参 `get` 数。 参数按照转换提示放置，索引与参数的顺序相对应：

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

国际化字符串和翻译提示必须与词典中的字符串和注释完全匹配。 通过提供值作为第二个参数，可 `null` 以忽略本地化提示。

#### 使用静态获取方法 {#using-the-static-get-method}

该 `I18N` 类定义一种静态方 `get` 法，当您需要本地化少量字符串时，该方法非常有用。 除了对象方法的参数之外， `get` 静态方法还需要对象或您使用的 `SlingHttpRequest``ResourceBundle` 对象，具体取决于您确定用户首选语言的方式：

* 使用用户的语言首选项：提供SlingHttpRequest作为第一个参数。

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 使用页面语言：提供ResourceBundle作为第一个参数。

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### 在Javascript代码中国际化字符串 {#internationalizing-strings-in-javascript-code}

Javascript API使您能够在客户端上本地化字符串。 与 [Java和JSP代码一样](#internationalizing-strings-in-java-and-jsp-code) ,Javascript API使您能够识别要本地化的字符串、提供本地化提示以及将变量包含在本地化字符串中。

客 `granite.utils` 户端 [库文件夹提供Javascript API](/help/sites-developing/clientlibs.md) 。 要使用API，请在页面上包含此客户端库文件夹。 本地化函数使用命名 `Granite.I18n` 空间。

在显示本地化字符串之前，您需要使用函数设置区 `Granite.I18n.setLocale` 域设置。 该函数需要区域设置的语言代码作为参数：

```
Granite.I18n.setLocale("fr");
```

要显示本地化字符串，请使用函 `Granite.I18n.get` 数：

```
Granite.I18n.get("string to localize");
```

以下示例国际化字符串“欢迎返回”:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

函数参数与Java I18n不同。get方法：

* 第一个参数是要本地化的字符串文本。
* 第二个参数是要注入到字符串文本中的值的数组。
* 第三个参数是本地化提示。

以下示例使用Javascript本地化“欢迎返回管理员”。 收件箱中有2条邮件。” 句子：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### 从JCR节点国际化字符串 {#internationalizing-strings-from-jcr-nodes}

UI字符串通常基于JCR节点属性。 例如，页面 `jcr:title` 的属性通常用作页面代码中元 `h1` 素的内容。 类提 `I18n` 供了定位这 `getVar` 些字符串的方法。

以下示例JSP脚本从存储库中检 `jcr:title` 索该属性，并在页面上显示本地化的字符串：

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### 为JCR节点指定翻译提示 {#specifying-translation-hints-for-jcr-nodes}

与Java API [中的翻译提示类似](#using-translation-hints)，您可以提供翻译提示以区分词典中的重复字符串。 将翻译提示作为包含国际化属性的节点的属性提供。 提示属性的名称由国际化属性名称的名称组成，后缀为 `_commentI18n` :

`${prop}_commentI18n`

例如，节点 `cq:page` 包含正在本地化的jcr:title属性。 提示作为名为jcr:title_commentI18n的属性的值提供。

### 测试国际化覆盖面 {#testing-internationalization-coverage}

测试您的UI中的所有字符串是否已国际化。 要查看涵盖的字符串，请将用户语言设置为zz_ZZ，然后在Web浏览器中打开UI。 国际化字符串显示为存根转换，格式如下：

`USR_*Default-String*_尠`

下图显示了AEM主页的存根翻译：

![chlimage_1](assets/chlimage_1a.jpeg)

要为用户设置语言，请为用户帐户配置首选项节点的语言属性。

用户的首选项节点具有如下路径：

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

