---
title: 创建自定义自适应表单主题
seo-title: 创建自定义自适应表单主题
description: 自适应表单主题是AEM客户端库，用于定义自适应表单的样式（外观）。 了解如何创建自定义自适应表单主题。
seo-description: 自适应表单主题是AEM客户端库，用于定义自适应表单的样式（外观）。 了解如何创建自定义自适应表单主题。
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 创建自定义自适应表单主题{#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供了[主题编辑器](/help/forms/using/themes.md)创建和修改自适应表单[主题](/help/forms/using/themes.md)的功能。 仅当您从没有[主题编辑器](/help/forms/using/themes.md)的版本升级，并且已对使用Less/CSS文件（预主题编辑器方法）创建的主题进行了现有投资时，才应执行本文中列出的步骤。

## 前提条件 {#prerequisites}

* LESS（精简版CSS）框架知识
* 如何在Adobe Experience Manager中创建客户端库
* [创建自适应表](/help/forms/using/custom-adaptive-forms-templates.md) 单模板以使用您创建的主题

## 自适应表单主题{#adaptive-form-theme}

**自适应表单主题**&#x200B;是一个AEM客户端库，用于定义自适应表单的样式（外观）。

创建&#x200B;**自适应模板**&#x200B;并将主题应用于模板。 然后，使用此自定义模板创建&#x200B;**自适应表单**。

![自适应表单和客户端库](assets/hierarchy.png)

## 创建自适应表单主题{#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>使用AEM对象（如节点、属性和文件夹）的示例名称描述了以下过程。
>
>如果使用名称执行这些步骤，则生成的模板应类似于以下快照：

![林主题自适应表单](assets/thumbnail.png)
**快照图：** *林主题示例*

1. 在`/apps`节点下创建类型为`cq:ClientLibraryFolder`的节点。

   例如，创建以下节点：

   `/apps/myAfThemes/forestTheme`

1. 向节点添加多值字符串属性`categories`并相应地设置其值。

   例如，将属性设置为：`af.theme.forest`。

   ![CRX存储库快照](assets/3-2.png)

1. 向步骤1中创建的节点添加两个文件夹（`less`和`css`）以及一个文件(`css.txt`):

   * `less` 文件夹：包含 `less` 用于定义变量和 `less` 用 `less mixins` 于管理.css样式的变量文件。

      此文件夹由`less`变量文件、`less` mixin文件、`less`文件组成，这些文件使用mixin和变量定义样式。 然后，所有这些较少的文件都将以styles.less的形式导入。

   * `css`文件夹：包含.css文件，您可以在其中定义要在主题中使用的静态样式。

   **变量文件较少**:这些文件是您在其中定义或覆盖定义CSS样式时使用的变量的文件。

   自适应表单提供在以下.less文件中定义的OOTB变量：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   自适应表单还提供以下内容中定义的第三方变量：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用随自适应表单提供的较少变量，可以覆盖这些变量，也可以创建新的较少变量。

   >[!NOTE]
   >
   >导入较少预处理器的文件时，在import语句中指定文件的相对路径。

   覆盖变量的示例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   要覆盖`less`变量，请执行以下操作：

   1. 导入默认自适应表单变量：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然后，导入包含被覆盖变量的较少文件。

   示例新变量定义：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **少混合文件：** 您可以定义接受变量作为参数的函数。这些函数的输出是生成的样式。 在不同样式中使用这些混合，以避免重复CSS样式。

   自适应表单提供在以下位置定义的OOTB混合：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   自适应表单还提供以下定义的第三方混合：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   混合定义示例：

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Styles.less文件：** 使用此文件可包含您在客户端库中需要使用的所有较少文件（变量、混合、样式）。

   在以下示例`styles.less`文件中，可以按任意顺序放置import语句。

   必须使用用于导入以下.less文件的语句：

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   `css.txt`包含要为库下载的.css文件的路径。

   例如：

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >styles.less文件不是必填文件。 这意味着，如果您未定义任何自定义样式、变量或混合，则无需创建此文件。
   >
   >但是，如果不创建style.less文件，则需要在css.txt文件中取消注释以下行：
   >
   >**`#base=less`**
   >
   >并注释以下行：
   >
   >**`styles.less`**

## 在自适应表单{#to-use-a-theme-in-an-adaptive-form}中使用主题

创建自适应表单主题后，请执行以下步骤以在自适应表单中使用此主题：

1. 要包含在[中创建的主题以创建自适应表单主题](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p)部分，请创建类型为`cq:Component`的自定义页面。

   例如，`/apps/myAfCustomizations/myAfPages/forestPage`

   1. 添加`sling:resourceSuperType`属性，并将其值设置为`fd/af/components/page/base`。

      ![CRX存储库快照](assets/1-2.png)

   1. 要在页面中使用主题，您需要向节点添加覆盖文件library.jsp。

      然后，导入在创建本文自适应表单主题部分中创建的主题。

      以下代码片段示例导入了`af.theme.forest`主题。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可选**:在自定义页中，根据需要覆盖header.jsp、footer.jsp和body.jsp。

1. 创建自定义模板(例如：`/apps/myAfCustomizations/myAfTemplates/forestTemplate`)，其jcr:content指向在上一步中创建的自定义页面(例如：`myAfCustomizations/myAfPages/forestPage)`。

   ![CRX存储库快照](assets/2-1.png)

1. 使用在上一步中创建的模板创建自适应表单。 自适应表单的外观由本文创建自适应表单主题部分中创建的主题定义。
