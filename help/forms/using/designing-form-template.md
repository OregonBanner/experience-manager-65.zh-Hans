---
title: 为HTML5表单设计表单模板
seo-title: 为HTML5表单设计表单模板
description: AEM Forms优惠将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用设计人员设计表单模板，并使用HTML5再现功能。
seo-description: AEM Forms优惠将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用设计人员设计表单模板，并使用HTML5再现功能。
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 为HTML5表单设计表单模板{#designing-form-templates-for-html-forms}

AEM优惠中的HTML5表单组件将XFA表单模板渲染为HTML5格式。 表单设计人员可以使用 [Forms Designer设计表单模板](https://www.adobe.com/go/learn_aemforms_designer_63) ，并使用HTML5再现功能。 这些表单模板及其资产可以驻留在AEM存储库、文件系统中，或通过http公开。 但是，如果您计划使用Forms Manager管理表单，则模板和资产应驻留在AEM存储库中。

尽管HTML5表单在很大程度上与PDF表单的行为匹配，但两种格式中有一些功能不适用于其他格式。 例如，Adobe Reader中PDF表单上的条形码应用方式因移动表单而异，或表单的数字签名方式也因格式而异。 有关这些变体的详细信息，请参 [阅HTML5表单与PDF表单功能区分](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

有关常见的XFA功能，请参阅以下设计两种格式均可用的表单的最佳实践和准则。

## Best practices {#best-practices}

设计表单模板(如模式绑定或编写表单逻辑)的大多数步骤都是相同的。 但是，由于Adobe Reader等粗客户端的渲染和脚本引擎与基于浏览器的表单之间的内在差异，最佳实践文章中介绍了一些 [建议](/help/forms/using/design-accessible-html5-forms.md) 。 这些最佳实践可帮助您设计表单模板，使其在两种格式中均能正常工作。

### AEM Forms Designer for HTML5 Forms中的功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 预览HTML {#preview-html}

预览HTML选项卡在设计过程中添加在“设计”模式中，以使表单设计人员在设计过程中预览HTML5格式的表单。 有关如何在AEM Forms Designer中启用和配置此功能的详细信息，请参阅 [预览HTML](../../forms/using/preview-xdp-forms-html.md)。

#### 连笔签名 {#scribble-signature}

HTML5表单的关键目标是触控设备。 因此，AEM Forms Designer中新增了一个涂抹签名控件。 您可以单击或拖放表单模板上的涂鸦式签名控件并对其进行配置。 它在HTML5再现中呈现为涂抹字段，可用于在触控设备上涂抹签名。 在台式机器上，可以使用鼠标控制将其用作涂抹字段。 有关如何使用此功能的详细信息，请参阅 [XFA涂抹字段](../../forms/using/scribble-signature.md)。

![4](assets/4.png)

#### Rich text format {#rich-text-format}

您可以将文本字段转换为富文本字段。 它向文本字段添加一列表格式选项。 要进行转换，请打开表单设计器，点按设计视图中的文 **[!UICONTROL 本字段]**。 在“字 **[!UICONTROL 段]** ”选项卡中，从“字段格式”下拉 **[!UICONTROL 列表中选]** 择“富文本 **** ”。 现在，当XFA表单呈现为HTML5表单时，该字段将呈现为富文本字段。 点按最 ![大化](assets/maximize_icon.svg) ，以视图其他格式选项。
