---
title: 自定义自适应表单的错误消息的布局和位置
description: 您可以自定义自适应对象的错误消息的布局和位置。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 自定义自适应表单的错误消息的布局和位置{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

您可以自定义自适应表单的错误消息的布局和位置。 您可以执行以下自定义设置：

* 自定义字段标题的位置和布局，而不更改相应的CSS属性
* 自定义内联错误消息的位置
* 自定义动态帮助指示器的内容
* 自定义字段组件（题注、小组件、简短描述、详细描述和帮助指示器组件）的位置，而不更改相应的CSS属性

## 自定义字段布局 {#customize-layout-of-fields}

您可以自定义单个字段或所有字段的布局，以更改标题和错误消息的位置。

要将自定义布局应用于字段，请执行以下操作：

### 自定义单个字段的布局 {#customize-layout-of-a-single-field}

1. 在中打开表单 **样式** 模式。 要在样式模式下打开表单，请在页面工具栏中，点按 ![画布下拉列表](assets/canvas-drop-down.png) > **样式**.
1. 在侧栏中，在 **表单对象**，选择字段并点击编辑按钮 ![编辑按钮](assets/edit-button.png).
1. 选择要自定义的字段的状态，并指定该状态的样式。

   ![指定字段的内联样式](assets/edit-error-state.png)

### 自定义表单所有字段的布局 {#customize-layout-of-all-the-fields-of-a-form}

通过AEM Forms，您现在可以创建主题并将其应用于表单。 主题编辑器允许您在一个位置指定表单组件的样式。 创建主题时，可在组件级别指定样式。 有关主题的更多信息，请参阅 [AEM Forms中的主题](../../forms/using/themes.md).

使用主题编辑器创建主题以自定义表单中所有字段的布局。 创建主题后，请执行以下步骤以将其应用于表单：

1. 在编辑模式下打开表单。
1. 在编辑模式下，选择一个组件，然后点按 ![字段级](assets/field-level.png) > **自适应表单容器**，然后点击 ![cmppr](assets/cmppr.png).
1. 在侧栏的自适应表单主题下，选择您使用主题编辑器创建的主题。

## 创建自定义字段布局 {#create-a-custom-field-layout}

1. 打开 CRXDE Lite。默认URL为https://&#39;[服务器]：[端口]&#39;/crx/de.
1. 将字段布局从/libs/fd/af/layouts/field节点（例如defaultFieldLayout）复制到/apps节点（例如/apps/af-field-layout）。
1. 重命名复制的节点和defaultFieldLayout.jsp文件。 例如，errorOnRight.jsp。

1. 更改所复制节点的qtip和jcr：description属性的值。 例如，将属性的值更改为Error On Right

1. 要添加新样式和行为，请在/etc节点中创建客户端库。

   例如，在/etc/af-field-layout-clientlib位置，创建节点client-library。 添加值为af.field.errorOnRight的categories属性以及具有以下代码的style.less文件：

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. 要增强外观和行为，请在布局文件(errorOnRight.jsp)中包含创建的客户端库。
1. 打开字段的编辑对话框，然后选择 **样式** 选项卡。 在 **配置字段布局** 下拉框中，选择新创建的布局，然后单击 **确定**.

ErrorOnRight.zip包包含用于在字段右侧显示错误消息的代码。

[获取文件](assets/erroronright.zip)
