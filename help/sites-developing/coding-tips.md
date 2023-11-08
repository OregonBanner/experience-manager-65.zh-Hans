---
title: 编码提示
description: 了解在Adobe Experience Manager中编码最佳实践的一些提示。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 编码提示{#coding-tips}

## 尽可能使用taglibs或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含scriptlet会导致难以调试代码中的问题。 此外，通过在JSP中包含scriptlet，很难将业务逻辑与视图层分离，这违反了单责任原则和MVC设计模式。

### 可写可读代码 {#write-readable-code}

代码只写入一次，但读取多次。 花一些时间提前清理编写的代码，会在您和其他开发人员稍后阅读代码时产生回报。

### 选择表明意向的名称 {#choose-intention-revealing-names}

理想情况下，其他程序员不必打开模块即可了解其功能。 类似地，他们应该能够在不阅读方法的情况下判断方法的用途。 您能更好地订阅这些想法，越容易阅读代码，您就能越快地编写和更改代码。

在AEM代码库中，使用以下约定：


* 接口的单个实现名为 `<Interface>Impl`，即， `ReaderImpl`.
* 接口的多个实现已命名 `<Variant><Interface>`，即， `JcrReader` 和 `FileSystemReader`.
* 抽象基类被命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`.
* 包已命名 `com.adobe.product.module`. 每个Maven工件或OSGi捆绑包必须具有自己的包。
* Java™实施位于其API下的实施包中。


这些约定不一定适用于客户实施，但定义约定并遵守这些约定很重要，这样代码才能持续可维护。

理想情况下，名字应该表明他们的意图。 当名称不够清晰时，常见的代码测试是存在解释变量或方法的用途的注释：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清楚</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d； //用时天数</p> </td>
   <td><p>int elapsedTimeInDays；</p> </td>
  </tr>
  <tr>
   <td><p>//获取带标记的图像<br /> 公共列表getItems() {}</p> </td>
   <td><p>公共列表getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重复您自己  {#don-t-repeat-yourself}

DRY表示绝不应复制同一组代码。 这也适用于字符串文本等。 代码复制为某些必须更改的内容打开了缺陷之门，应寻找并消除这些缺陷。

### 避免使用裸露的CSS规则 {#avoid-naked-css-rules}

CSS规则应该特定于应用程序上下文中的目标元素。 例如，应用于 *.content .center* 过于宽泛，最终可能会影响您系统中的大量内容，要求其他人将来覆盖此样式。 而， *.myapp-centertext* 将是一个更具体的规则，因为它指定居中 *文本* 在应用程序的上下文中。

### 消除使用已弃用的API {#eliminate-usage-of-deprecated-apis}

弃用API后，最好查找新的推荐方法，而不是依赖已弃用的API。 这将确保未来能够更平稳地升级。

### 编写可本地化的代码 {#write-localizable-code}

任何不是由作者提供的字符串都应封装在对AEM i18n词典的调用中，该词典可通过 *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 在JavaScript中。 如果找不到任何实施，此实施将返回传递给它的字符串，因此在使用主要语言实施功能后，这提供了实施本地化的灵活性。

### 为安全而转义资源路径 {#escape-resource-paths-for-safety}

虽然JCR中的路径不应包含空格，但它们的存在不应导致代码中断。 Jackrabbit提供了一个文本实用程序类，其中 *escape()* 和 *escapePath()* 方法。 对于JSP，Granite UI公开 *granite：encodeURIPath() EL* 函数。

### 使用XSS API和/或HTL防止跨站点脚本攻击 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供了一个XSS API，用于轻松清除参数并确保免受跨站点脚本攻击的安全。 此外，HTL将这些保护直接内置到模板语言中。 API备忘表可从以下位置下载： [开发 — 准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md).

### 实施适当的日志记录 {#implement-appropriate-logging}

对于Java™代码，AEM支持slf4j作为用于记录消息的标准API，并且应该与通过OSGi控制台提供的配置一起使用，以确保管理的一致性。 Slf4j公开五个不同的日志记录级别。 Adobe建议在选择要在哪个级别记录消息时遵循以下准则：

* 错误：当代码中的某些内容损坏时，处理无法继续。 这通常因意外异常而发生。 在这些场景中包含栈栈跟踪很有帮助。
* 警告：当某些内容未正确工作时，可以继续处理。 这通常是我们所期望的例外情况的结果，例如 *PathNotFoundException*.
* 信息：监视系统时有用的信息。 请记住，这是默认设置，大多数客户会将其保留在其环境中。 因此，请勿过度使用它。
* DEBUG：有关处理的较低级别信息。 在使用支持功能调试问题时，此变量将非常有用。
* TRACE：最低级别的信息，如输入/退出方法。 这通常仅供开发人员使用。

如果存在JavaScript， *console.log* 应仅在开发期间使用，并且应在发布之前删除所有日志语句。

### 避免狂热的编程 {#avoid-cargo-cult-programming}

避免在不了解代码用途的情况下复制代码。 如有疑问，请始终询问对您不了解的模块或API拥有更多经验的人员。
