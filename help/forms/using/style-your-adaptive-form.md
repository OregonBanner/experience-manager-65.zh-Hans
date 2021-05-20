---
title: '设置自适应表单的样式 '
seo-title: '设置自适应表单的样式 '
description: '了解如何创建自定义主题、设置单个组件的样式，以及在主题中使用Web字体 '
seo-description: '了解如何创建自定义主题、设置单个组件的样式，以及在主题中使用Web字体 '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: 自适应表单
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 8%

---

# 设置自适应表单的样式{#do-not-publish-style-your-adaptive-form}

了解如何创建自定义主题、设置单个组件的样式，以及在主题中使用Web字体

![](do-not-localize/08-style_your_adaptiveformmain.png)

本教程是[创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一个步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

## 关于教程{#about-the-tutorial}

您可以使用主题为自适应表单提供独特的外观和样式。 您可以应用随自适应表单编辑器提供的开箱即用主题，也可以创建您自己的自定义主题。 AEM [!DNL Forms]提供[主题编辑器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)以创建自定义主题。 单个主题可以为在移动设备、平板电脑或桌面上打开的同一自适应表单提供不同的外观。 使用主题编辑器不需要任何有关CSS或LESS的先前知识，但需要它。

在教程结束时，您将学习：

* 将现成主题应用于自适应表单
* 使用主题编辑器创建自适应表单的主题
* 设置单个组件的样式
* 附加部分：在自定义主题中使用Web字体

完成教程后，表单将类似于以下内容：

![具有自定义主题的表单](assets/styled-adaptive-form.png)

## 开始之前{#before-you-start}

在本地计算机上下载标题样式和徽标图像（如下所示）。 `shipping-address-add-update-form`自适应表单的标题使用标题样式和徽标图像。 标题样式图像显示在标题的右侧。

[获取文件](assets/header-style.png)

[获取文件](assets/logo-1.png)

## 步骤1:将主题应用于自适应表单{#step-apply-a-theme-to-your-adaptive-form}

自适应表单编辑器提供了多个现成主题。 如果您计划不对自适应表单使用自定义样式，则还可以使用现成的主题发布自适应表单。 主题与自适应表单无关。 您可以将同一主题应用于多个自适应表单。 要将主题应用到自适应表单，请执行以下操作：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 打开&#x200B;**[!UICONTROL 自适应表单容器]**&#x200B;的属性。 在属性浏览器中，导航到&#x200B;**[!UICONTROL 基本]** > **[!UICONTROL 自适应表单主题]**。 **[!UICONTROL 自适应表单主题]**&#x200B;字段列出了所有现成主题和自定义主题。 默认情况下，将应用画布主题。
1. 从&#x200B;**[!UICONTROL 自适应表单主题]**&#x200B;字段中选择主题。 例如，**调查主题**。 点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以应用所选主题。

   ![具有默认主题的自适应表单](assets/default-adaptive-form.png)

   **图：** *具有默认主题的自适应表单*

   ![具有调查主题的自适应表单](assets/adaptive-form-with-survey-theme.png)

   **图：** *具有调查主题的自适应表单*

## 步骤2:更新自适应表单{#step-update-your-adaptive-form}

上面显示的设计需要更改现有自适应表单的占位符文本和徽标。 执行以下步骤以进行所需的更改：

1. 更改标题的现有徽标和文本。 要删除徽标，请执行以下操作：

   1. 在表单编辑器中打开表单。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 点按[!UICONTROL 标题]组件中的徽标图像，然后点按![cmpr](assets/cmppr.png) **[!UICONTROL 属性]**。 在[!UICONTROL image]属性中，点按X以删除现有徽标图像。
   1. 点按&#x200B;**[!UICONTROL upload]**，选择logo.png，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以保存更改。 在[开始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start)部分下载了该图像。
   1. 点按标题文本`We.Retail`，然后点按![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL 编辑]**。 将标题文本更改为`we retail`。 仅对`we retail`中的`we`应用粗体格式。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 删除标题并添加占位符文本：

   1. 点按客户ID字段，然后点按![cmppr](assets/cmppr.png)属性。
   1. 将&#x200B;**[!UICONTROL Title]**&#x200B;字段的内容复制到&#x200B;**[!UICONTROL 占位符文本]**&#x200B;字段。
   1. 删除&#x200B;**[!UICONTROL 标题]**&#x200B;字段的内容，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 对表单中的所有文本框、数字框和电子邮件字段重复上述三个步骤。

      ![更新了自适应表单](assets/updated-adaptive-form.png)

## 步骤3:为自适应表单{#step-create-a-custom-theme-for-your-adaptive-form}创建自定义主题

可以使用[主题编辑器](/help/forms/using/themes.md)创建自定义主题。 主题编辑器是功能强大的WYSIWYG编辑器。 将CSS应用于自适应表单的各种组件是一种可视化方法。 它为自适应表单的组件和面板的样式提供了更精细的控制。

主题是与自适应表单类似的单独实体。 它包含自适应表单的组件和面板的样式(CSS)。 样式包括CSS属性，如背景颜色、状态颜色、透明度、对齐方式和大小。 应用主题时，指定的样式将应用于自适应表单的相应组件。

在本教程中，您将设计页眉和页脚、文本和数字组件、附件组件和按钮的样式。 让我们从创建主题开始：

### 创建主题{#create-a-theme}

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主题]**。 默认URL为[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 主题]**。 出现[!UICONTROL 创建主题]页面，其中包含创建主题所需的字段。 **[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 名称]**&#x200B;字段是必填字段：

   * **标题：** 指定主题的标题。例如，**全局主题。** 标题可帮助您从主题列表中识别主题。
   * **名称：** 指定主题的名称。例如，**Global-Theme。** 在存储库中创建具有指定名称的节点。开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。

