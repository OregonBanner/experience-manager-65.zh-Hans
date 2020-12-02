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
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---


# 编码提示{#coding-tips}

## 尽可能使用标语或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含scriptlet使得调试代码中的问题变得困难。 此外，在JSP中加入scriptlet很难将业务逻辑与视图层分离，这违反了单责任原则和MVC设计模式。

### 写入可读代码{#write-readable-code}

代码只写一次，但读多次。 我们会花一些时间在前面清理我们编写的代码，这样我们和其他开发者需要稍后阅读它时，就会付出回报。

### 选择意图——显示名称{#choose-intention-revealing-names}

理想情况下，其他程序员不必打开一个模块来了解其功能。 同样，他们应该能够在不阅读方法的情况下判断方法的用途。 我们订阅这些想法越好，阅读代码就越容易，编写和更改代码的速度就越快。

在AEM代码库中，使用以下约定：


* 接口的单个实现名为`<Interface>Impl`，即`ReaderImpl`。
* 接口的多个实现命名为`<Variant><Interface>`，即`JcrReader`和`FileSystemReader`。
* 抽象基类名为`Abstract<Interface>`或`Abstract<Variant><Interface>`。
* 包名为`com.adobe.product.module`。  每个Maven藏物或OSGi捆绑包必须有其自己的包。
* Java实现位于其API下的实施包中。


请注意，这些约定不一定需要应用于客户实施，但必须定义和遵守约定，以使代码保持可维护性。

理想情况下，名字应该能揭示出自己的意图。 当名称不应该清晰时，常用的代码测试是存在说明变量或方法用途的注释：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清晰</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//已用时间（天）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br />公共列表getItems(){}</p> </td>
   <td><p>公共列表getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重复自己的{#don-t-repeat-yourself}

DRY声明，不应复制同一组代码。 这也适用于字符串文字等内容。 代码复制为任何需要改变的事物打开了缺陷之门，需要找出并消除缺陷。

### 避免裸CSS规则{#avoid-naked-css-rules}

CSS规则应该特定于应用程序上下文中的目标元素。 例如，应用于&#x200B;*.content .center*&#x200B;的CSS规则将过于宽泛，可能最终影响整个系统的大量内容，要求其他人将来覆盖此样式。 *.myapp-* centertexttw将是更具体的规则，因为它将在应用程 ** 序上下文中指定居中文本。

### 消除已弃用API的使用{#eliminate-usage-of-deprecated-apis}

当API被弃用时，总是最好找到建议的新方法，而不是依赖已弃用的API。 这将确保将来更顺利地升级。

### 写入可本地化的代码{#write-localizable-code}

创作者未提供的任何字符串都应打包在通过JSP/Java中的&#x200B;*I18n.get()*&#x200B;和JavaScript中的&#x200B;*CQ.I18n.get()*&#x200B;调用AEM的i18n词典中。 如果找不到任何实现，此实现将返回传递给它的字符串，因此这优惠了在主语言中实现这些功能后实现本地化的灵活性。

### 安全{#escape-resource-paths-for-safety}的转义资源路径

虽然JCR中的路径不应包含空格，但它们的存在不应导致代码中断。 Jackrabbit提供具有&#x200B;*escape()*&#x200B;和&#x200B;*escapePath()*&#x200B;方法的文本实用程序类。 对于JSP,Granite UI显示&#x200B;*granite:encodeURIPath()EL*&#x200B;函数。

### 使用XSS API和／或HTL防止跨站点脚本攻击{#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供了一个XSS API，可轻松清理参数并确保避免跨站点脚本攻击的安全性。 此外，HTL还直接将这些保护内置到模板语言中。 可从[开发——准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)下载API备忘单。

### 实施适当的日志记录{#implement-appropriate-logging}

对于Java代码，AEM支持slf4j作为记录消息的标准API，并应与通过OSGi控制台提供的配置结合使用，以便在管理中保持一致。 Slf4j显示五个不同的日志记录级别。 我们建议在选择在哪个级别登录消息时使用以下准则：

* 错误：当代码中的某些内容已损坏，且处理无法继续。 这通常是意外异常的结果。 在这些情况下包含堆栈跟踪通常很有帮助。
* 警告：当某些内容无法正常工作，但处理可以继续。 这通常是我们预期的异常的结果，如&#x200B;*PathNotFoundException*。
* 信息：在监视系统时有用的信息。 请记住，这是默认设置，大多数客户都会将其保留在环境上。 因此，不要过度使用它。
* 调试：有关处理的较低级别信息。 在调试支持问题时很有用。
* TRACE:最低级别信息，如输入／退出方法。 这通常只供开发人员使用。

对于JavaScript,*console.log*&#x200B;只应在开发过程中使用，并且在发布之前应删除所有日志语句。

### 避免货物崇拜编程{#avoid-cargo-cult-programming}

避免在不了解代码功能的情况下复制代码。 如果存疑，最好向对模块或API有更多经验、但您不清楚的人询问。
