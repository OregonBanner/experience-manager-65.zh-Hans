---
title: 设置自适应表单的样式
seo-title: Style your adaptive form
description: 了解如何创建自定义主题、为各个组件设置样式以及在主题中使用Web字体
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 8%

---

# 设置自适应表单的样式 {#do-not-publish-style-your-adaptive-form}

了解如何创建自定义主题、为各个组件设置样式以及在主题中使用Web字体

![](do-not-localize/08-style_your_adaptiveformmain.png)

本教程是 [创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 系列。 建议按时间顺序关注该系列，以了解、执行和演示完整的教程用例。

## 关于教程  {#about-the-tutorial}

您可以使用主题为自适应表单提供独特的外观和样式。 您可以应用随自适应表单编辑器提供的现成主题，也可以创建自己的自定义主题。 AEM [!DNL Forms] 提供 [主题编辑器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) 创建自定义主题。 单个主题可以为在移动设备、平板电脑或桌面上打开的相同自适应表单提供不同的外观。 使用主题编辑器不需要具备CSS或LESS的任何先验知识，但这是必需的。

在本教程结束时，您将学习：

* 将现成的主题应用于自适应表单
* 使用主题编辑器为自适应表单创建主题
* 为单个组件设置样式
* 附加部分：在自定义主题中使用Web字体

完成本教程后，该表单将类似于以下内容：

![具有自定义主题的表单](assets/styled-adaptive-form.png)

## 开始之前 {#before-you-start}

将下面给定的页眉样式和徽标图像下载到本地计算机上。 的标题 `shipping-address-add-update-form` 自适应表单使用页眉样式和徽标图像。 标题样式图像显示在标题的右侧。

[获取文件](assets/header-style.png)

[获取文件](assets/logo-1.png)

## 步骤1：将主题应用于自适应表单 {#step-apply-a-theme-to-your-adaptive-form}

自适应表单编辑器提供了多个现成的主题。 如果您计划不对自适应表单使用自定义样式，则还可以使用现成的主题发布自适应表单。 主题与自适应表单无关。 您可以将同一主题应用于多个自适应表单。 要将主题应用于自适应表单，请执行以下操作：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 打开属性 **[!UICONTROL 自适应表单容器]**. 在属性浏览器中，导航到 **[!UICONTROL 基本]** > **[!UICONTROL 自适应表单主题]**. 此 **[!UICONTROL 自适应表单主题]** 字段列出了所有现成的主题和自定义主题。 默认情况下，将应用画布主题。
1. 从中选择主题 **[!UICONTROL 自适应表单主题]** 字段。 例如， **调查主题**. 点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 以应用所选主题。

   ![带有默认主题的自适应表单](assets/default-adaptive-form.png)

   **图：** *带有默认主题的自适应表单*

   ![带有调查主题的自适应表单](assets/adaptive-form-with-survey-theme.png)

   **图：** *带有调查主题的自适应表单*

## 步骤2：更新您的自适应表单 {#step-update-your-adaptive-form}

以上显示的设计要求更改现有自适应表单的占位符文本和徽标。 执行以下步骤以进行所需的更改：

1. 更改页眉的现有徽标和文本。 要删除徽标，请执行以下操作：

   1. 在表单编辑器中打开表单。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 点按中的徽标图像 [!UICONTROL 标头] 组件和点按 ![cmppr](assets/cmppr.png) **[!UICONTROL 属性]**. 在 [!UICONTROL 图像] 属性，点按X可删除现有的徽标图像。
   1. 点按 **[!UICONTROL 上传]**，选择logo.png ，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 以保存更改。 图像下载到 [开始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start) 部分。
   1. 点按标题文本， `We.Retail`，然后点按 ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL 编辑]**. 将标题文本更改为 `we retail`. 仅将粗体格式应用于 `we`在 `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 删除标题并添加占位符文本：

   1. 点按客户ID字段，然后点按 ![cmppr](assets/cmppr.png) 属性。
   1. 复制的内容 **[!UICONTROL 标题]** 字段到 **[!UICONTROL 占位符文本]** 字段。
   1. 删除的内容 **[!UICONTROL 标题]** 字段并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. 对表单中的所有文本框、数字框和电子邮件字段重复前三个步骤。

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 步骤3：为自适应表单创建自定义主题 {#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用 [主题编辑器](/help/forms/using/themes.md) 创建自定义主题。 主题编辑器是一个功能强大的WYSIWYG编辑器。 这是一种将CSS应用于自适应表单的各种组件的可视化方法。 它提供更精细的控件以设置自适应表单的组件和面板的样式。

主题是一个单独的实体，例如自适应表单。 它包含自适应表单的组件和面板的样式(CSS)。 样式包括CSS属性，例如背景颜色、状态颜色、透明度、对齐方式和大小。 应用主题时，指定的样式将应用于自适应表单的相应组件。

在本教程中，您将设置页眉和页脚、文本和数字组件、附件组件和按钮的样式。 让我们从创建主题开始：

### 创建主题 {#create-a-theme}

1. 登录到AEM创作实例并导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主题]**. 默认URL为 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. 点按 **[!UICONTROL 创建]** 并选择 **[!UICONTROL 主题]**. 此 [!UICONTROL 创建主题] 此时将显示包含创建主题所需字段的页面。 此 **[!UICONTROL 标题]** 和 **[!UICONTROL 名称]** 字段为必填字段：

   * **标题：** 指定主题的标题。 例如， **全局主题。** 标题可帮助您从主题列表中识别主题。
   * **名称：** 指定主题的名称。 例如， **全局主题。** 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成“名称”字段的值。 您可以更改建议值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入均被替换为连字符。

1. 点按&#x200B;**[!UICONTROL 创建]**。创建主题，并显示用于打开表单进行编辑的对话框。 点按 **[!UICONTROL 打开]** 在新选项卡中打开新创建的主题。 主题将在主题编辑器中打开。 对于样式，主题编辑器使用AEM附带的现成自适应表单 [!DNL Forms].

   有关使用主题编辑器UI的信息，请参阅 [关于主题编辑器](/help/forms/using/themes.md#aboutthethemeeditor).

1. 点按 **[!UICONTROL 主题选项]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 配置]**. 在 **[!UICONTROL 预览表单]** 字段中，选择 **shipping-address-add-update-form** 自适应表单，点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，点按 **[!UICONTROL 保存]**. 现在，主题编辑器配置为使用您自己的自适应表单，而不是默认的自适应表单。 点按 **[!UICONTROL 取消]** 以返回到主题编辑器。

   ![custom-them](assets/custom-theme.png)

   **图：** *带有shipping-address-add-update-form自适应表单的主题编辑器*

   ![create-a-them](assets/create-a-theme.png)

   **图：** *带有默认表单的自适应表单*

### 样式页眉和页脚 {#style-header-and-footer}

页眉和页脚为自适应表单提供一致且独特的外观。 通常，页眉包含组织的徽标和名称，页脚包含版权信息，并且这些信息在组织的多个表单中保持相同。 要设置shipping-address-add-update-form自适应表单的页眉和页脚样式，请执行以下操作：

1. 导航至 **[!UICONTROL 页眉]** > **[!UICONTROL 文本]** 选项。 “选择器”面板位于主题编辑器的左侧。 如果面板不可见，请点按 ![切换侧面板](assets/toggle-side-panel.png) 切换侧面板。

1. 在中设置以下属性 **[!UICONTROL 文本]** 可折叠项和点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 值 |
   |---|---|
   | 字体系列 | Arial |
   | 字体颜色 | FFFFFF |
   | 字体大小 | 54px |

1. 点按 [!UICONTROL 标头] 小工具和点按 **[!UICONTROL 页眉]**. 用于设置标题小组件样式的选项显示在左侧。 展开 **[!UICONTROL Dimension和位置]** 可折叠项，设置 **[!UICONTROL 高度]** 到 `120px`，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 展开 **[!UICONTROL 背景]** 标题小部件的折叠面板，设置 **[!UICONTROL 背景颜色]** 到 `F6921E.`

   将鼠标悬停在 **[!UICONTROL 图像和渐变]** > **[!UICONTROL +添加]**，点按 **[!UICONTROL 图像]**. 设置以下属性并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 值 |
   |---|---|
   | 图像 | 上传header-style.png。 图像下载到 [开始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start) 部分。 |
   | 位置 | 右下 |
   | 并排显示 | 不重复 |

1. 在主题编辑器中，点按标题中的徽标并点按 **[!UICONTROL 页眉徽标]**. 展开Dimension和位置折叠面板，设置以下属性并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>边距</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>顶部：1.5雷姆</li> 
        <li>底部：-35像素</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>提示：</strong> 点按 <img src="assets/link.png"> 链接图标，为每个字段提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 点按页脚小组件并点按 **[!UICONTROL 页脚]**. 展开 **[!UICONTROL 背景]** 可折叠项，设置 **[!UICONTROL 背景颜色]** 到 `F6921E`，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### 设置数据捕获组件的样式，并将背景应用于自适应表单 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在自适应表单中使用多个组件来捕获数据。 例如，文本框和数字框。 您可以为所有数据捕获组件提供相同的样式，或者为每个组件提供单独的样式。 在本教程中，会将相同的样式应用于数字框（客户ID、邮政编码）和文本框（客户ID、名称、送货地址、省/州、电子邮件）。 设置数据捕获组件的样式：

1. 点按 **[!UICONTROL 客户ID]** 字段并点按 **[!UICONTROL 字段小组件]** 选项。 设置以下属性并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>折叠</b></td> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径 </td> 
      <td> 
       <ul> 
        <li>顶部：7像素<br /> </li> 
        <li>右：7像素<br /> </li> 
        <li>底部：7像素<br /> </li> 
        <li>左：7像素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>宽度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>左：10雷姆</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 点按“ ”上方的空白区域 **[!UICONTROL 客户ID]** 字段并点按 **[!UICONTROL 响应面板容器]**. 设置 **[!UICONTROL 背景]** > **[!UICONTROL 背景颜色]** 到F1F2F2。 点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### 设置按钮的样式 {#style-the-buttons}

您可以使用自定义主题将相同的样式应用于自适应表单的所有按钮，并且 [内联样式](/help/forms/using/inline-style-adaptive-forms.md) 将样式应用于特定按钮。 设置按钮的样式：

1. 点按 **[!UICONTROL 提交]** 按钮并点按 **[!UICONTROL 按钮]** 选项。 设置以下属性并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>折叠</b></td> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框<br /> </td> 
      <td>边框颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径 </td> 
      <td> 
       <ul> 
        <li>顶部：7像素<br /> </li> 
        <li>右：7像素<br /> </li> 
        <li>底部：7像素<br /> </li> 
        <li>左：7像素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文本<br /> </td> 
      <td>字体系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18px</td> 
     </tr> 
    </tbody> 
   </table>

1. [应用自定义主题](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)，全局主题，添加到自适应表单。 如果样式未反映在自适应表单上，请清除浏览器缓存并重试。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步骤4：设置单个组件的样式 {#step-style-individual-components}

某些样式仅应用于特定组件。 此类组件在自适应表单编辑器中设置样式。

1. 打开自适应表单进行编辑。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在顶部栏上，选择 **[!UICONTROL 样式]** 选项。

   ![style-option](assets/style-option.png)

1. 点按 **[!UICONTROL 附加]** 按钮并点按 ![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 在中设置以下属性 **[!UICONTROL Dimension和位置]** 可折叠项：

   | 属性 | 值 |
   |---|---|
   | 浮点数 | 左 |
   | 宽度 | 10% |

1. 点按 **[!UICONTROL 政府批准的地址证明]** 选项，然后点按 ![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 设置以下属性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折叠</b></td> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮点数</td> 
      <td>左</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>宽度</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>左：10像素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>高度</td> 
      <td>40px</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置<br /> </td> 
      <td>边距</td> 
      <td><br /> 
       <ul> 
        <li>右：2rem</li> 
        <li>左：10雷姆 </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框宽度</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框样式</td> 
      <td>实线</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体系列</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>行高</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 点按 **[!UICONTROL 提交]** 按钮并点按 ![aem_6_3_edit](assets/aem_6_3_edit.png) 图标。 设置以下属性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折叠</b></td> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>浮点数</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>顶部：5雷姆</li> 
        <li>右：14雷姆</li> 
        <li>底部：20像素</li> 
        <li>左：20像素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 步骤5：附加部分：在自定义主题中使用Web字体 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

您可以使用各种字体设计自适应表单。 查看自适应表单的所有设备可能没有用于设计自适应表单的字体。 您可以使用Web字体服务将所需的字体交付给目标设备。

[!DNL Adobe Fonts] 是Web字体服务。 您可以针对自适应表单配置和使用服务。 使用 [!DNL Adobe Fonts] 在自适应表单中：

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] 现在称为Adobe Fonts，包含在Creative Cloud和其他订阅中。 [了解更多](https://fonts.adobe.com/)。

1. 创建 [Adobe Fonts](https://typekit.com/) 帐户、创建套件、将字体Myriad Pro添加到套件、发布套件并获取套件ID。 需要使用 [!DNL Adobe Fonts] （Web字体）。
1. 在AEM中 [!DNL Forms] 服务器，导航到 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. 现在，打开一个配置文件夹。 如果配置已经可用，请单击 **[!UICONTROL 创建]** 按钮以创建新实例。

   在创建配置对话框中，指定 **标题** ，然后单击 **[!UICONTROL 创建]**. 您将被重定向到配置页面。 在 [!UICONTROL 编辑组件] 对话框，请提供 **套件ID** 并单击 **[!UICONTROL 确定]**.

1. 配置主题以使用 [!DNL Adobe Fonts] 配置。 在创作实例上，打开 **[!UICONTROL 全局主题]** 在主题编辑器中。 在主题编辑器中，导航到 **[!UICONTROL 主题选项]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 配置]**. In **[!UICONTROL Adobe Fonts配置]** 字段，选择配套件，然后单击 **[!UICONTROL 保存]**.

   添加到中的字体 **[!UICONTROL Adobe Fonts]** 可在 **[!UICONTROL 文本]** 所有组件的折叠面板。
