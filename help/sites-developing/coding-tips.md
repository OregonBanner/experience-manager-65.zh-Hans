---
title: 编码提示
seo-title: Coding Tips
description: AEM的编码提示
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 编码提示{#coding-tips}

## 尽可能使用taglibs或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含Scriptlet会导致难以调试代码中的问题。 此外，通过在JSP中包含脚本程序，很难将业务逻辑与视图层分离，这违反了单责任原则和MVC设计模式。

### 可写可读代码 {#write-readable-code}

代码只写入一次，但读取多次。 花一些时间来清理我们编写的代码将带来回报，因为我们和其他开发人员以后需要阅读它。

### 选择意图揭示型姓名 {#choose-intention-revealing-names}

理想情况下，另一个程序员不必打开模块就能了解它的功能。 类似地，他们应该能够在不阅读方法的情况下判断方法的用途。 我们订阅这些想法得越好，代码读取越容易，编写和更改代码的速度就越快。

在AEM代码库中，使用以下约定：


* 接口的单个实现名为 `<Interface>Impl`，即 `ReaderImpl`.
* 接口的多个实现已命名 `<Variant><Interface>`，即 `JcrReader` 和 `FileSystemReader`.
* 抽象基类被命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`.
* 包已命名 `com.adobe.product.module`.  每个Maven工件或OSGi捆绑包必须具有自己的包。
* Java实施放置在其API下的实施包中。


请注意，这些约定不一定需要应用于客户实施，但请务必定义并遵守约定，以便代码可持续维护。

理想情况下，姓名应表明其意图。 当名称不够清晰时，常见的代码测试是存在解释变量或方法的用途的注释：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清楚</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d； //用天表示的时间</p> </td>
   <td><p>int elapsedTimeInDays；</p> </td>
  </tr>
  <tr>
   <td><p>//get标记的图像<br /> 公共列表getItems() {}</p> </td>
   <td><p>公共列表getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重复您自己  {#don-t-repeat-yourself}

DRY声明同一组代码绝不应重复。 这也适用于字符串文本等。 代码复制为需要更改的内容打开了缺陷的大门，应该寻找并消除这些缺陷。

### 避免使用裸的CSS规则 {#avoid-naked-css-rules}

CSS规则应特定于应用程序上下文中的目标元素。 例如，应用于 *.content .center* 过于广泛，最终可能会影响您系统中的许多内容，从而要求其他人将来覆盖此样式。 *.myapp-centertext* 将是一个更具体的规则，因为它指定居中 *text* 在应用程序的上下文中。

### 消除使用已弃用的API {#eliminate-usage-of-deprecated-apis}

弃用API后，最好始终查找新的推荐方法，而不是依赖已弃用的API。 这将确保未来升级更加顺畅。

### 编写可本地化的代码 {#write-localizable-code}

不应由作者提供的任何字符串应通过封装在AEM i18n词典的调用中 *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 在JavaScript中。 如果找不到任何实施，此实施将返回传递给它的字符串，因此在使用主要语言实施功能后，这提供了实施本地化的灵活性。

### 为安全起见而转义资源路径 {#escape-resource-paths-for-safety}

虽然JCR中的路径不应包含空格，但它们的存在不应导致代码中断。 Jackrabbit提供了一个文本实用程序类，其中 *escape()* 和 *escapePath()* 方法。 对于JSP，Granite UI公开 *granite：encodeURIPath() EL* 函数。

### 使用XSS API和/或HTL抵御跨站点脚本攻击 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供了一个XSS API，用于轻松清除参数并确保免受跨站点脚本攻击的安全。 此外，HTL还将这些保护直接内置到模板语言中。 API备忘表可从以下位置下载： [开发 — 准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md).

### 实施适当的日志记录 {#implement-appropriate-logging}

对于Java代码，AEM支持slf4j作为用于记录消息的标准API，并且应该与通过OSGi控制台提供的配置结合使用，以确保管理的一致性。 Slf4j公开五个不同的日志记录级别。 我们建议在选择记录消息的级别时遵循以下准则：

* 错误：当代码中的某些内容损坏时，处理无法继续。 此问题通常因意外异常而发生。 在这些场景中包含栈栈跟踪通常很有帮助。
* 警告：当某些内容未正确工作时，可以继续处理。 这通常是由于我们预期的例外情况所致，例如 *PathNotFoundException*.
* 信息：监视系统时有用的信息。 请记住，这是默认设置，大多数客户将在其环境中保留此设置。 因此，请勿过度使用它。
* DEBUG：有关处理的较低级别信息。 在调试支持问题时很有用。
* TRACE：最低级别信息，如输入/退出方法。 这通常仅由开发人员使用。

对于JavaScript， *console.log* 应仅在开发期间使用，并且所有日志语句都应在发布之前删除。

### 避免货运狂热编程 {#avoid-cargo-cult-programming}

避免在不了解代码作用的情况下复制代码。 如有疑问，最好始终询问对您不熟悉的模块或API有更多经验的人员。
