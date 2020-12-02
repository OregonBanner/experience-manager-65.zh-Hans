---
title: AEM开发——准则和最佳实践
seo-title: AEM开发——准则和最佳实践
description: 在AEM上制定指南和最佳做法
seo-description: 在AEM上制定指南和最佳做法
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---


# AEM开发——准则和最佳实践{#aem-development-guidelines-and-best-practices}

## 使用模板和组件{#guidelines-for-using-templates-and-components}的准则

AEM组件和模板构成了一个非常强大的工具包。 开发人员可以使用它们为网站业务用户、编辑人员和管理员提供功能，使其网站能够适应不断变化的业务需求（内容敏捷性），同时保持网站的统一布局（品牌保护）。

对于负责网站或网站集（例如，在全球性企业的分支机构中）的人员来说，一个典型的挑战是在其网站上引入一种新类型的内容演示。

我们假定需要向网站添加新闻列表页面，列表从已发布的其他文章中提取该页面。 页面的设计和结构应与网站的其余部分相同。

应对这种挑战的建议方法是：

* 重复使用现有模板以创建新类型的页面。 模板粗略地定义了页面结构（导航元素、面板等），其设计（CSS、图形）进一步对此结构进行了微调。
* 在新页面上使用段落系统(parsys/iparsys)。
* 定义段落系统“设计”模式的访问权限，以便只有经授权的人员（通常是管理员）才能更改它们。
* 定义给定段落系统中允许的组件，这样编辑人员就可以将所需的组件放在页面上。 在我们的情况下，它可以是列表组件，它可以遍历页面的子树，并根据预定义的规则提取信息。
* 编辑人员在他们负责的页面上添加和配置允许的组件，以向企业提供所请求的功能（信息）。

这说明了这种方法如何帮助网站的贡献用户和管理员快速响应业务需求，而无需开发团队的参与。 另一种方法，如创建新模板，通常代价高昂，需要变革管理过程和开发团队的参与。 这使整个过程更长、成本更高。

因此，基于AEM的系统的开发人员应使用：

* 段落系统设计的模板和访问控制，以实现一致性和品牌保护
* 段落系统包括其灵活性配置选项。

在大多数常见项目中，针对开发人员的以下一般规则是有意义的：

* 将模板数保持在低位——低于网站上根本不同的页面结构数。
* 为您的自定义组件提供必要的灵活性和配置功能。
* 最大限度地利用AEM段落系统（parsys和iparsys组件）的功能和灵活性。

### 自定义组件和其他元素{#customizing-components-and-other-elements}

创建您自己的组件或自定义现有组件时，通常最容易（也最安全）重用现有定义。 同样的原则也适用于AEM中的其他元素，例如错误处理程序。

这可以通过复制和覆盖现有定义来完成。 换言之，将定义从`/libs`复制到`/apps/<your-project>`。 此新定义位于`/apps`中，可以根据您的要求进行更新。

>[!NOTE]
>
>有关详细信息，请参阅[使用叠加](/help/sites-developing/overlays.md)。

例如：

* [自定义组件](/help/sites-developing/components.md)

   这涉及覆盖组件定义：

   * 通过复制现有组件在`/apps/<website-name>/components/<MyComponent>`中创建新组件文件夹：

      * 例如，要自定义文本组件副本，请执行以下操作：

         * 从 `/libs/foundation/components/text`
         * 到 `/apps/myProject/components/text`

* [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   本例涉及覆盖servlet:

   * 在存储库中，复制默认脚本：

      * 从 `/libs/sling/servlet/errorhandler/`
      * 到 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>您&#x200B;**不得**&#x200B;更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>对于配置和其他更改：
>
>1. 将`/libs`中的项复制到`/apps`
>1. 在`/apps`中进行任何更改


## 何时使用JCR查询，何时不使用{#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR查询在正确使用时是一个强大的工具。 它们适用于：

* 真正的最终用户查询，如内容全文搜索。
* 需要在整个存储库中找到结构化内容的情况。

   在这种情况下，请确保查询仅在绝对需要时运行，例如，在组件激活或缓存失效时(与工作流步骤、在内容修改时触发的事件处理程序、过滤器等相反)。

JCR查询永远不应用于纯渲染请求。 例如，JCR查询不适用于

* 渲染导航
* 创建“十大最新新闻项目”概述
* 显示内容项的计数

对于渲染内容，请使用对内容树的导航访问，而不是执行JCR查询。

>[!NOTE]
>
>如果使用[查询生成器](/help/sites-developing/querybuilder-api.md)，则使用JCR查询，因为查询生成器在内部生成JCR查询。


## 安全注意事项{#security-considerations}

>[!NOTE]
>
>还值得参考[安全清单](/help/sites-administering/security-checklist.md)。

### JCR（存储库）会话{#jcr-repository-sessions}

您应使用用户会话，而不是管理会话。 这意味着您应使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect反对跨站点脚本(XSS){#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)使攻击者能够将代码注入其他用户查看的网页中。 恶意Web用户可能利用此安全漏洞绕过访问控制。

AEM在输出时应用过滤所有用户提供的内容的原则。 在开发和测试过程中，防止XSS优先。

此外，Web应用程序防火墙（如Apache](https://modsecurity.org)的[mod_security）可以提供对部署环境安全的可靠、集中的控制，并防止以前未检测到的跨站点脚本攻击。

>[!CAUTION]
>
>随AEM提供的示例代码本身可能无法抵御此类攻击，并且通常依赖Web应用程序防火墙的请求过滤。

XSS API备忘单包含您需要了解的信息，以便使用XSS API并使AEM应用程序更安全。 您可以在以下位置下载它：

XSSAPI备忘单。

[获取文件](assets/xss_cheat_sheet_2016.pdf)

### 保护机密信息通信{#securing-communication-for-confidential-information}

对于任何Internet应用程序，请确保在传输机密信息时

* 通信通过SSL进行保护
* HTTPPOST（如果适用）

这适用于对系统保密的信息（如配置或管理访问）以及对用户保密的信息（如其个人详细信息）

## 独特的开发任务{#distinct-development-tasks}

### 自定义错误页面{#customizing-error-pages}

可以为AEM自定义错误页面。 这是建议的，这样实例不会在内部服务器错误上显示sling跟踪。

有关完整的详细信息，请参阅[自定义错误处理程序](/help/sites-developing/customizing-errorhandler-pages.md)显示的错误页面。

### 在Java进程{#open-files-in-the-java-process}中打开文件

由于AEM可以访问大量文件，因此建议为AEM显式配置Java进程[打开的文件数。](/help/sites-deploying/configuring.md#open-files-in-the-java-process)

为最大限度地减少此问题的发展，应确保尽可能快（有意义）正确关闭任何打开的文件。
