---
title: 编码提示
seo-title: 编码提示
description: 关于AEM编码的提示
seo-description: 关于AEM编码的提示
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# 编码提示{#coding-tips}

## 尽可能使用taglibs或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含脚本，使得调试代码中的问题变得困难。 另外，在JSP中加入脚本，很难将业务逻辑与视图层分离，这违反了单责原则和MVC设计模式。

### 写入可读代码{#write-readable-code}

代码只写一次，但会读多次。 我们需要提前一段时间清理我们所写的代码，这样我们和其他开发者以后需要阅读时，就会在路上派发股息。

### 选择显示意图的名称{#choose-intention-revealing-names}

理想情况下，另一个程序员应该不必打开一个模块来了解它的功能。 同样，他们应该能够在不阅读方法的情况下判断方法的用途。 我们越能订阅这些想法，就越容易阅读代码，我们编写和更改代码的速度就越快。

在AEM代码库中，使用以下约定：


* 接口的单个实现名为`<Interface>Impl`，即`ReaderImpl`。
* 接口的多个实现名为`<Variant><Interface>`，即`JcrReader`和`FileSystemReader`。
* 抽象基类名为`Abstract<Interface>`或`Abstract<Variant><Interface>`。
* 包名为`com.adobe.product.module`。  每个Maven藏物或OSGi包必须有其自己的包。
* Java实施放置在其API下方的实施包中。


请注意，这些约定不一定需要应用于客户实施，但务必要定义并遵守约定，以便代码能够保持可维护。

理想情况下，名字应该显示其意图。 名称不应清晰时的常见代码测试是，存在一些说明变量或方法用途的注释：

<table>
 <tbody>
  <tr>
   <td><p><strong>不明</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//已用时间（以天为单位）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get标记的图像<br />公共列表getItems(){}</p> </td>
   <td><p>public List getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重复自己的{#don-t-repeat-yourself}

DRY声明，同一组代码绝不应重复。 这也适用于字符串文本之类的内容。 每当有需要改变的事情时，代码重复就会为缺陷打开大门，需要寻找和消除。

### 避免裸CSS规则{#avoid-naked-css-rules}

CSS规则应该特定于应用程序上下文中的目标元素。 例如，应用于&#x200B;*.content .center*&#x200B;的CSS规则将过于宽泛，可能最终会影响您系统中的许多内容，要求其他人将来覆盖此样式。 *.myapp-centertextw* 可能是一个更具体的规则，因为它在应用程序 ** 的上下文中指定居中文本。

### 消除对已弃用API {#eliminate-usage-of-deprecated-apis}的使用

当API被弃用时，最好找到新的推荐方法，而不是依赖已弃用的API。 这将确保未来更顺利的升级。

### 写入可本地化的代码{#write-localizable-code}

作者未提供的任何字符串都应包含在JavaScript中通过&#x200B;*I18n.get()*&#x200B;的JSP/Java和&#x200B;*CQ.I18n.get()*&#x200B;对AEM i18n词典的调用中。 此实施将返回在未找到实施时传递给它的字符串，因此在以主语言实施功能后，这样就可以灵活地实施本地化。

### 为安全{#escape-resource-paths-for-safety}转义资源路径

虽然JCR中的路径不应包含空格，但是它们的存在不应导致代码中断。 Jackrabbit提供了一个Text实用程序类，该类包含&#x200B;*escape()*&#x200B;和&#x200B;*escapePath()*&#x200B;方法。 对于JSP，Granite UI会公开&#x200B;*granite:encodeURIPath()EL*&#x200B;函数。

### 使用XSS API和/或HTL防止跨站点脚本攻击{#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供了XSS API，可轻松清理参数并确保免受跨站点脚本攻击的安全。 此外，HTL还直接在模板语言中内置了这些保护。 可在[开发 — 准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)下载API备忘单。

### 实施适当的日志记录{#implement-appropriate-logging}

对于Java代码，AEM支持将slf4j作为记录消息的标准API，并且应与通过OSGi控制台提供的配置结合使用，以保持管理的一致性。 Slf4j会公开五个不同的日志记录级别。 在选择要在中记录消息的级别时，我们建议遵循以下准则：

* 错误：当代码中的某些内容已损坏，且处理无法继续。 这通常是意外异常的结果。 在这些情况下包含堆栈跟踪通常非常有用。
* 警告：当某些组件无法正常工作，但处理可以继续。 这通常是我们预期的异常的结果，例如&#x200B;*PathNotFoundException*。
* 信息：在监控系统时有用的信息。 请记住，这是默认设置，大多数客户都会将其保留在其环境中。 因此，请勿过度使用。
* 调试：有关处理的较低级别信息。 在调试支持的问题时很有用。
* TRACE:最低级别的信息，如进入/退出方法。 这通常仅供开发人员使用。

对于JavaScript，应仅在开发期间使用&#x200B;*console.log* ，并且所有log语句都应在发布之前删除。

### 避免货物追踪编程{#avoid-cargo-cult-programming}

在不了解代码功能的情况下，避免复制代码。 如有疑问，最好向对模块或API具有更多经验且您不清楚的人员提出问题。
