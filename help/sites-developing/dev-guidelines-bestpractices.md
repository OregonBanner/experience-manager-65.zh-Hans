---
title: AEM开发 — 准则和最佳实践
seo-title: AEM开发 — 准则和最佳实践
description: 在AEM上开发的准则和最佳实践
seo-description: 在AEM上开发的准则和最佳实践
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---

# AEM开发 — 准则和最佳实践{#aem-development-guidelines-and-best-practices}

## 使用模板和组件的准则{#guidelines-for-using-templates-and-components}

AEM组件和模板构成了一个非常强大的工具包。 开发人员可以使用这些组件为网站业务用户、编辑人员和管理员提供功能，使其网站能够适应不断变化的业务需求（内容敏捷性），同时保持网站的统一布局（品牌保护）。

对于负责网站或网站集的人员（例如在全球企业的分支机构）来说，一个典型的挑战是在其网站上引入一种新类型的内容演示。

假设需要向网站中添加新闻列表页面，该页面会列出已发布的其他文章的摘要。 页面的设计和结构应与网站的其他部分相同。

应对这种挑战的建议方法是：

* 重复使用现有模板来创建新类型的页面。 模板大致定义了页面结构（导航元素、面板等），该结构可通过其设计（CSS、图形）进一步进行微调。
* 在新页面上使用段落系统(parsys/iparsys)。
* 定义段落系统“设计”模式的访问权限，以便只有经授权的人员（通常是管理员）才能更改这些权限。
* 定义给定段落系统中允许使用的组件，以便编辑器随后将所需的组件放在页面上。 在我们的示例中，它可以是列表组件，组件可以遍历页面的子树，并根据预定义的规则提取信息。
* 编辑者在他们负责的页面上添加并配置允许的组件，以将所请求的功能（信息）交付给企业。

这说明了此方法如何让网站的参与用户和管理员能够快速响应业务需求，而无需开发团队的参与。 替代方法（如创建新模板）通常代价高昂，需要变革管理过程和开发团队的参与。 这会使整个过程更长、成本更高。

因此，基于AEM的系统的开发人员应使用：

* 用于统一和品牌保护的段落系统设计的模板和访问控制
* 段落系统，包括其灵活配置选项。

在大多数常见项目中，以下面向开发人员的一般规则是有意义的：

* 将模板数保持为低 — 低于网站上从根本上不同的页面结构数。
* 为您的自定义组件提供必要的灵活性和配置功能。
* 最大限度地利用AEM段落系统（parsys和iparsys组件）的强大功能和灵活性。

### 自定义组件和其他元素{#customizing-components-and-other-elements}

创建自己的组件或自定义现有组件时，通常最简单（也最安全）的方法是重复使用现有定义。 同样的原则也适用于AEM中的其他元素，例如错误处理程序。

可通过复制和叠加现有定义来完成此操作。 换言之，将定义从`/libs`复制到`/apps/<your-project>`。 `/apps`中的此新定义可根据您的要求进行更新。

>[!NOTE]
>
>有关更多详细信息，请参阅[使用叠加](/help/sites-developing/overlays.md)。

例如：

* [自定义组件](/help/sites-developing/components.md)

   这涉及到覆盖组件定义：

   * 通过复制现有组件在`/apps/<website-name>/components/<MyComponent>`中创建新组件文件夹：

      * 例如，要自定义文本组件副本，请执行以下操作：

         * 从 `/libs/foundation/components/text`
         * 到 `/apps/myProject/components/text`

* [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   此例涉及覆盖Servlet:

   * 在存储库中，复制默认脚本：

      * 从 `/libs/sling/servlet/errorhandler/`
      * 到 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**不得**&#x200B;更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>对于配置和其他更改：
>
>1. 将`/libs`中的项目复制到`/apps`
>1. 在`/apps`中进行任何更改


## 何时使用JCR查询以及何时不使用{#when-to-use-jcr-queries-and-when-not-to-use-them}

正确使用JCR查询时，JCR查询是一款功能强大的工具。 它们适用于：

* 真正的最终用户查询，如对内容的全文搜索。
* 有时，需要在整个存储库中找到结构化内容。

   在这种情况下，请确保查询仅在绝对需要时运行，例如在组件激活或缓存失效时（而不是在工作流步骤、在内容修改时触发的事件处理程序、过滤器等）。

JCR查询绝不应用于纯渲染请求。 例如，JCR查询不适用于

* 渲染导航
* 创建“前10个最新新闻项目”概述
* 显示内容项目计数

要渲染内容，请使用内容树的导航访问权限，而不是执行JCR查询。

>[!NOTE]
>
>如果使用[查询生成器](/help/sites-developing/querybuilder-api.md)，则使用JCR查询，因为查询生成器会在引擎盖下生成JCR查询。


## 安全注意事项{#security-considerations}

>[!NOTE]
>
>此外，还值得参考[安全检查表](/help/sites-administering/security-checklist.md)。

### JCR（存储库）会话{#jcr-repository-sessions}

您应使用用户会话，而不是管理会话。 这意味着您应使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect针对跨站点脚本(XSS){#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)允许攻击者将代码注入其他用户查看的网页中。 恶意Web用户可能会利用此安全漏洞绕过访问控制。

AEM在输出时应用过滤所有用户提供内容的原则。 在开发和测试过程中，防止XSS都是最优先的任务。

此外，Web应用程序防火墙（如Apache](https://modsecurity.org)的[mod_security）可以提供对部署环境安全的可靠、集中的控制，并防止以前未检测到的跨站点脚本攻击。

>[!CAUTION]
>
>随AEM提供的示例代码本身可能无法抵御此类攻击，并且通常依赖于Web应用程序防火墙的请求过滤。

XSS API速查表包含您需要了解的信息，以便使用XSS API并使AEM应用程序更加安全。 您可以在此处下载它：

XSSAPI备忘单。

[获取文件](assets/xss_cheat_sheet_2016.pdf)

### 保护机密信息的通信{#securing-communication-for-confidential-information}

对于任何Internet应用程序，请确保在传输机密信息时

* 通过SSL保护流量
* HTTPPOST（如果适用）

这适用于对系统保密的信息（如配置或管理访问），以及对其用户保密的信息（如其个人详细信息）

## 不同的开发任务{#distinct-development-tasks}

### 自定义错误页{#customizing-error-pages}

可以为AEM自定义错误页面。 这是一种建议，以便实例不会在内部服务器错误上显示sling跟踪。

有关完整详细信息，请参阅[自定义错误处理程序](/help/sites-developing/customizing-errorhandler-pages.md)显示的错误页面。

### 在Java进程{#open-files-in-the-java-process}中打开文件

由于AEM可以访问大量文件，因此建议为AEM明确配置[为Java进程打开的文件数](/help/sites-deploying/configuring.md#open-files-in-the-java-process)。

要最大限度地减少此问题的发展，应确保尽快（有意义地）正确关闭任何打开的文件。
