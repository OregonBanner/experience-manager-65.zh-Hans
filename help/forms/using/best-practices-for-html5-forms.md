---
title: HTML5表单的最佳实践
seo-title: HTML5表单的最佳实践
description: 调整基于XFA的HTML5 Forms以获得最佳性能。
seo-description: 了解如何调整基于XFA的HTML5 Forms以获得最佳性能。
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: 移动设备表单
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 1%

---


# HTML5表单的最佳实践{#best-practices-for-html-forms}

## 概述 {#overview}

AEM Forms有一个称为HTML5表单的组件。 它有助于以HTML5格式呈现现有的基于XFA的PDF forms（XDP文件）。 此文档提供了相关指导和建议，可缩短加载时间并改进HTML5表单在移动设备上的性能。

大多数移动设备的处理能力和内存能力都有限。 它有助于提高移动设备的待机时间。 在移动设备上运行的Web浏览器对有限的资源（有限的内存和处理能力）具有访问权限。 达到限制后，浏览器行为将变得迟钝。 此文档提供了一些建议，以保持HTML5表单的大小受到控制。 较小的表单不会违反设备的内存和处理能力限制，并提供流畅的体验。

尽管本文中讨论的建议针对HTML5表单，但这些建议同样适用于基于XFA的PDF forms。 这些最佳实践共同有助于提高HTML5表单的整体性能。 它需要仔细规划，以开发高效、高效的表单。 让我们开始：

## 节点是HTML5表单的货币，明智地使用{#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表单包含多个元素。 例如，表、文本字段和图像。 每个元素都具有许多属性来控制元素的行为和外观。 当XFA表单以HTML5格式呈现时，所有XFA元素和相应属性都将转换为Model或HTML DOM节点。 这些节点增加了DOM的大小和复杂性。 使HTML5表单的渲染速度变慢。

浏览器可以更轻松地渲染更精简的DOM。 因此，您可以对XFA表单执行以下优化以减少节点数。 因此，生成一个精益DOM结构：

* 使用题注属性向字段添加标签。 请勿使用单独的Text元素添加标签。 它有助于减少额外权重，从而提高性能。 它还有助于避免布局问题。
* 将表单上“绘制”文本元素的数量保持最小。 绘制元素有助于提高可读性和外观，但没有任何信息存储功能。 建议将多个Draw文本元素合并为一个Draw文本元素。 不要掉石头，让形体更瘦。

## 精简表单的性能更好，保持压缩的资源{#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表单可包含多个外部资源，如图像、JavaScript和CSS文件。 每次浏览器请求表单时，外部资源都会通过网络发送。 通过网络传输所需的时间与文件的大小成正比。

因此，减少外部资源的规模并仅使用绝对需要的资源是改进表单性能的首选方法。 您可以对XFA表单执行以下优化以减小表单的外部资源大小：

* 使用[压缩图像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)。 它减少了呈现表单所需的网络活动和内存量。 因此，形状加载时间显着减少。
* 使用AEM Configuration Manager(Day CQ HTML Library Manager)中的minify选项压缩JavaScript和CSS文件。 有关详细信息，请参阅[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。
* 启用Web压缩。 它可减小源自表单的请求和响应的大小。 有关详细信息，请参阅[AEM forms server的性能调整](https://helpx.adobe.com/cn/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持兴趣，仅显示必填字段{#keep-the-interest-alive-show-only-required-fields}

HTML5表单可以运行到数百个页面中。 具有大量字段的表单在浏览器中加载速度较慢。 您可以对XFA表单执行以下优化，以使用大量字段和页面优化表单：

* 评估将大型表单拆分为多个表单。 您还可以使用表单集将所有较小的表单组合在一起，并以单个单位形式显示。 表单集仅加载所需的表单。 此外，在表单集中，您可以配置不同表单中的常用字段以共享数据绑定。 数据绑定只帮助用户填写一次公共信息；信息会在后续表单中自动填写，从而大幅改善性能。 有关表单集的详细信息，请参阅AEM表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。[
* 请考虑拆分部分并将每个部分移动到不同的页面。 HTML5表单在页面滚动请求时动态加载每页。 只有滚动的页面（显示的页面及其前面的页面）存储在内存中；其余页面按需加载。 因此，拆分和移动页面上的某个部分可减少加载表单所需的时间。 您还可以使用表单的第一页作为登陆页。 它类似于书籍的目录(TOC)。 表单的登陆页只包含指向表单其他部分的链接。 它显着缩短了表单第一页的加载时间，并改善了用户体验。
* 默认情况下，保持条件节隐藏。 仅当满足特定条件时，才使这些部分可见。 它有助于将DOM的大小保持在最小。 您还可以使用选项卡式导航一次仅显示一个截面。

## “少”即“多”，减少页数{#less-is-more-reduce-the-number-of-pages}

HTML5表单可以包含数据驱动字段（表和子表单）。 这些字段会在运行时扩展表单的大小。 例如，HTML5表单中的数据驱动表可以跨成千行。 此类表可能导致布局和性能降级。 下面建议的优化可以帮助您使用数据驱动字段缩短HTML5表单的加载时间：

* 使用XFA脚本实现分页导航以显示数据驱动字段（表和子表单）。 在分页导航中，页面上仅显示特定数据。 它将浏览器绘画操作限制为一次显示的字段，并使表单的导航更轻松。 此外，移动设备上的用户只对数据子集感兴趣。 它可以帮助您提供出色的用户体验并减少加载所需数据所需的时间。 您只需购买一个解决方案即可获得两种解决方案。  另请注意，分页导航不是开箱即用的。 您可以使用XFA脚本开发分页导航。

* 评估将多个只读列合并为单个列。 它减少了显示表单所需的内存。 另外，避免显示不需要用户输入的列。
* 如果上述建议没有带来许多改进，请评估将数据驱动表单拆分为[表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果一个表的行数超过1000，则每100行将一行移动到另一个表单。 它有助于改善表单的加载时间和性能。  另请注意，表单集会为所有表单生成一个统一的提交XML。 要区分每种形式的数据，请使用不同的数据根。 有关详细信息，请参阅AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)中的[表单集。

## 二的幂用于记录文档(DOR){#power-of-two-for-document-of-record-dor}

XFA表单可以包含大量专用于记录文档(DOR)的部分。 要减少节点数并提高此类表单的性能，您可以保留表单的不同副本 — 一个用于填写表单的副本，另一个用于在服务器上生成记录文档。 在填写XFA表单的副本中，显示仅捕获数据所需的字段。 在“记录XFA自”的生成文档中，仅在表单的打印输出中保留必填字段。 在选择所建议的方法之前，对性能增益和维护开销进行评估。

## 建议的读取数{#recommended-reads}

Adobe Experience Manager(AEM)表单可以帮助您将复杂的事务转化为简单愉悦的数字体验。 然而，它需要共同努力，发展高效和富有成效的形式。 除HTML5 Forms外，以下是一般AEM最佳实践的推荐读取内容：

* [部署和维护AEM的最佳实践](/help/sites-deploying/best-practices.md)
* [创作内容的最佳实践](/help/sites-authoring/best-practices.md)
* [管理 AEM 的最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发解决方案的最佳实践](/help/sites-developing/best-practices.md)
* [使用自适应表单的最佳实践](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms服务器不将字体嵌入动态PDF表单](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速参考卡{#quick-reference-card}

您可以打印下列信息卡（单击信息卡可下载高分辨率版本），并将其保留在办公桌上以供快速参考：
[ ![HTML5 Forms最佳做法快速参考卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
