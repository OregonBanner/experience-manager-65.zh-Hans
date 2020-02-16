---
title: 编码提示
seo-title: 编码提示
description: AEM编码提示
seo-description: AEM编码提示
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 编码提示{#coding-tips}

## 尽可能使用标语或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含scriptlet使得调试代码中的问题变得困难。 此外，通过在JSP中加入scriptlet，很难将业务逻辑与视图层分离，这违反了单责原则和MVC设计模式。

### 编写可读代码 {#write-readable-code}

代码只编写一次，但读取多次。 在前面花一些时间清理我们编写的代码，会在将来支付红利，因为我们和其他开发者需要稍后阅读它。

### 选择意图显示名称 {#choose-intention-revealing-names}

理想情况下，另一个程序员不必打开一个模块来了解它的功能。 同样，他们应该能够在不阅读方法的情况下判断方法的用途。 我们越能订阅这些想法，就越容易阅读我们的代码，并且编写和更改代码的速度也越快。

在AEM代码库中，使用以下约定：


* 将接口的单个实现命 `<Interface>Impl`名为： `ReaderImpl`.
* 将接口的多个实现命 `<Variant><Interface>`名为，即 `JcrReader` 和 `FileSystemReader`。
* 抽象基类被命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`。
* 将命名包 `com.adobe.product.module`。  每个Maven藏物或OSGi捆绑包都必须有其自己的包。
* Java实现放在API下的实施包中。


请注意，这些约定不一定需要适用于客户实施，但务必定义并遵守约定，这样代码才能保持可维护性。

理想情况下，名字应该能够揭示其意图。 当名称不应该清晰时，常见的代码测试是存在说明变量或方法的用途的注释：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清晰</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//已用时间（以天为单位）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems(){}</p> </td>
   <td><p>public List getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 别再重复一遍 {#don-t-repeat-yourself}

DRY声明不应复制同一组代码。 这也适用于字符串文本等内容。 代码复制为任何需要改变的事情打开了缺陷的大门，需要找出并消除缺陷。

### 避免裸CSS规则 {#avoid-naked-css-rules}

CSS规则应特定于应用程序上下文中的目标元素。 例如，应用于 ** .content .center的CSS规则将过于广泛，并可能最终影响整个系统中的大量内容，要求其他人将来覆盖此样式。 *.myapp-centertext将是一个更具体的规则* ，因为它将在应用程序的上 *下文中指定居中文本* 。

### 消除已弃用API的使用 {#eliminate-usage-of-deprecated-apis}

当API被弃用时，最好找到新推荐的方法而不是依赖已弃用的API。 这将确保将来更顺利的升级。

### 编写可本地化的代码 {#write-localizable-code}

不是由作者提供的任何字符串都应包含在JavaScript中通过 *I18n.get()* (JSP/Java和 ** CQ.I18n.get())调用AEM的i18n词典中。 如果未找到实现，则此实现将返回传递给它的字符串，因此在实现主语言中的功能后，这提供了实现本地化的灵活性。

### 为安全起见而逃生资源路径 {#escape-resource-paths-for-safety}

虽然JCR中的路径不应包含空格，但它们的存在不应导致代码中断。 Jackrabbit提供了一个包含 *escape()和escapePath()方法的Text**实用程序类* 。 对于JSP,Granite UI显示 *granite:encodeURIPath()EL函数* 。

### 使用XSS API和／或HTL防止跨站点脚本攻击 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供了XSS API，可轻松清理参数并确保免受跨站点脚本攻击的安全。 此外，HTL还将这些保护直接内置到模板语言中。 API备忘单可从“开发——准则和最 [佳实践”下载](/help/sites-developing/dev-guidelines-bestpractices.md)。

### 实施适当的日志记录 {#implement-appropriate-logging}

对于Java代码，AEM支持slf4j作为记录消息的标准API，并且应与通过OSGi控制台提供的配置结合使用，以便在管理中保持一致。 Slf4j显示五个不同的日志记录级别。 在选择要在上记录消息的级别时，建议使用以下准则：

* 错误：当代码中的某些内容已损坏，且处理无法继续。 这通常是意外异常的结果。 在这些场景中包含堆栈跟踪通常很有帮助。
* 警告：当某些内容未正常工作，但处理可以继续。 这通常是我们预期的例外的结果，如 *PathNotFoundException*。
* 信息：在监视系统时有用的信息。 请记住，这是默认设置，大多数客户都会将其保留在其环境中。 因此，不要过度使用它。
* 调试：更低级别的处理信息。 在调试具有支持的问题时很有用。
* 跟踪：最低级别信息，如进入／退出方法。 这通常只供开发人员使用。

对于JavaScript, *console.log* only be used in development and all log statements be release.

### 避免货物崇拜编程 {#avoid-cargo-cult-programming}

避免在不了解代码功能的情况下复制代码。 如果存疑，最好询问对模块或API具有更多经验但您并不清楚的人。
