---
title: 自适应表单中的分隔符组件
seo-title: Separator component in adaptive forms
description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---

# 自适应表单中的分隔符组件{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

您可以使用分隔符组件以可视方式分隔表单的面板。 通过指定分隔符组件的以下属性，可以定义分隔符组件的整体外观和样式：

* **元素名称：** 指定组件的名称。 SOM表达式使用在元素名称字段中指定的值寻址组件。
* **粗细：** 指定分隔符组件的粗细（以像素为单位）。

* **CSS类：** 指定分隔符组件的自定义CSS类

* **内联样式：** 借助AEM Forms，您现在可以将内联CSS样式应用于各个自适应表单组件并实时预览更改。

您可以使用布局模式定义分隔符组件跨越的列数。 有关更多信息，请参阅 [使用布局模式调整组件大小](../../forms/using/resize-using-layout-mode.md).

要指定分隔符组件的属性，请执行以下操作：

1. 选择分隔符组件并点按 ![cmppr](assets/cmppr.png). 属性在侧栏中打开。
1. 单击“内联CSS属性”部分中的选项卡可指定CSS属性。 例如：a。在字段选项卡中，单击 **添加项目**. 将添加包含两个字段的行。
1. 在左侧的第一个字段中，指定要应用的CSS3属性。 例如， **边框**. 您还可以通过单击向下箭头按钮选择属性。 下拉列表并非详尽无遗，您可以在此字段中指定任何支持的CSS3属性名称。
1. 在相邻的字段中，为指定的CSS3属性指定有效值。 例如， **3px实心黑色**.
1. 单击 **添加项目** 以指定另一个属性及其值。
1. 单击 **预览** 以预览表单中的更改。
1. 单击 **确定** 确认更改或 **取消** 退出对话框而不进行任何更改。
