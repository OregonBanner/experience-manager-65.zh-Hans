---
title: HTML5表单的最佳实践
seo-title: HTML5表单的最佳实践
description: 优化基于XFA的HTML5 Forms，以获得最佳性能。
seo-description: 了解如何优化基于XFA的HTML5 Forms，以获得最佳性能。
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: 移动设备表单
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 1%

---

# HTML5表单的最佳实践{#best-practices-for-html-forms}

## 概述 {#overview}

AEM Forms有一个名为HTML5表单的组件。 它有助于以HTML5格式呈现现有的基于XFA的PDF forms（XDP文件）。 本文档提供了减少加载时间并提高移动设备上HTML5表单性能的准则和建议。

大多数移动设备的处理能力和内存能力都有限。 它有助于提高移动设备的待机时间。 在移动设备上运行的Web浏览器有权访问有限的资源（有限的内存和处理能力）。 达到限制后，浏览器行为变得缓慢。 本文档提供了一些建议，以保持HTML5表单的大小处于可控状态。 较小型号不会违反设备的内存和处理能力限制，并提供流畅的体验。

尽管如此，本文中讨论的建议将针对HTML5表单，但这些建议同样适用于基于XFA的PDF forms。 这些最佳实践会共同影响HTML5表单的整体性能。 它需要仔细规划，以开发高效和高效的形式。 我们开始吧：

## 节点是HTML5表单的货币，明智地使用它们{#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表单具有多个元素。 例如，表、文本字段和图像。 每个元素都具有许多用于控制元素行为和外观的属性。 当XFA表单以HTML5格式呈现时，所有XFA元素和相应属性都将转换为模型或HTML DOM节点。 这些节点增加了DOM的大小和复杂性。 使HTML5表单呈现缓慢。

浏览器更容易渲染更精简的DOM。 因此，您可以对XFA表单执行以下优化，以减少节点数。 因此，请生成精益DOM结构：

* 使用标题属性向字段添加标签。 请勿使用单独的文本元素添加标签。 它有助于减轻额外的重量，从而提高性能。 它还有助于避免布局问题。
* 尽量减少表单上绘制文本元素的数量。 绘制元素有助于提高可读性和外观，但没有任何信息存储功能。 建议将多个绘制文本元素合并到一个绘制文本元素中。 不要翻石，让形体更瘦。

## Lite表单性能更好，保持压缩的资源{#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表单可以包含多个外部资源，如图像、JavaScript和CSS文件。 每次浏览器请求表单时，外部资源都会通过网络发送。 通过网络传输所需的时间与文件的大小成正比。

因此，减少外部资源的大小并仅使用绝对需要的资源是改进表单性能的首选方法。 您可以对XFA表单执行以下优化，以减小表单的外部资源大小：

* 使用[压缩图像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)。 它减少了呈现表单所需的网络活动和内存量。 因此，形式加载时间基本上减少。
* 使用AEM Configuration Manager（Day CQ HTML库管理器）中的缩小选项来压缩JavaScript和CSS文件。 有关详细信息，请参阅[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。
* 启用Web压缩。 它可减小源自表单的请求和响应的大小。 有关详细信息，请参阅[AEM Forms服务器的性能优化](https://helpx.adobe.com/cn/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持兴趣有效，仅显示必填字段{#keep-the-interest-alive-show-only-required-fields}

HTML5表单可以包含数百个页面。 在浏览器中加载具有大量字段的表单速度较慢。 您可以对XFA表单执行以下优化，以通过大量字段和页面优化表单：

* 评估将大型表单拆分为多个表单的情况。 您还可以使用表单集将所有较小的表单分组在一起，并以单个单位显示它们。 表单集仅加载所需的表单。 此外，在表单集中，您可以配置不同表单中的常用字段以共享数据绑定。 数据绑定帮助用户仅填写一次常见信息；这些信息会在后续表单中自动填充，从而大幅提升性能。 有关表单集的更多详细信息，请参阅AEM表单中的[表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。
* 请考虑拆分各个部分，并将每个部分移动到不同的页面。 在页面滚动请求中，HTML5表单会动态加载每个页面。 只有滚动页面（显示的页面及其前面的页面）存储在内存中；其余的页面会按需加载。 因此，在页面上拆分和移动某个部分会减少加载表单所需的时间。 您还可以将表单的第一页用作登陆页面。 它类似于书籍目录(TOC)。 表单的登陆页面只包含指向表单其他部分的链接。 它显着缩短了表单首页的加载时间，并改善了用户体验。
* 默认情况下，将条件部分保持隐藏状态。 仅当满足特定条件时，才可显示这些部分。 它有助于将DOM的大小保持在最小。 您还可以使用选项卡式导航一次只显示一个截面。

## 越少越多，减少页数{#less-is-more-reduce-the-number-of-pages}

HTML5表单可以包含数据驱动字段（表和子表单）。 这些字段会在运行时展开表单的大小。 例如，HTML5表单中的数据驱动表可以跨越数千行。 此类表可能导致布局和性能下降。 下面建议的优化内容可帮助您减少具有数据驱动字段的HTML5表单的加载时间：

* 使用XFA脚本实现分页导航，以显示数据驱动字段（表和子表单）。 在分页导航中，页面上只显示特定数据。 它将浏览器绘画操作限制为一次显示的字段，并且更便于导航表单。 此外，移动设备上的用户只对数据子集感兴趣。 它有助于您提供出色的用户体验，并减少加载所需数据所需的时间。 你只要买一个，就能得到两个解决方案。  另请注意，页面导航功能不是开箱即用的。 您可以使用XFA脚本开发分页导航。

* 评估将多个只读列合并到单个列中的情况。 它减少了显示表单所需的内存。 此外，还应避免显示不需要用户任何输入的列。
* 如果上述建议没有带来多项改进，请评估将数据驱动表单拆分为[表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果一个表的行数超过1000，则每100行将一个表格移动到其他表格。 这将有助于提高表单的加载时间和性能。  另请注意，表单集为所有表单生成统一的提交XML。 要区分每种形式的数据，请使用不同的数据根。 有关更多信息，请参阅AEM Forms中的[表单集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。

## 记录文档(DOR){#power-of-two-for-document-of-record-dor}的二次幂

XFA表单可以具有大量专用于记录文档(DOR)的部分。 为了减少节点数并提高此类表单的性能，您可以维护表单的不同副本 — 一个用于填写表单的副本，另一个用于在服务器上生成记录文档。 在填写XFA表单的副本中，显示仅捕获数据所需的字段。 在生成XFA记录文档中，仅在表单的打印输出中保留必填字段。 在选择建议的方法之前，先评估性能增益和维护开销。

## 建议读取{#recommended-reads}

Adobe Experience Manager(AEM)表单可帮助您将复杂的事务转换为简单、令人愉快的数字体验。 但是，需要协调一致地努力发展高效和生产性形式。 除了HTML5 Forms之外，以下是一般AEM最佳实践的推荐读取内容：

* [部署和维护AEM的最佳实践](/help/sites-deploying/best-practices.md)
* [内容创作最佳实践](/help/sites-authoring/best-practices.md)
* [管理 AEM 的最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发解决方案的最佳实践](/help/sites-developing/best-practices.md)
* [使用自适应表单的最佳实践](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms服务器未将字体嵌入到动态PDF表单](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速参考卡{#quick-reference-card}

您可以打印下列信息卡（单击信息卡可下载高分辨率版本），并将其保留在您的办公桌上以供快速参考：
[ ![HTML5 Forms最佳实践快速参考卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
