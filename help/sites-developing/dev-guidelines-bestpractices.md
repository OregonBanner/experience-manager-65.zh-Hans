---
title: AEM开发 — 准则和最佳实践
seo-title: AEM Development - Guidelines and Best Practices
description: 在AEM上开发的准则和最佳实践
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# AEM开发 — 准则和最佳实践{#aem-development-guidelines-and-best-practices}

## 使用模板和组件的准则 {#guidelines-for-using-templates-and-components}

AEM组件和模板构成了一个功能非常强大的工具包。 开发人员可以使用它们为网站业务用户、编辑和管理员提供使其网站适应不断变化的业务需求（内容敏捷性）的功能，同时保留网站的统一布局（品牌保护）。

对负责一个网站或一组网站（例如，在全球企业的一个分支办公室中）的人员来说，一个典型的挑战是在其网站上引入一种新类型的内容演示。

假设需要向网站添加新闻列表页面，其中列出了从其他已发布的文章中提取的内容。 页面应具有与网站其余部分相同的设计和结构。

应对这一挑战的建议方法是：

* 重用现有模板以创建新类型的页面。 模板粗略地定义了页面结构（导航元素、面板等），该页面结构通过其设计（CSS、图形）进一步细化。
* 在新页面上使用段落系统(parsys/iparsys)。
* 定义对段落系统设计模式的访问权限，以便只有授权人员（通常是管理员）才能更改这些权限。
* 定义给定段落系统中允许的组件，以便编辑器随后将所需的组件放在页面上。 在我们的例子中，它可以是一个列表组件，它可以遍历页面的子树，并根据预定义的规则提取信息。
* 编辑者在他们负责的页面上添加和配置允许的组件，以便为业务提供所请求的功能（信息）。

这说明了这种方法如何使网站贡献用户和管理员能够快速响应业务需求，而无需开发团队的参与。 替代方法，如创建新模板，通常是一项费用高昂的工作，需要变更管理过程和开发团队的参与。 这使得整个过程耗时更长，成本更高。

因此，基于AEM的系统的开发人员应使用：

* 用于统一性和品牌保护的段落系统设计模板和访问控制
* 段落系统，包括其配置选项，以提供灵活性。

以下适用于开发人员的一般规则适用于大多数常规项目：

* 保持较低的模板数量 — 与网站上完全不同的页面结构数量一样低。
* 为自定义组件提供必要的灵活性和配置功能。
* 最大限度地利用AEM段落系统（parsys和iparsys组件）的强大功能和灵活性。

### 自定义组件和其他元素 {#customizing-components-and-other-elements}

在创建自己的组件或自定义现有组件时，重复使用现有定义通常最简单（也最安全）。 同样的原则也适用于AEM中的其他元素，例如错误处理程序。

这可以通过复制和覆盖现有定义来完成。 换句话说，从以下位置复制定义： `/libs` 到 `/apps/<your-project>`. 此新定义，位于 `/apps`，可以根据您的要求进行更新。

>[!NOTE]
>
>参见 [使用叠加](/help/sites-developing/overlays.md) 了解更多详细信息。

例如：

* [自定义组件](/help/sites-developing/components.md)

  这涉及覆盖组件定义：

   * 在中创建新组件文件夹 `/apps/<website-name>/components/<MyComponent>` 通过复制现有组件：

      * 例如，要自定义文本组件副本，请执行以下操作：

         * 从 `/libs/foundation/components/text`
         * 到 `/apps/myProject/components/text`

* [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  这种情况涉及覆盖servlet：

   * 在存储库中，复制默认脚本：

      * 从 `/libs/sling/servlet/errorhandler/`
      * 到 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>您 **不得** 更改 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>对于配置和其他更改：
>
>1. 将项目复制到 `/libs` 到 `/apps`
>1. 在中进行任何更改 `/apps`

## 何时使用JCR查询以及何时不使用它们 {#when-to-use-jcr-queries-and-when-not-to-use-them}

正确使用时，JCR查询是一个功能强大的工具。 它们适用于：

* 真正的最终用户查询，例如对内容的全文搜索。
* 需要在整个存储库中找到结构化内容的情况。

  在这种情况下，请确保查询仅在绝对需要时运行，例如在组件激活或缓存失效时（而不是在内容修改时触发的工作流步骤、事件处理程序、过滤器等）。

绝不能将JCR查询用于纯渲染请求。 例如，JCR查询不适用于

* 渲染导航
* 创建“前10大最新新闻项目”概述
* 显示内容项目的计数

要呈现内容，请使用对内容树的导航访问权限，而不是执行JCR查询。

>[!NOTE]
>
>如果您使用 [查询生成器](/help/sites-developing/querybuilder-api.md)，您使用JCR查询，因为查询生成器会生成JCR查询。
>

## 安全注意事项 {#security-considerations}

>[!NOTE]
>
>此外，您还应该参考 [安全核对清单](/help/sites-administering/security-checklist.md).

### JCR（存储库）会话 {#jcr-repository-sessions}

您应该使用用户会话，而不是管理会话。 这意味着您应该使用：

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect防止跨站点脚本(XSS) {#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)允许攻击者将代码注入其他用户查看的网页中。 此安全漏洞可被恶意Web用户利用来绕过访问控制。

AEM应用了在输出时筛选所有用户提供的内容的原则。 在开发和测试过程中，防御XSS被列为最高优先事项。

此外，Web应用程序防火墙，例如 [适用于Apache的mod_security](https://modsecurity.org)提供了对部署环境的安全性的可靠集中控制，并抵御以前未检测到的跨站点脚本攻击。

>[!CAUTION]
>
>随AEM提供的示例代码本身可能无法抵御此类攻击，通常依赖于Web应用程序防火墙的请求过滤。

XSS API备忘表包含要使用XSS API并使AEM应用程序更安全而需要了解的信息。 您可以在此处下载它：

XSSAPI备忘单。

[获取文件](assets/xss_cheat_sheet_2016.pdf)

### 保护机密信息的通信 {#securing-communication-for-confidential-information}

对于任何Internet应用程序，请确保在传输机密信息时

* 通过SSL保护流量
* 如果适用，则使用HTTPPOST

这适用于对系统保密的信息（如配置或管理访问权限）及其用户保密的信息（如其个人详细信息）

## 不同的开发任务 {#distinct-development-tasks}

### 自定义错误页面 {#customizing-error-pages}

可以为AEM自定义错误页面。 建议这样做，以便实例不会显示内部服务器错误上的Sling跟踪。

参见 [自定义错误处理程序显示的错误页面](/help/sites-developing/customizing-errorhandler-pages.md) 以了解完整的详细信息。

### 在Java进程中打开文件 {#open-files-in-the-java-process}

由于AEM可以访问大量文件，因此建议将 [打开Java进程的文件](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 已为AEM明确配置。

为了最大限度地减少此问题，开发应确保尽快（有意义）正确关闭任何打开的文件。
