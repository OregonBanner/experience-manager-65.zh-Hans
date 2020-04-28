---
title: HTML5表单的最佳实践
seo-title: HTML5表单的最佳实践
description: 调整基于XFA的HTML5表单以获得最佳性能。
seo-description: 了解如何调整基于XFA的HTML5表单以获得最佳性能。
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: b6c013a31b70166cba80fea53dffc3794ffee5b8

---


# Best practices for HTML5 forms{#best-practices-for-html-forms}

## 概述 {#overview}

AEM Forms有一个称为HTML5表单的组件。 它有助于以HTML5格式呈现现有的基于XFA的PDF表单（XDP文件）。 本文档提供了减少加载时间并改进移动设备上HTML5表单性能的指南和建议。

大多数移动设备的处理能力和内存能力都有限。 它有助于缩短移动设备的待机时间。 在移动设备上运行的Web浏览器可以访问有限的资源（有限的内存和处理功能）。 达到限制后，浏览器行为将变慢。 此文档提供了一些建议，可使HTML5表单的大小保持不变。 较小的表单不会违反设备的内存和处理能力限制并提供流畅的体验。

尽管本文讨论的建议针对HTML5表单，但这些建议同样适用于基于XFA的PDF表单。 这些最佳做法集中有助于HTML5表单的整体性能。 它需要仔细规划，以开发高效、高效的表单。 让我们开始：

## 节点是HTML5表单的货币，明智地使用它们 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表单包含多个元素。 例如，表、文本字段和图像。 每个元素都有许多用于控制元素行为和外观的属性。 当XFA表单以HTML5格式呈现时，所有XFA元素和相应的属性都将转换为“模型”或“HTML DOM”节点。 这些节点增加了DOM的大小和复杂性。 使HTML5表单的渲染速度变慢。

浏览器更容易呈现更精简的DOM。 因此，您可以对XFA表单执行以下优化以减少节点数。 因此，生成一个精简的DOM结构：

* 使用题注属性向字段添加标签。 请勿使用单独的“文本”元素添加标签。 它有助于减少额外的权重，从而提高性能。 它还有助于避免布局问题。
* 将表单上的“绘制”文本元素数量保持最少。 绘制元素有助于提高可读性和外观，但没有任何信息存储功能。 建议将多个Draw文本元素合并到单个Draw文本元素中。 不要让石头掉下来，让表单变得更简洁。

## Lite表单性能更好，资源保持压缩 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表单可以包含多个外部资源，如图像、JavaScript和CSS文件。 每次浏览器请求表单时，外部资源都会通过网络发送。 通过网络传输所需的时间与文件的大小成正比。

因此，减少外部资源的大小并且只使用绝对必需的资源是改进表单性能的优选方法。 您可以对XFA表单执行以下优化以减小表单的外部资源的大小：

* 使用 [压缩图像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)。 它减少了呈现表单所需的网络活动和内存量。 因此，形状加载时间基本上减少。
* 使用AEM Configuration Manager(Day CQ HTML Library Manager)中的minify选项压缩JavaScript和CSS文件。 有关详细信息，请参 [阅OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。
* 启用Web压缩。 它可减小源自表单的请求和响应的大小。 有关详细信息，请参 [阅AEM表单服务器的性能调整](https://helpx.adobe.com/cn/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持兴趣，仅显示必填字段 {#keep-the-interest-alive-show-only-required-fields}

HTML5表单可以运行到数百个页面中。 具有大量字段的表单在浏览器中加载速度较慢。 您可以对XFA表单执行以下优化，以优化具有大量字段和页面的表单：

* 评估如何将大型表单拆分为多个表单。 您还可以使用表单集将所有较小的表单组合在一起，并将它们作为一个单元显示。 表单集仅加载所需的表单。 此外，在表单集中，您可以配置不同表单中的公用字段以共享数据绑定。 数据绑定帮助用户只填写一次公共信息；这些信息会在后续表单中自动填写，从而大幅改善性能。 有关表单集的详细信息，请参 [阅AEM表单中的表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。
* 请考虑拆分部分并将每个部分移至不同的页面。 HTML5表单在页面滚动请求时动态加载每页。 只有滚动的页面（显示的页面及其前面的页面）存储在内存中；其余的页面按需加载。 因此，拆分和移动页面上的某个部分可以减少加载表单所需的时间。 您还可以使用表单的第一页作为登陆页。 它类似于书籍的目录(TOC)。 表单的登陆页仅包含指向表单其他部分的链接。 它显着缩短了表单第一页的加载时间，并改善了用户体验。
* 默认情况下，将条件部分保持隐藏。 只有在满足特定条件时，才能显示这些部分。 它有助于将DOM的大小保持在最小。 您还可以使用选项卡式导航一次仅显示一个节。

## 少就是多，减少页数 {#less-is-more-reduce-the-number-of-pages}

HTML5表单可以包含数据驱动字段（表和子表单）。 这些字段会在运行时扩展表单的大小。 例如，HTML5表单中的数据驱动表可以跨成千行。 此类表可能导致布局和性能降级。 下面建议的优化可以帮助您减少具有数据驱动字段的HTML5表单的加载时间：

* 使用XFA脚本实现分页导航以显示数据驱动的字段（表和子表单）。 在分页导航中，页面上仅显示特定数据。 它将浏览器绘画操作限制为一次显示的字段，并使表单导航更简单。 此外，移动设备上的用户只对数据子集感兴趣。 它可以帮助您提供出色的用户体验并减少加载所需数据所需的时间。 您只需购买一个，即可获得两种解决方案。  另请注意，分页导航功能不可用。 您可以使用XFA脚本开发分页导航。

* 评估将多个只读列合并为一列。 它减少了显示表单所需的内存。 另外，避免显示不需要用户输入的列。
* 如果上述建议没有带来许多改进，请 [评估将数据驱动的表单拆分为表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果一个表格的行数超过1000，则每100行将一次移动到其他表单。 它有助于提高表单的加载时间和性能。  另请注意，表单集会为所有表单生成一个统一的提交XML。 要区分每种形式的数据，请使用不同的数据根。 有关详细信息，请参 [阅AEM Forms中的表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。

## 记录文档(DOR)的2的强大功能 {#power-of-two-for-document-of-record-dor}

XFA表单可以具有大量专用于记录文档(DOR)的部分。 要减少节点数并改进此类表单的性能，您可以维护表单的不同副本——一个用于填写表单的副本，另一个用于在服务器上生成记录文档。 在填写XFA表单的副本中，显示仅捕获数据所需的字段。 在“记录XFA”的生成文档中，仅在表单的打印输出中保留必填字段。 在选择所建议的方法之前，评估性能增益和维护开销。

## 建议的读取数 {#recommended-reads}

Adobe Experience Manager(AEM)表单可以帮助您将复杂的交易转变为简单、愉悦的数字体验。 但是，它需要共同努力，以开发高效和富有成效的表单。 除HTML5表单外，以下是一些建议的读取内容，用于了解一般AEM最佳实践：

* [部署和维护AEM的最佳实践](/help/sites-deploying/best-practices.md)
* [创作内容的最佳实践](/help/sites-authoring/best-practices.md)
* [管理 AEM 的最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发解决方案的最佳实践](/help/sites-developing/best-practices.md)
* [使用自适应表单的最佳实践](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms服务器不将字体嵌入到动态PDF表单](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速参考卡 {#quick-reference-card}

您可以打印以下卡（单击卡下载高分辨率版本）并将其放在办公桌上以供快速参考：[![HTML5 Forms最佳实践快速参考卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
