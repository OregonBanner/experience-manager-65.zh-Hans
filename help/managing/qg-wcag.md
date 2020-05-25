---
title: WCAG 2.1 快速指南
description: WCAG 2.1 快速指南
translation-type: tm+mt
source-git-commit: a8e7fe89376b30df0b1c5403aabea6862cef09fc
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 83%

---


# WCAG 2.1 快速指南{#quick-guide-to-wcag}

Adobe Experience Manager(AEM)的开发旨在最大限度地遵守Web内容辅助功能准则。

The [Web Content Accessibility Guidelines (WCAG) version 2.1](https://www.w3.org/TR/WCAG/) are a set of internationally recognized guidelines developed by the [World Wide Web Consortium (W3C)](https://www.w3.org/) under their [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

>[!NOTE]
> 
> WCAG 2.1从2008年起更新了先前版本WCAG 2.0。 请参阅 [WCAG 2.1 - 与 WCAG 2.0 的比较](https://www.w3.org/TR/WCAG21/#comparison-with-wcag-2-0)。

>[!NOTE]
> 
>目前正在开发[该指南的更新版本 - WCAG 2.2](https://www.w3.org/TR/WCAG22/)，但此时不予考虑更新事宜。

WCAG 2.1 包含一系列非技术层面的准则及成功标准，旨在确保残障人士能够访问并使用 Web 内容。这些准则和成功标准向 Web 内容作者、设计人员和开发人员提供建议，确保他们创作的资源可尽可能多地供更多人访问，而无论他们具有任何缺陷；例如，视觉障碍、听力损失、学习困难、年龄限制等。

例如，使用 HTML 中的 `alt` 属性描述图像（或任何其他非文本内容）会使失明或部分视力受损的人受益匪浅。`alt` 属性中的文本描述内容可以转换为语音输出或传输为可刷新的电子盲文显示屏。

Additionally, WCAG 2.1 can result in advantages for other beneficiaries, including people who may be considered *situationally disabled*. 由于浏览技术、网络连接速度或浏览环境等情况，他们可能会遇到与残障人士类似的障碍。

使用 Adobe Experience Manager，内容作者和/或网站所有者可以创建符合 WCAG 2.1 A 级和 AA 级相关成功标准的 Web 内容。

因此，要了解 Web 辅助功能以及这些准则如何帮助创建易访问 Web 内容，务必要了解 WCAG 2.1 的目标以及准则的结构方式。

WCAG 2.1 的目的是提供以下准则：

* **与技术无关：**
换句话说，准则可以应用于各种 Web 内容格式，而不仅仅是 HTML。因此，WCAG 2.1 可以涵盖由 PDF、Flash、JavaScript 和其他当前和未来 Web 技术生成或提供的内容。

* **可测试：**
每个准则均以一种可进行客观测试的方式编写，以确保一组辅助功能专家都同意同容符合该准则要求。辅助功能准则的一个挑战是，虽然一些准则在技术上可以测试，但另一些准则需要人为判断来确定是否成功达到了准则要求。

* 支持 **按优先顺序和情境实施：**
WCAG 2.1准则被赋予优先权，与不遵守关于特定残疾用户群的准则可能产生的影响有关。 这使作者能够就其特殊情况最重要的准则作出知情决定。 此外，还引入了支持 *的辅助功* 能的概念。 这允许作者决定如何最好地使用可能没有完全辅助功能支持的Web技术，或者可能需要用户具有特定的辅助技术和／或浏览器才能从辅助功能中受益。

这些目标对 WCAG 2.1 的结构有显著的影响。

>[!NOTE]
>
>创建出满足各种残障人士或各种类型人员的网站几乎是不可能的。WCAG 2.1 旨在帮助 Web 作者尽可能创建能够在特定条件和合理范围内能进行访问的站点。

## 结构 {#structure}

在构建 WCAG 2.1 时引入了以逐步细化的方式引创建易访问 Web 内容的概念。这可能给人们留下这样的印象，即 WCAG 2.1 是一组非常复杂的相互关联的文档，但其目标是，在作者需要时（逐步）提供更详细的信息，而不是在一个非常大的文档中提供所有信息。

WCAG 2.1 包含有四个用于辅助设计的关键原则，有时由首字母缩写 **POUR** 表示。这四个关键原则分别是：

1. **可感知**：用户能否感知到相关 Web 内容？
1. **可操作**：用户能否导航、输入数据或与 Web 内容进行交互？
1. **可理解**：用户能否处理并理解呈现给他们的 Web 内容？
1. **强健**：Web 内容是否可以按预期方式在各种浏览环境（包括旧版和新兴的浏览环境）中可用？

详细说明：
* 每个&#x200B;**原则**&#x200B;都包括一个或多个&#x200B;**准则**。

* 准则的措辞为说明性文字，内容分为正面（请...）或负面（请不要...）。
* 准则编号为 1.1 - 4.1，其中第一个编号与父准则相对应。
* 每个准则都包含一个或多个&#x200B;**成功标准**。
* 成功标准将编写为语句，任何给定网页的结果都为 `True` 或 `False`。
* 成功标准可能包括其中一项/或多种选项，也可能包括例外，即不符合成功标准的情况。
* 成功标准按照父准则和原则编号，从 1.1.1 - 4.1.1。它们还有一个简短的名称，用于总结标准的目的，以便于参考。For example, success criterion [1.1.1 is Non-text Content](https://www.w3.org/TR/WCAG/#non-text-content).
* 成功标准包括一系列相关的&#x200B;**技术**（详见下文）。

## 支持资源 {#supporting-resources}

除了原则、准则和成功标准的核心 WCAG 2.1 组成部分外，还有一系列支持文档。其中一些文档就如何符合准则的某些方面提供了具体建议，而另一些文档则是一般性参考资料，可帮助拥有各种能力的 Web 作者、设计人员和开发人员尽可能有效地理解和使用 WCAG 2.1。

虽然WCAG 2.1本身是稳定的文档，不会改变，但这些支持资源大多是动态文档; 随着新技术的出现，它们会随着时间的推移而改变和增长，并会发现如何实现web辅助功能的新示例。

### WCAG 2.1 资源 {#wcag-resources}

本列表并非详尽内容，它介绍了一些可用资源：
* [所有 WCAG 相关文档的概要](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [不同文档的概要](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Web 内容辅助功能准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [WCAG 2.1 的新增内容](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [如何满足 WCAG 2.1 的快速参考指南](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2 常见问题解答](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### WCAG 2.1 的新增内容 {#what-is-new}

这些准则提供了有关WCAG 2.1中新增功能的信息：

* [WCAG 2.1中的新增功能提供](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) 有关WCAG 2.0和WCAG 2.1之间增量的重要信息。

* [WCAG 2.0 和 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) 节进一步阐明了两者的关系状况。

### 用于 WCAG 2.1 的技术 {#techniques-for-wcag}

用于 WCAG 2.1 的技术可在[用于 WCAG 2.1 的技术](https://www.w3.org/WAI/WCAG21/Techniques/)页面上找到。

**技术**&#x200B;构成了 WCAG 2.1 层次结构中成功标准以下的级别。WAI 将这些技术划分信息类，而非规范类。换句话说，为了使资源符合 WCAG 2.1，不必拘泥于使用某些特定技术。

由于技术比成功标准更具体，它们通常指特定的技术或内容类型（例如 HTML 或视频）或情况（例如电子商务或电子教学应用程序）。您可以将技术视为如何满足特定准则和成功标准的已验证示例，因此这些技术对于在特定环境工作的作者和开发人员很有帮助。

技术的访问方式可包括：

* 通过收藏集（技术可能是一般性内容，也可能与特定技术或格式相关 - 例如 HTML、CSS 或客户端脚本），或
* 通过相关的成功标准。技术可应用于多个成功标准。

每种技术都有一个与其收藏集相关的唯一编号。For example, one of the ARIA techniques is [Technique ARIA2: Identifying a required field with the aria-required property](https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA2.html).

技术可分为“充分”、“建议”或“失败”：

* 对于&#x200B;*充分技术*，如果遵循，则足以满足特定的成功标准。
* 对于&#x200B;*建议技术*，如果遵循，则将对辅助功能产生积极影响，但它自己可能不足以确保满足特定成功标准。
* *失败*&#x200B;技术用于描述不满足成功标准的具体示例。

技术的详细信息包括说明、适用性、示例、获取更多信息的资源以及作者如何测试该技术是否成功应用的详细信息。

技术列表并不完善，WAI 正不断用新的示例更新列表，以体现 Web 技术、设计方法和研究成果的发展。因此，请务必定期查看技术列表以了解新增内容。

### 了解 WCAG 2.1 {#understanding-wcag}

WCAG 2.1 是指一系列文档，它提供了一些建议可帮助读者理解具体准则和成功标准的目的。您可以[下载简介，以及指向更详细信息的链接](https://www.w3.org/WAI/WCAG21/Understanding/)。

每一个准则和成功标准都有其自己的“了解”页面，其中提供有关以下项的信息：

* 准则的目的；
* 具体成功标准；
* 建议技术，可帮助满足准则的要求，但不属于任何特定成功标准。

每个成功标准的单独“了解”页面提供有关以下项的信息：

* 成功标准的目的；
* 如何满足成功标准的一般示例；
* 有关如何满足成功标准的相关（非 W3C）资源；
* 技术与失败：如何满足成功标准的具体详细示例（详见下文）
* 关键术语 - 理解成功标准的重要术语的术语表。

示例可在[了解成功标准 1.1.1（“非文本内容”）](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content)中找到。

### 如何满足 WCAG 2.1 {#how-to-meet-wcag}

“如何满足”部分显示在[如何满足 WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) 页面上。本节提供WCAG的替代演示，使读者能够将指南的内容调整为与他们自己的兴趣和／或情况最相关的内容。 读者可以通过指定特定 Web 内容技术（如层叠样式表或脚本）或指定特定优先级来筛选他们希望查看的成功标准技术。

如果不进行筛选，此资源将提供按准则分组的所有成功标准。对于每个成功标准，提供以下内容：

* 成功标准的文本；
* 指向相应“了解”文档的链接；
* 链接到每种技术详细信息的“充分技术”相关列表；
* 链接到每种技术详细信息（如果存在）的“建议技术”相关列表；
* 链接到每种失败详细信息的失败相关列表。
