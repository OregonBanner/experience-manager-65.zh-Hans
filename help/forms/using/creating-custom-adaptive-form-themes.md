---
title: 创建自定义自适应表单主题
seo-title: Creating custom adaptive form themes
description: 自适应表单主题是一个AEM客户端库，可使用它定义自适应表单的样式（外观）。 了解如何创建自定义自适应表单主题。
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 创建自定义自适应表单主题 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供 [主题编辑器](/help/forms/using/themes.md) 创建和修改自适应表单的功能 [主题](/help/forms/using/themes.md). 执行本文中列出的步骤（仅当从没有的版本升级时） [主题编辑器](/help/forms/using/themes.md) 并且您目前在使用Less/CSS文件（预主题编辑器方法）创建的主题方面有所投资。

## 前提条件 {#prerequisites}

* 了解LESS (Leaner CSS)框架
* 如何在Adobe Experience Manager中创建客户端库
* [创建自适应表单模板](/help/forms/using/custom-adaptive-forms-templates.md) 用于使用您创建的主题

## 自适应表单主题 {#adaptive-form-theme}

An **自适应表单主题** 是一个AEM客户端库，可使用它定义自适应表单的样式（外观）。

您创建 **自适应模板** 并将主题应用于模板。 然后，您可以使用此自定义模板创建 **自适应表单**.

![自适应表单和客户端库](assets/hierarchy.png)

## 创建自适应表单主题 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>以下过程使用AEM对象（如节点、属性和文件夹）的示例名称进行描述。
>
>如果使用名称执行这些步骤，则生成的模板应类似于以下快照：

![林主题的自适应表单快照](assets/thumbnail.png)
**图：** *林主题示例*

1. 创建节点类型 `cq:ClientLibraryFolder` 在 `/apps`节点。

   例如，创建以下节点：

   `/apps/myAfThemes/forestTheme`

1. 添加多值字符串属性 `categories` ，并相应地设置其值。

   例如，将属性设置为： `af.theme.forest`.

   ![CRX存储库快照](assets/3-2.png)

1. 添加两个文件夹， `less` 和 `css`和文件 `css.txt` 到步骤1中创建的节点：

   * `less` 文件夹：包含 `less` 变量文件，可在其中定义 `less` 变量和 `less mixins` 用于管理.css样式的属性。

      此文件夹包括 `less` 变量文件， `less` mixin文件， `less` 使用mixin和变量定义样式的文件。 然后所有这些较少的文件以样式.less导入。

   * `css`文件夹：包含.css文件，可在其中定义要在主题中使用的静态样式。

   **变量较少文件**：这些是文件，您可以在其中定义或覆盖在定义CSS样式中使用的变量。

   自适应表单提供以下.less文件中定义的OOTB变量：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   自适应表单还提供中定义的第三方变量：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用自适应表单中提供的更少变量，也可以覆盖这些变量，或者创建新的更少变量。

   >[!NOTE]
   >
   >在导入较少预处理器的文件时，在import语句中指定文件的相对路径。

   覆盖变量的示例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   要覆盖 `less`变量：

   1. 导入默认自适应表单变量：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然后导入包含被覆盖变量的较少文件。

   新变量定义示例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **更少的mixin文件：** 您可以定义接受变量作为参数的函数。 这些函数的输出是生成样式。 请在不同的样式中使用这些mixin，以避免重复CSS样式。

   自适应表单提供中定义的OOTB mixin：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   自适应表单还提供中定义的第三方Mixin：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   示例mixin定义：

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

   **Styles.less文件：** 使用此文件可以包含需要在客户端库中使用的所有较少文件（变量、mixin、样式）。

   在以下示例中 `styles.less` 文件，导入语句可以按任意顺序放置。

   导入以下.less文件的语句是必需的：

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

   此 `css.txt` 包含要为库下载的.css文件的路径。

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
   >styles.less文件不是强制性的。 这意味着如果您尚未定义任何自定义样式、变量或mixin，则无需创建此文件。
   >
   >但是，如果您未创建style.less文件，则需要在css.txt文件中取消注释以下行：
   >
   >**`#base=less`**
   >
   >并注释以下行：
   >
   >**`styles.less`**

## 在自适应表单中使用主题 {#to-use-a-theme-in-an-adaptive-form}

创建自适应表单主题后，执行以下步骤以在自适应表单中使用此主题：

1. 包括在中创建的主题 [创建自适应表单主题](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) 部分，创建类型的自定义页面 `cq:Component`.

   例如，`/apps/myAfCustomizations/myAfPages/forestPage`

   1. 添加 `sling:resourceSuperType` 属性并将其值设置为 `fd/af/components/page/base`.

      ![CRX存储库快照](assets/1-2.png)

   1. 要在页面中使用主题，您需要向节点添加覆盖文件library.jsp。

      然后，导入在本文的创建自适应表单主题部分中创建的主题。

      以下示例代码片段导入 `af.theme.forest` 主题。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可选**：在自定义页面中，根据需要覆盖header.jsp、footer.jsp和body.jsp。

1. 创建自定义模板(例如： `/apps/myAfCustomizations/myAfTemplates/forestTemplate`)的jcr：content指向在上一步中创建的自定义页面(例如： `myAfCustomizations/myAfPages/forestPage)`.

   ![CRX存储库快照](assets/2-1.png)

1. 使用上一步中创建的模板创建自适应表单。 自适应表单的外观由本文的创建自适应表单主题部分中创建的主题定义。
