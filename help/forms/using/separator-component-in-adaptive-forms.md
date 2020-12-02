---
title: 自适应表单中的分隔符组件
seo-title: 自适应表单中的分隔符组件
description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
seo-description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# 自适应表单中的分隔符组件{#separator-component-in-adaptive-forms}

您可以使用分隔符组件以可视方式隔离表单的面板。 您可以通过指定分隔符组件的以下属性来定义分隔符组件的整体外观和样式：

* **元素名** 称：指定组件的名称。SOM表达式用元素名称字段中指定的值对组件进行寻址。
* **粗细：** 指定分隔符组件的粗细（以像素为单位）。

* **CSS类：指** 定分隔符组件的自定义CSS类

* **内联样式：** 现在，借助AEM Forms，您可以将内联CSS样式应用于单个自适应表单组件并实时预览更改。

您可以使用布局模式定义分隔符组件跨入的列数。 有关详细信息，请参阅[使用布局模式调整组件大小](../../forms/using/resize-using-layout-mode.md)。

要指定分隔符组件的属性，请执行以下操作：

1. 选择分隔符组件，然后点按![cmppr](assets/cmppr.png)。 在提要栏中打开属性。
1. 单击“内联CSS属性”部分中的选项卡以指定CSS属性。 例如：a.在“字段”选项卡中，单击&#x200B;**添加项目**。 将添加包含两个字段的行。
1. 在左侧的第一个字段中，指定要应用的CSS3属性。 例如，**border**。 您还可以通过单击向下箭头按钮来选择属性。 下拉列表不是完全的，您可以在此字段中指定任何受支持的CSS3属性名称。
1. 在相邻字段中，为指定的CSS3属性指定一个有效值。 例如，**3px纯黑**。
1. 单击&#x200B;**添加项**&#x200B;以指定其他属性及其值。
1. 单击&#x200B;**预览**&#x200B;以预览表单中的更改。
1. 单击&#x200B;**确定**&#x200B;以确认更改，或单击&#x200B;**取消**&#x200B;以退出对话框而不进行任何更改。

