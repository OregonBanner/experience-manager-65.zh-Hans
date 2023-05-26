---
title: 为HTML5表单设计表单模板
seo-title: Designing form templates for HTML5 forms
description: AEM Forms提供将XFA表单模板渲染为HTML5格式。 窗体设计人员可以使用Designer设计窗体HTML并使用Template5呈现功能。
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# 为HTML5表单设计表单模板{#designing-form-templates-for-html-forms}

AEM中的HTML5表单组件提供将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用以下工具设计表单模板 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63_cn) 和使用HTML5呈现版本功能。 这些表单模板及其资产可以驻留在AEM存储库、文件系统中，或通过http公开。 但是，如果您计划使用Forms Manager管理表单，则模板和资产应驻留在AEM存储库中。

虽然HTML5表单在很大程度上与PDF forms的行为相匹配，但两种格式都存在一些不适用于其他格式的特征。 例如，Adobe Reader中对PDF表单应用条形码的方式与移动设备表单有所不同，表单的数字签名方式也因格式而异。 有关此类变体的更多信息，请参阅 [HTML5表单和PDF forms之间的功能区别](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

有关常见XFA功能，请参阅以下最佳实践和准则来设计可同时用于两种格式的表单。

## 最佳实践 {#best-practices}

设计表单模板的大多数步骤（如架构绑定或编写表单逻辑）都是相同的。 但是，由于大型客户端(如Adobe Reader)的渲染引擎和脚本编写引擎与基于浏览器的表单存在固有差异，因此中介绍了一些建议 [最佳实践](/help/forms/using/design-accessible-html5-forms.md) 文章。 这些最佳实践可帮助您设计可在两种格式中按预期使用的表单模板。

### 适用于HTML5 Forms的AEM Forms Designer中的功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 预览HTML {#preview-html}

“预览HTML”选项卡会添加到“设计”模式中，以供表单设计者在设计过程中以HTML5格式预览表单。 有关如何在AEM Forms Designer中启用和配置此功能的详细信息，请参阅 [预览HTML](../../forms/using/preview-xdp-forms-html.md).

#### 连笔签名 {#scribble-signature}

HTML5表单的主要目标是触摸设备。 因此，在AEM Forms Designer中添加了新的涂写签名控件。 您可以单击或拖放表单模板上的涂写签名控件并对其进行配置。 它在HTML5呈现中呈现为涂写字段，可用于在触控设备上涂写签名。 在桌面计算机上，它可以使用鼠标控制作为涂写字段。 有关如何使用此功能的更多信息，请参阅 [XFA涂写字段](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### 富文本格式 {#rich-text-format}

您可以将文本字段转换为富文本字段。 它向文本字段添加一个格式设置选项列表。 要转换，请打开Forms Designer，点按中的文本字段 **[!UICONTROL 设计视图]**. 在 **[!UICONTROL 字段]** 选项卡，选择 **[!UICONTROL 富文本]** 从 **[!UICONTROL 字段格式]** 下拉列表。 现在，当XFA表单呈现为HTML5表单时，该字段呈现为富文本字段。 点按 ![最大化](assets/maximize_icon.svg) 查看其他格式选项。