1. 点按&#x200B;**[!UICONTROL 创建]**。随即会创建主题，并显示一个用于打开表单进行编辑的对话框。 点按&#x200B;**[!UICONTROL 打开]** ，以在新选项卡中打开新创建的主题。 主题在主题编辑器中打开。 对于样式，主题编辑器使用AEM [!DNL Forms]附带的现成自适应表单。

   有关使用主题编辑器UI的信息，请参阅[关于主题编辑器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 点按&#x200B;**[!UICONTROL 主题选项]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 配置]**。 在&#x200B;**[!UICONTROL 预览表单]**&#x200B;字段中，选择&#x200B;**shipping-add-update-form**&#x200B;自适应表单，点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，点按&#x200B;**[!UICONTROL Save]**。 现在，主题编辑器配置为使用您自己的自适应表单，而不是默认的自适应表单。 点按&#x200B;**[!UICONTROL 取消]**&#x200B;以返回到主题编辑器。

   ![自定义主题](assets/custom-theme.png)

   **图：** *带有shipping-add-update-form自适应表单的主题编辑器*

   ![create-a-theme](assets/create-a-theme.png)

   **图：** *使用默认表单的自适应表单*

### 样式页眉和页脚{#style-header-and-footer}

页眉和页脚为自适应表单提供了一致且独特的外观。 通常，页眉包含组织的徽标和名称，页脚包含版权信息，并且这些信息在组织的多种形式中保持相同。 要设置shipping-add-update-form自适应表单的页眉和页脚的样式，请执行以下操作：

1. 导航“选择器”面板中的&#x200B;**[!UICONTROL 标题]** > **[!UICONTROL 文本]**&#x200B;选项。 “选择器”面板位于主题编辑器的左侧。 如果面板不可见，请点按![切换侧面板](assets/toggle-side-panel.png)切换侧面板。

1. 在&#x200B;**[!UICONTROL Text]**&#x200B;折叠面板中设置以下属性，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 值 |
   |---|---|
   | 字体系列 | Arial |
   | 字体颜色 | FFFFFF |
   | 字体大小 | 54px |

1. 点按[!UICONTROL 标题]小组件，然后点按&#x200B;**[!UICONTROL 标题]**。 用于设置标题小组件样式的选项将显示在左侧。 展开&#x200B;**[!UICONTROL Dimension和位置]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL 高度]**&#x200B;设置为`120px`，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展开标题小组件的&#x200B;**[!UICONTROL Background]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL Background Color]**&#x200B;设置为`F6921E.`

   将鼠标悬停在&#x200B;**[!UICONTROL Image &amp; Gradient]** > **[!UICONTROL + Add]**&#x200B;上，点按&#x200B;**[!UICONTROL Image]**。 设置以下属性，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 值 |
   |---|---|
   | 图像 | 上传header-style.png。 在[开始之前](/help/forms/using/style-your-adaptive-form.md#before-you-start)部分下载了该图像。 |
   | 位置 | 右下 |
   | 并排显示 | 不重复 |

1. 在主题编辑器中，点按标题中的徽标，然后点按&#x200B;**[!UICONTROL 标题徽标]**。 展开“Dimension和位置”折叠面板，设置以下属性，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>顶部：1.5rem</li> 
        <li>底部：-35px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>提示：</strong> 点按链 <img src="assets/link.png"> 接图标，为每个字段提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 点按页脚小组件，然后点按&#x200B;**[!UICONTROL 页脚]**。 展开&#x200B;**[!UICONTROL Background]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL Background Color]**&#x200B;设置为`F6921E`，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 设置数据捕获组件的样式，并将背景应用于自适应表单{#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在自适应表单中使用多个组件来捕获数据。 例如，文本框和数字框。 您可以提供与所有数据捕获组件相同的样式，也可以为每个组件提供单独的样式。 在本教程中，数字框（客户ID、邮政编码）和文本框（客户ID、名称、送货地址、状态、电子邮件）应用了相同的样式。 要设置数据捕获组件的样式，请执行以下操作：

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段，然后点按&#x200B;**[!UICONTROL 字段小组件]**&#x200B;选项。 设置以下属性，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>顶部：7px<br /> </li> 
        <li>对：7px<br /> </li> 
        <li>底部：7px<br /> </li> 
        <li>左：7px<br /> </li> 
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
        <li>左：10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段上方的空区域，然后点按&#x200B;**[!UICONTROL 响应面板容器]**。 将&#x200B;**[!UICONTROL Background]** > **[!UICONTROL Background Color]**&#x200B;设置为F1F2F2。 点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![](do-not-localize/responsive-panel-container.png)

### 设置按钮的样式{#style-the-buttons}

您可以使用自定义主题将相同的样式应用于自适应表单的所有按钮，[内联样式](/help/forms/using/inline-style-adaptive-forms.md)将样式应用于特定按钮。 要设置按钮的样式，请执行以下操作：

1. 点按&#x200B;**[!UICONTROL Submit]**&#x200B;按钮，然后点按&#x200B;**[!UICONTROL Button]**&#x200B;选项。 设置以下属性，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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
        <li>顶部：7px<br /> </li> 
        <li>对：7px<br /> </li> 
        <li>底部：7px<br /> </li> 
        <li>左：7px</li> 
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

1. [将自定义主题](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)（全局主题）应用到自适应表单。如果样式未反映在自适应表单上，请清理浏览器缓存，然后重试。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步骤4:设置单个组件的样式{#step-style-individual-components}

某些样式仅适用于特定组件。 此类组件在自适应表单编辑器中设置样式。

1. 打开自适应表单进行编辑。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在顶部栏中，选择&#x200B;**[!UICONTROL Style]**&#x200B;选项。

   ![style-option](assets/style-option.png)

1. 点按&#x200B;**[!UICONTROL Attach]**&#x200B;按钮，然后点按![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 在&#x200B;**[!UICONTROL Dimension和位置]**&#x200B;折叠面板中设置以下属性：

   | 属性 | 值 |
   |---|---|
   | 浮点数 | 左 |
   | 宽度 | 10% |

1. 点按&#x200B;**[!UICONTROL 政府批准的地址校样]**&#x200B;选项，然后点按![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 设置以下属性：

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
        <li>左：10px</li> 
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
        <li>对：2rem</li> 
        <li>左：10rem </li> 
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

1. 点按&#x200B;**[!UICONTROL Submit]**&#x200B;按钮，然后点按![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 设置以下属性：

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
        <li>顶部：5rem</li> 
        <li>对：14rem</li> 
        <li>底部：20px</li> 
        <li>左：20px<br /> </li> 
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

   ![样式化自适应表单1](assets/styled-adaptive-form-1.png)

## 步骤5:附加部分：在自定义主题{#step-bonus-section-using-web-fonts-in-a-custom-theme}中使用Web字体

您可以使用各种字体来设计自适应表单。 查看自适应表单的所有设备可能没有设计自适应表单所使用的字体。 您可以使用Web字体服务将所需的字体交付到目标设备。

[!DNL Adobe Fonts] 是web字体服务。您可以对自适应表单配置并使用该服务。 要在自适应表单中使用[!DNL Adobe Fonts]，请执行以下操作：

>[!NOTE]
>
>![typekit到adobe-fontsis现在](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] 称为Adobe Fonts，随Creative Cloud和其他订阅提供。[了解更多](https://fonts.adobe.com/)。

1. 创建[Adobe Fonts](https://typekit.com/)帐户，创建套件，将字体Myriad Pro添加到套件，发布套件，并获取套件ID。 需要在自适应表单中使用[!DNL Adobe Fonts]（Web字体）。
1. 在AEM [!DNL Forms]服务器中，导航到![ adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**。 现在，打开配置文件夹。 如果配置已可用，请单击&#x200B;**[!UICONTROL 创建]**&#x200B;按钮以创建新实例。

   在创建配置对话框中，为配置指定&#x200B;**标题** ，然后单击&#x200B;**[!UICONTROL 创建]**。 系统会将您重定向到配置页面。 在出现的[!UICONTROL 编辑组件]对话框中，提供您的&#x200B;**工具包ID**，然后单击&#x200B;**[!UICONTROL 确定]**。

1. 配置主题以使用[!DNL Adobe Fonts]配置。 在创作实例中，打开主题编辑器中的&#x200B;**[!UICONTROL 全局主题]**。 在主题编辑器中，导航到&#x200B;**[!UICONTROL 主题选项]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 配置]**。 在&#x200B;**[!UICONTROL Adobe Fonts配置]**&#x200B;字段中，选择工具包，然后单击&#x200B;**[!UICONTROL 保存]**。

   添加到&#x200B;**[!UICONTROL Adobe Fonts]**&#x200B;的字体可在所有组件的&#x200B;**[!UICONTROL Text]**&#x200B;折叠面板中进行选择。
