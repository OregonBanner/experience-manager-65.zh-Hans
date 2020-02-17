---
title: AEM开发——准则和最佳实践
seo-title: AEM开发——准则和最佳实践
description: 在AEM上开发的准则和最佳做法
seo-description: 在AEM上开发的准则和最佳做法
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM开发——准则和最佳实践{#aem-development-guidelines-and-best-practices}

## 使用模板和组件的准则 {#guidelines-for-using-templates-and-components}

AEM组件和模板构成了一个功能强大的工具包。 开发人员可以使用它们为网站业务用户、编辑人员和管理员提供功能，使其网站适应不断变化的业务需求（内容敏捷性），同时保持网站的统一布局（品牌保护）。

对于负责网站或网站集的人（例如，在全球企业的分支机构中）来说，一个典型的挑战是在其网站上引入一种新类型的内容演示。

假设需要向网站添加新闻列表页面，该页面会列出已发布的其他文章的提取内容。 页面的设计和结构应与网站的其余部分相同。

应对此类挑战的建议方法是：

* 重复使用现有模板以创建新类型的页面。 模板粗略地定义了页面结构（导航元素、面板等），该结构通过其设计（CSS、图形）进一步进行了微调。
* 在新页面上使用段落系统(parsys/iparsys)。
* 定义对段落系统“设计”模式的访问权限，以便只有授权人员（通常是管理员）才能更改这些权限。
* 定义给定段落系统中允许的组件，这样编辑人员就可以将所需的组件放在页面上。 在我们的例子中，它可以是列表组件，它可以遍历页面的子树并根据预定义的规则提取信息。
* 编辑人员在他们负责的页面上添加和配置允许的组件，以将所请求的功能（信息）交付给企业。

这说明了这种方法如何帮助网站的贡献用户和管理员快速响应业务需求，而无需开发团队的参与。 创建新模板等替代方法通常代价高昂，需要变革管理过程和开发团队的参与。 这使整个过程更长、成本更高。

因此，基于AEM的系统的开发人员应使用：

* 模板和访问控制，以实现一致性和品牌保护的段落系统设计
* 段落系统包括其配置选项，以实现灵活性。

对于大多数常见项目来说，针对开发人员的以下一般规则是有意义的：

* 将模板数量保持在低位——低至网站上完全不同的页面结构数量。
* 为您的自定义组件提供必要的灵活性和配置功能。
* 充分利用AEM段落系统（parsys和iparsys组件）的强大功能和灵活性。

### 自定义组件和其他元素 {#customizing-components-and-other-elements}

创建您自己的组件或自定义现有组件时，重新使用现有定义通常最简单（也最安全）。 同样的原则也适用于AEM中的其他元素，例如错误处理程序。

这可以通过复制和覆盖现有定义来完成。 换句话说，将定义从复制到 `/libs` 中 `/apps/<your-project>`。 中的此新定义 `/apps`可以根据您的要求进行更新。

>[!NOTE]
>
>有关更 [多详细信息](/help/sites-developing/overlays.md) ，请参阅使用叠加。

例如：

* [自定义组件](/help/sites-developing/components.md)

   这涉及覆盖组件定义：

   * 通过复制现有组件在中 `/apps/<website-name>/components/<MyComponent>` 创建新组件文件夹：

      * 例如，要自定义文本组件副本，请执行以下操作：

         * 起始日期: `/libs/foundation/components/text`
         * 到 `/apps/myProject/components/text`

* [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   此例涉及覆盖servlet:

   * 在存储库中，复制默认脚本：

      * 起始日期: `/libs/sling/servlet/errorhandler/`
      * 到 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>您 **不得更改** 路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
>
>对于配置和其他更改：
>
>1. 将项目复制到 `/libs``/apps`
>1. 在 `/apps`


## 何时使用JCR查询以及何时不使用它们 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR查询是正确使用时的强大工具。 它们适用于：

* 真实的最终用户查询，如内容的全文搜索。
* 需要在整个存储库中找到结构化内容的场合。

   在这种情况下，请确保查询仅在绝对需要时运行，例如，在组件激活或缓存失效时（与工作流步骤、在内容修改时触发的事件处理函数、过滤器等相反）。

JCR查询绝不应用于纯渲染请求。 例如，JCR查询不适用于

* 渲染导航
* 创建“十大最新新闻项目”概述
* 显示内容项目计数

对于渲染内容，请使用对内容树的导航访问，而不是执行JCR查询。

>[!NOTE]
>
>如果使用 [Query Builder](/help/sites-developing/querybuilder-api.md)，则使用JCR查询，因为Query builder在后台生成JCR查询。


## 安全注意事项 {#security-considerations}

>[!NOTE]
>
>参考安全清单也是值得 [参考的](/help/sites-administering/security-checklist.md)。

### JCR（存储库）会话 {#jcr-repository-sessions}

您应使用用户会话，而不是管理会话。 这意味着您应使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### 防止跨站点脚本(XSS) {#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)使攻击者能够将代码注入其他用户查看的网页中。 恶意Web用户可能会利用该安全漏洞绕过访问控制。

AEM在输出时应用过滤所有用户提供的内容的原则。 在开发和测试过程中，防止XSS的优先级最高。

此外，Web应用程序防火墙(如Apache的 [mod_security](https://modsecurity.org))可以提供对部署环境安全的可靠、集中的控制，并防止以前未被检测到的跨站点脚本攻击。

>[!CAUTION]
>
>随AEM提供的示例代码本身可能不会针对此类攻击提供保护，并且通常依赖Web应用程序防火墙的请求过滤。

XSS API备忘单包含您需要了解的信息，以便使用XSS API并使AEM应用程序更加安全。 您可以在以下位置下载它：

XSSAPI备忘单。

[获取文件](assets/xss_cheat_sheet_2016.pdf)

### 保护机密信息的通信 {#securing-communication-for-confidential-information}

至于任何Internet应用程序，请确保在传输机密信息时

* 通信通过SSL进行保护
* HTTP POST（如果适用）

这适用于对系统保密的信息（如配置或管理访问）以及对用户保密的信息（如其个人详细信息）

## 独特的开发任务 {#distinct-development-tasks}

### 自定义错误页面 {#customizing-error-pages}

可以为AEM自定义错误页面。 这是建议的，因此实例不会在内部服务器错误上显示sling跟踪。

有关完 [整的详细信息，请参阅自定义错误处理程序显示的错误页](/help/sites-developing/customizing-errorhandler-pages.md) 。

### 在Java进程中打开文件 {#open-files-in-the-java-process}

由于AEM可以访问大量文件，因此建议为AEM显 [式配置Java进程的打开文件](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 。

要最大限度地减少此问题的发展，应确保尽可能快（有意义）正确关闭打开的任何文件。
