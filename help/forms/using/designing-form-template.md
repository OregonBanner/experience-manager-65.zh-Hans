---
title: 为HTML5表单设计表单模板
description: AEM Forms可以将XFA表单模板渲染为HTML5格式。 窗体设计人员可以使用Designer设计窗体HTML并使用Template5呈现功能。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 为HTML5表单设计表单模板{#designing-form-templates-for-html-forms}

AEM中的HTML5表单组件可以将XFA表单模板渲染为HTML5格式。 窗体设计人员可以使用来设计窗体模板 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) 并使用HTML5呈现版本功能。 这些表单模板及其资源可以驻留在AEM存储库、文件系统中，或通过http公开。 但是，如果您计划使用Forms Manager管理表单，则模板和资源应驻留在AEM存储库中。

虽然HTML5表单在很大程度上与PDF forms的行为相匹配，但两种格式都存在一些不适用于其他格式的特征。 例如，Adobe Reader中对PDF表单应用条形码的方式因移动设备表单而异，表单的数字签名方式也因格式而异。 有关此类变体的更多信息，请参阅 [HTML5表单与PDF forms之间的功能区别](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

有关常见的XFA功能，请参阅以下最佳实践和指南，以设计可同时满足两种格式的表单。

## 最佳实践 {#best-practices}

设计表单模板的大多数步骤（如架构绑定或编写表单逻辑）都是相同的。 但是，由于Adobe Reader等胖客户端的渲染引擎与基于浏览器的表单的脚本引擎之间存在固有差异，因此中介绍了一些建议 [最佳实践](/help/forms/using/design-accessible-html5-forms.md) 文章。 这些最佳实践可帮助您设计两种格式的表单模板，使其按预期工作。

### 适用于HTML5 Forms的AEM Forms Designer中的功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 预览HTML {#preview-html}

在“设计”模式下会添加“预览HTML”选项卡，以供表单设计人员在设计过程中以HTML5格式预览表单。 有关如何在AEM Forms Designer中启用和配置此功能的更多信息，请参阅 [预览HTML](../../forms/using/preview-xdp-forms-html.md).

#### 连笔签名 {#scribble-signature}

HTML5表单的主要目标是触摸设备。 因此，在AEM Forms Designer中添加了新的涂写签名控件。 您可以单击或拖放表单模板上的涂写签名控件并对其进行配置。 它在HTML5呈现中呈现为涂写字段，并且可用于在触摸设备上涂写签名。 在桌面计算机上，它可用作使用鼠标控制的涂写字段。 有关如何使用此功能的详细信息，请参阅 [XFA涂写字段](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### 富文本格式 {#rich-text-format}

您可以将文本字段转换为富文本字段。 它向文本字段添加一个格式设置选项列表。 要进行转换，请打开Forms Designer，选择中的文本字段 **[!UICONTROL 设计视图]**. 在 **[!UICONTROL 字段]** 选项卡，选择 **[!UICONTROL 富文本]** 从 **[!UICONTROL 字段格式]** 下拉列表。 现在，当XFA表单呈现为HTML5表单时，该字段呈现为富文本字段。 选择 ![最大化](assets/maximize_icon.svg) 查看其他格式选项。
