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
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---


# 国际化UI字符串{#internationalizing-ui-strings}

Java和Javascript API使您能够在以下类型的资源中将字符串国际化：

* Java源文件。
* JSP脚本。
* 客户端库或页面源中的Javascript。
* 对话框和组件配置属性中使用的JCR节点属性值。

有关国际化和本地化流程的概述，请参阅[国际化组件](/help/sites-developing/i18n.md)。

## 在Java和JSP代码中国际化字符串{#internationalizing-strings-in-java-and-jsp-code}

`com.day.cq.i18n` Java包允许您在UI中显示本地化字符串。 `I18n`类提供从AEM词典检索本地化字符串的`get`方法。 `get`方法的唯一必需参数是英语中的字符串文本。 英语是UI的默认语言。 以下示例本地化单词`Search`:

`i18n.get("Search");`

英语中的字符串标识与通常的国际化框架不同，在国际化框架中，ID标识字符串，并在运行时用于引用该字符串。 使用英文字符串文本具有以下优点：

* 代码易于理解。
* 默认语言中的字符串始终可用。

### 确定用户语言{#determining-the-user-s-language}

有两种方法可确定用户喜欢的语言：

* 对于经过身份验证的用户，从用户帐户的首选项中确定语言。
* 请求的页面的区域设置。

用户帐户的语言属性是首选方法，因为它更可靠。 但是，用户必须登录才能使用此方法。

#### 创建I18n Java对象{#creating-the-i-n-java-object}

I18n类提供两个构造函数。 您如何确定用户的首选语言，从而确定要使用的构造函数。

要以用户帐户中指定的语言显示字符串，请使用以下构造函数（导入`com.day.cq.i18n.I18n)`后）:

```java
I18n i18n = new I18n(slingRequest);
```

构造函数使用`SlingHTTPRequest`检索用户的语言设置。

要使用页面区域设置确定语言，您首先需要获取所请求页面语言的ResourceBundle:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 国际化字符串{#internationalizing-a-string}

使用`I18n`对象的`get`方法来国际化字符串。 `get`方法唯一必需的参数是要国际化的字符串。 该字符串与Translator词典中的字符串相对应。 get方法查找字典中的字符串并返回当前语言的翻译。

`get`方法的第一个参数必须符合以下规则：

* 值必须是字符串文本。 类型`String`的变量不可接受。
* 字符串文本必须在单行上表示。
* 字符串区分大小写。

```xml
i18n.get("Enter a search keyword");
```

#### 使用翻译提示{#using-translation-hints}

指定国际化字符串的[转换提示](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)以区分字典中的重复字符串。 使用`get`方法的第二个可选参数提供转换提示。 翻译提示必须与词典中项的“注释”属性完全匹配。

例如，词典包含字符串`Request`两次：一次是动词，一次是名词。 以下代码将转换提示作为`get`方法中的参数：

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 在局部化句子{#including-variables-in-localized-sentences}中包含变量

在本地化字符串中包含变量，将上下文意义构建到句子中。 例如，登录Web应用程序后，主页将显示消息“欢迎返回管理员”。 收件箱中有2条邮件。” 页面上下文决定用户名和消息数。

[在字典中](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)，变量在字符串中表示为带括号的索引。将变量的值指定为`get`方法的参数。 参数按照转换提示放置，索引与参数的顺序相对应：

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

国际化字符串和翻译提示必须与字典中的字符串和注释完全匹配。 通过提供`null`值作为第二个参数，可以忽略本地化提示。

#### 使用静态获取方法{#using-the-static-get-method}

`I18N`类定义静态`get`方法，当您需要本地化少量字符串时，这种方法非常有用。 除了对象的`get`方法的参数之外，static方法还需要您使用的`SlingHttpRequest`对象或`ResourceBundle`，具体取决于您确定用户首选语言的方式：

* 使用用户的语言首选项：将SlingHttpRequest作为第一个参数。

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 使用页面语言：将ResourceBundle作为第一个参数提供。

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### 在Javascript代码{#internationalizing-strings-in-javascript-code}中国际化字符串

Javascript API使您能够在客户端上本地化字符串。 与[Java和JSP](#internationalizing-strings-in-java-and-jsp-code)代码一样，Javascript API允许您识别要本地化的字符串、提供本地化提示以及在本地化的字符串中包含变量。

`granite.utils` [客户端库文件夹](/help/sites-developing/clientlibs.md)提供Javascript API。 要使用API，请在页面中包含此客户端库文件夹。 本地化函数使用`Granite.I18n`命名空间。

在显示本地化字符串之前，您需要使用`Granite.I18n.setLocale`函数设置区域设置。 该函数需要区域设置的语言代码作为参数：

```
Granite.I18n.setLocale("fr");
```

要显示本地化字符串，请使用`Granite.I18n.get`函数：

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
* 第二个参数是要注入字符串文本的值数组。
* 第三个参数是本地化提示。

以下示例使用Javascript本地化“欢迎返回管理员”。 收件箱中有2条邮件。” 句子：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### 国际化JCR节点的字符串{#internationalizing-strings-from-jcr-nodes}

UI字符串通常基于JCR节点属性。 例如，页面的`jcr:title`属性通常用作页面代码中`h1`元素的内容。 `I18n`类提供用于定位这些字符串的`getVar`方法。

以下示例JSP脚本从存储库中检索`jcr:title`属性，并在页面上显示本地化字符串：

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### 指定JCR节点{#specifying-translation-hints-for-jcr-nodes}的转换提示

与Java API](#using-translation-hints)中的[转换提示相似，您可以提供转换提示以区分字典中的重复字符串。 将翻译提示作为包含国际化属性的节点的属性提供。 提示属性的名称由国际化属性名称的名称组成，并带有`_commentI18n`后缀：

`${prop}_commentI18n`

例如，`cq:page`节点包含正在本地化的jcr:title属性。 提示作为名为jcr:title_commentI18n的属性的值提供。

### 测试国际化覆盖{#testing-internationalization-coverage}

测试您的UI中的所有字符串是否已国际化。 要查看涉及哪些字符串，请将用户语言设置为zz_ZZ并在Web浏览器中打开UI。 国际化字符串以下列格式显示存根转换：

`USR_*Default-String*_尠`

下图显示了AEM主页的存根转换：

![chlimage_1](assets/chlimage_1a.jpeg)

要为用户设置语言，请为用户帐户配置首选项节点的语言属性。

用户的首选项节点具有如下路径：

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

