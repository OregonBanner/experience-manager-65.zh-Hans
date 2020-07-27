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
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# 创建自定义自适应表单主题 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供 [主题编辑器](/help/forms/using/themes.md) ，以创建和修改自适应表单 [主题](/help/forms/using/themes.md)。 只有从没有主题编辑器的版本升级，并且已对使用Less/CSS文件( [预主题编辑器方法](/help/forms/using/themes.md) )创建的主题进行了现有投资，才能修改本文中列出的步骤。

## 前提条件 {#prerequisites}

* 了解LESS(Leaner CSS)框架
* 如何在Adobe Experience Manager中创建客户端库
* [创建自适应表单模板](/help/forms/using/custom-adaptive-forms-templates.md) ，以使用您创建的主题

## Adaptive form theme {#adaptive-form-theme}

自适应 **表单主题** 是AEM客户端库，用于定义自适应表单的样式（外观）。

您可以创建自 **适应模板** ，并将主题应用到模板。 然后，使用此自定义模板创建自 **适应表单**。

![自适应表单和客户端库](assets/hierarchy.png)

## 创建自适应表单主题 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>使用节点、属性和文件夹等AEM对象的示例名称介绍了以下过程。
>
>如果使用名称执行这些步骤，则生成的模板应类似于以下快照：

![林主题自适应表单快照](assets/thumbnail.png)**图：** *林主题示例*

1. 在节点下创建类 `cq:ClientLibraryFolder` 型的 `/apps`节点。

   例如，创建以下节点：

   `/apps/myAfThemes/forestTheme`

1. 向节点添加多值字符串 `categories` 属性并相应地设置其值。

   例如，将属性设置为： `af.theme.forest`.

   ![CRX存储库快照](assets/3-2.png)

1. 将两个文件 `less` 夹 `css`和一个文件 `css.txt` 添加到在步骤1中创建的节点：

   * `less` 文件夹： 包含 `less` 用于定义变量和 `less` 管理 `less mixins` .css样式的变量文件。

      此文件夹由变量 `less` 文件、混合 `less` 文件、使用混合 `less` 和变量定义样式的文件组成。 然后，所有这些较少的文件都以样式。less导入。

   * `css`文件夹： 包含。css文件，您可在其中定义要在主题中使用的静态样式。

   **变量文件更少**: 这些是文件，您可在其中定义或覆盖用于定义CSS样式的变量。

   自适应表单提供在以下。less文件中定义的OOTB变量：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   自适应表单还提供以下定义的第三方变量：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用随自适应表单提供的较少变量，可以覆盖这些变量，也可以创建新的较少变量。

   >[!NOTE]
   >
   >导入较少预处理器的文件时，在import语句中指定文件的相对路径。

   覆盖变量示例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   要覆盖变 `less`量：

   1. 导入默认自适应表单变量：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然后导入包含被覆盖变量的较少文件。

   新变量定义示例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **混音文件更少：** 您可以定义接受变量作为参数的函数。 这些函数的输出是生成的样式。 在不同的样式中使用这些混音，以避免重复CSS样式。

   自适应表单提供在以下位置定义的OOTB混合：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   自适应表单还提供以下定义的第三方混合：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   混音定义示例：

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

   **Styles.less文件：** 使用此文件可以包含客户端库中需要使用的所有较少文件（变量、混合、样式）。

   在以下示例文 `styles.less` 件中，导入语句可以按任意顺序放置。

   导入以下。less文件的语句是必填的：

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

   包 `css.txt` 含要为库下载的。css文件的路径。

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
   >styles.less文件不是必需的。 这意味着，如果您尚未定义任何自定义样式、变量或混合，则无需创建此文件。
   >
   >但是，如果不在css.txt文件中创建style.less文件，则需要取消以下行的注释：
   >
   >**`#base=less`**
   >
   >并注释以下行：
   >
   >**`styles.less`**

## 在自适应表单中使用主题 {#to-use-a-theme-in-an-adaptive-form}

创建自适应表单主题后，请执行以下步骤以在自适应表单中使用此主题：

1. 要包含创建自适应表 [单主题部分的主题](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) ，请创建自定义页面类型 `cq:Component`。

   例如，`/apps/myAfCustomizations/myAfPages/forestPage`

   1. 添加属 `sling:resourceSuperType` 性并将其值设置为 `fd/af/components/page/base`。

      ![CRX存储库快照](assets/1-2.png)

   1. 要使用页面中的主题，您需要向节点添加一个覆盖文件library.jsp。

      然后，导入在本文的“要创建自适应表单主题”部分中创建的主题。

      以下示例代码片段导入主 `af.theme.forest` 题。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可选**: 在自定义页面中，根据需要覆盖header.jsp、footer.jsp和body.jsp。

1. 创建自定义模板(例如： `/apps/myAfCustomizations/myAfTemplates/forestTemplate`)，其jcr:content指向在上一步中创建的自定义页面(例如： `myAfCustomizations/myAfPages/forestPage)`.

   ![CRX存储库快照](assets/2-1.png)

1. 使用在上一步中创建的模板创建自适应表单。 自适应表单的外观由本文“要创建自适应表单主题”部分中创建的主题定义。

