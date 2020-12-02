---
title: 自定义自适应表单的错误消息的布局和位置
seo-title: 自定义自适应表单的错误消息的布局和位置
description: '您可以自定义自适应错误消息的布局和位置。 '
seo-description: '您可以自定义自适应错误消息的布局和位置。 '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# 自定义自适应表单的错误消息的布局和位置{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

您可以自定义自适应表单错误消息的布局和位置。 您可以执行以下自定义：

* 自定义字段标题的位置和布局，而不对相应的CSS属性进行任何更改
* 自定义内联错误消息的位置
* 自定义动态帮助指示器的内容
* 自定义字段组件（题注、构件、简短描述、长描述和帮助指示器组件）的位置，而不对相应的CSS属性做任何更改

## 自定义字段{#customize-layout-of-fields}的布局

您可以自定义单个字段或所有字段的布局以更改题注和错误消息的位置。 请执行以下步骤将自定义布局应用于字段：

### 自定义单个字段{#customize-layout-of-a-single-field}的布局

请执行以下步骤将自定义布局应用于单个字段：

1. 在&#x200B;**样式**&#x200B;模式下打开表单。 要在样式模式下打开表单，请在页面工具栏中点按![画布下拉框](assets/canvas-drop-down.png) > **样式**。
1. 在提要栏的&#x200B;**表单对象**&#x200B;下，选择字段，然后点按编辑按钮![edit-button](assets/edit-button.png)。
1. 选择要自定义的字段的状态，并指定该状态的样式。

   ![指定字段的内联样式](assets/edit-error-state.png)

### 自定义表单{#customize-layout-of-all-the-fields-of-a-form}中所有字段的布局

有了AEM Forms，您现在可以创建主题并将其应用于表单。 通过主题编辑器，您可以在一个位置指定表单组件的样式。 创建主题时，可在组件级别指定样式。 有关主题的详细信息，请参阅AEM Forms的[主题](../../forms/using/themes.md)。

使用主题编辑器创建主题，以自定义表单中所有字段的布局。 创建主题后，请执行以下步骤将其应用到表单：

1. 在编辑模式下打开表单。
1. 在编辑模式中，选择一个组件，点按![字段级别](assets/field-level.png) > **自适应表单容器**，然后点按![cmpr](assets/cmppr.png)。
1. 在提要栏的自适应表单主题下，选择您使用主题编辑器创建的主题。

## 创建自定义字段布局{#create-a-custom-field-layout}

1. 打开CRXDE lite。 默认URL为https://&#39;[server]:[port]&#39;/crx/de。
1. 将字段布局从/libs/fd/af/layouts/field节点（例如，defaultFieldLayout）复制到/apps节点（例如，/apps/af-field-layout）。
1. 重命名复制的节点和defaultFieldLayout.jsp文件。 例如，errorOnRight.jsp。

1. 更改复制节点的qtip和jcr:description属性的值。 例如，将属性的值更改为“右时出错”

1. 要添加新样式和行为，请在/etc节点中创建客户端库。

   例如，在/etc/af-field-layout-clientlib位置创建节点client-library。 添加具有af.field.errorOnRight值和style.less文件的类别属性，其代码如下：

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
1. 打开字段的编辑对话框，选择&#x200B;**样式**&#x200B;选项卡。 在&#x200B;**配置字段布局**&#x200B;下拉框中，选择新创建的布局，然后单击&#x200B;**确定**。

ErrorOnRight.zip包包含用于在字段右侧显示错误消息的代码。

[获取文件](assets/erroronright.zip)
