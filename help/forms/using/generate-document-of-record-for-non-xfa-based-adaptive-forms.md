---
title: 为自适应表单生成记录文档
description: 介绍如何为自适应表单的记录文档(DoR)生成模板。
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 3%

---

# 为自适应表单生成记录文档{#generate-document-of-record-for-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) |
| AEM 6.5 | 本文 |


## 概述 {#overview}

提交表单后，您的客户通常希望以打印或文档格式记录他们在表单中填写的信息，以供将来参考。 这称为记录文档。

本文介绍了如何为自适应表单生成记录文档。

>[!NOTE]
>
>基于XFA的自适应表单不支持自动生成记录文档。 但是，您可以使用用于创建自适应表单作为记录文档的XDP。

## 自适应表单类型及其记录文档 {#adaptive-form-types-and-their-documents-of-record}

创建自适应表单时，可以选择表单模型。 您的选项包括：

* [表单模板](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
允许您为自适应表单选择XFA模板。 当您选择XFA模板时，可以为记录文档使用关联的XDP文件，如上所述。

* [XML架构](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
允许您为自适应表单选择XML架构定义。 在为自适应表单选择XML架构时，您可以：

   * 为记录文档关联XFA模板。 确保关联的XFA模板使用与您的自适应表单相同的XML架构
   * 自动生成记录文档

* 无允许您创建没有表单模型的自适应表单。 系统会自动为您的自适应表单生成记录文档。

选择表单模型时，使用记录文档模板配置下可用的选项配置记录文档。 请参阅 [记录文档模板配置](#document-of-record-template-configuration).

## 自动生成记录文档 {#automatically-generated-document-of-record}

记录文档允许客户保留已提交表单的副本以进行打印。 当您自动生成记录文档时，每次更改表单时，其记录文档都会立即更新。 例如，对于选择美利坚合众国作为其国家/地区的客户，您将删除年龄字段。 当此类客户生成记录文档时，他们在记录文档中看不到年龄字段。

自动生成的记录文档具有以下优点：

* 它负责数据绑定。
* 它会自动隐藏在提交时标记为从记录文档中排除的字段。 无需额外工作。
* 本发明为记录文档模板的设计节省了时间。
* 它允许您使用不同的基本模板尝试不同的样式和外观，并为记录文档选择最佳的样式和外观。 样式外观是可选的，如果未指定样式，系统样式将设置为缺省值。
* 它确保表单中的任何更改都立即反映在记录文档中。

## 自动生成记录文档的组件 {#components-to-automatically-generate-a-document-of-record}

要为自适应表单生成记录文档，您需要以下组件：

**自适应表单** 要为其生成记录文档的自适应表单。

**基本模板（推荐）** 在AEM Designer中创建的XFA模板（XDP文件）。 基本模板用于指定记录文档模板的样式和品牌信息。

请参阅 [记录文档的基础模板](#base-template-of-a-document-of-record)

>[!NOTE]
>
>记录文档的基础模板也称为记录文档的元模板。

**记录文档模板** 从自适应表单生成的XFA模板（XDP文件）。

请参阅 [记录文档模板配置](#document-of-record-template-configuration).

**表单数据** 用户在自适应表单中填写的信息。 它与记录文档模板合并以生成记录文档。

## 自适应表单元素映射 {#mapping-of-adaptive-form-elements}

以下各节介绍自适应表单元素在记录文档中的显示方式。

### 字段 {#fields}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>对应的XFA组件</th>
   <th>默认情况下包含在记录文档模板中？</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>按钮</td>
   <td>按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td>复选框</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td>日期/时间字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>下拉列表</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>潦草签名</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>数值框</td>
   <td>数值字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密码框</td>
   <td>密码字段</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td>单选按钮</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文本字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>“重置”按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>“提交”按钮</td>
   <td><p>电子邮件提交按钮</p> <p>HTTP提交按钮</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>条款和条件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td> </td>
   <td>false</td>
   <td>在记录文档模板中不可用。 仅通过附件在记录文档中可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>对应的XFA组件</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表单<br /> </td>
   <td>可重复面板映射到可重复的子表单。</td>
  </tr>
 </tbody>
</table>

### 静态组件 {#static-components}

| 自适应表单组件 | 对应的XFA组件 | 注释 |
|---|---|---|
| 图像 | 图像 | 除非使用记录文档设置进行排除，否则TextDraw和Image组件（无论已绑定还是未绑定）始终显示在基于XSD的自适应表单的记录文档中。 |
| 文本 | 文本 |

>[!NOTE]
>
>在经典UI中，您获得不同的选项卡用于编辑字段属性。

### 表 {#tables}

自适应表单表组件（如页眉、页脚和行）映射到相应的XFA组件。 您可以将可重复面板映射到记录文档中的表格。

## 记录文档的基础模板 {#base-template-of-a-document-of-record}

基本模板为记录文档提供样式和外观信息。 它允许您自定义自动生成记录文档的默认外观。 例如，您希望在记录文档的页眉中添加公司徽标，在页脚中添加版权信息。 基础模板中的母版页用作记录文档模板的母版页。 母版页可以包含可应用于记录文档的页眉、页脚和页码等信息。 您可以使用基本模板将此类信息应用于记录文档，以自动生成记录文档。 使用基本模板可以更改字段的默认属性。

请务必关注 [基本模板约定](#base-template-conventions) 当您设计基础模板时。

## 基本模板约定 {#base-template-conventions}

基本模板用于定义记录文档的页眉、页脚、样式和外观。 页眉和页脚可以包含公司徽标和版权文本等信息。 基础模板中的第一个母版页被复制并用作记录文档的母版页，该母版页包含页眉、页脚、页码或应在记录文档的所有页面上显示的任何其他信息。 如果使用的基础模板不符合基础模板约定，则基础模板中的第一个母版页仍用于记录文档模板中。 强烈建议您按照其约定设计基础模板，并将其用于自动生成记录文档。

**母版页惯例**

* 在基本模板中，应将根子表单命名为 `AF_METATEMPLATE` 并且母版页为 `AF_MASTERPAGE`.

* 具有名称的母版页 `AF_MASTERPAGE` 位于 `AF_METATEMPLATE` 根子表单优先用于提取页眉、页脚和样式信息。

* 如果 `AF_MASTERPAGE` 不存在，则使用基本模板中存在的第一个母版页。

**字段的样式约定**

* 要对记录文档中的字段应用样式，基本模板在以下位置提供字段： `AF_FIELDSSUBFORM` subfrom位于 `AF_METATEMPLATE` 根子表单。

* 这些字段的属性应用于记录文档中的字段。 这些字段应遵循 `AF_<name of field in all caps>_XFO` 命名约定。 例如，复选框的字段名称应为 `AF_CHECKBOX_XFO`.

要创建基本模板，请在AEM Designer中执行以下操作。

1. 单击 **文件>新建**.
1. 选择 **基于模板** 选项。

1. 选择 **Forms — 记录文档** 类别。
1. 选择 **DoR基本模板**.
1. 单击 **下一个** 并提供所需信息。

1. （可选）修改要应用于记录文档中的字段的样式和外观。
1. 保存表单。

您现在可以将保存的表单用作记录文档的基础模板。
请勿修改或删除基本模板中存在的任何脚本。

**修改基本模板**

* 如果您没有对基础模板中的字段应用任何样式，则建议从基础模板中删除这些字段，以便自动选取对基础模板的任何升级。
* 修改基本模板时，请勿删除、添加或修改脚本。

>[!NOTE]
>
>使用约定并严格遵循上述步骤设计基础模板。

## 记录文档模板配置 {#document-of-record-template-configuration}

配置表单的记录文档模板，让客户下载已提交表单的打印友好副本。 XDP文件用作记录文档模板。 客户下载的记录文档根据XDP文件中指定的布局进行格式设置。

执行以下步骤为自适应表单配置记录文档：

1. 在AEM创作实例中，单击 **Forms > Forms和文档。**
1. 选择表单，然后单击 **查看属性**.
1. 在“属性”窗口中，选择 **表单模型**.
您还可以在创建表单时选择表单模型。

   >[!NOTE]
   >
   >在表单模型选项卡中，确保选择 **架构** 或 **无** 从 **选择自** 下拉菜单。 **[!UICONTROL 将表单模板作为表单模型的基于XFA的表单或自适应表单不支持记录文档。]**

1. 在“表单模型”选项卡的“记录文档模板配置”部分中，选择以下选项之一。

   **无** 如果不想为表单配置记录文档，请选择此选项。

   **将表单模板关联为记录文档模板** 如果您有要用作记录文档模板的XDP文件，请选择此选项。 选择此选项时，将显示AEM Forms存储库中可用的所有XDP文件。 选择相应的文件。

   选定的XDP文件与自适应表单关联。

   **生成记录文档** 选择此选项可使用XDP文件作为基本模板来定义记录文档的样式和外观。 选择此选项时，将显示AEM Forms存储库中可用的所有XDP文件。 选择相应的文件。

   >[!NOTE]
   >
   >确保在以下情况下用于创建自适应表单的架构与XFA表单的架构（数据架构）相同：
   >
   >
   >
   >    * 您的自适应表单基于架构
   >    * 您正在使用 **将表单模板关联为记录文档模板** 记录文档选项
   >
   >

1. 单击 **完成。**

## 自定义记录文档中的品牌信息 {#customize-the-branding-information-in-document-of-record}

生成记录文档时，您可以在记录文档选项卡上更改记录文档的品牌信息。 “记录文档”选项卡包括如下选项：徽标、外观、布局、页眉和页脚、免责声明，以及是否包括未选定的复选框和单选按钮选项。

要将您在“记录文档”选项卡中输入的品牌信息本地化，您需要确保正确设置浏览器的区域设置。 要自定义记录文档的品牌信息，请完成以下步骤：

1. 在记录文档中选择一个面板（根面板），然后选择 ![配置](assets/configure.png).
1. 选择 ![多塔布](/help/forms/using/assets/dortab.png). 此时将显示记录文档选项卡。
1. 选择用于呈现记录文档的默认模板或自定义模板。 如果选择默认模板，则记录文档的缩略图预览将显示在“模板”下拉列表下方。

   ![品牌模板](/help/forms/using/assets/brandingtemplate.png)

   如果选择选择自定义模板，请在AEM Forms服务器上浏览并选择XDP。 如果要使用AEM Forms服务器上尚未存在的模板，则需要先将XDP上传到AEM Forms服务器。

1. 根据您选择默认模板还是自定义模板，以下部分或全部属性将出现在“记录文档”选项卡中。 请适当指定以下内容：

   * **徽标图像**：您可以选择使用自适应表单中的徽标图像，从DAM中选择徽标图像，或从计算机上传徽标图像。
   * **表单标题**
   * **标题文本**
   * **免责声明标签**
   * **免责声明**
   * **免责声明文本**
   * **重点颜色**：标题文本和分隔行在文档或记录PDF中呈现的颜色
   * **字体系列**：记录文档PDF中文本的字体系列
   * **对于复选框和单选按钮组件，仅显示选定值**
   * **用于多个选定值的分隔符**
   * **包括未绑定到数据模型的表单对象**
   * **从记录文档排除隐藏字段**
   * **隐藏面板描述**

   如果您选择的自定义XDP模板包含多个母版页，则这些页的属性将显示在 **[!UICONTROL 内容]** 的部分 **[!UICONTROL 记录文档]** 选项卡。

   ![母版页属性](assets/master-page-properties.png)

   母版页属性包括徽标图像、页眉文本、表单标题、免责声明标签和免责声明文本。 您可以将自适应表单或XDP模板属性应用于记录文档。 默认情况下，AEM Forms将模板属性应用于记录文档。 您还可以定义母版页属性的自定义值。 有关如何在记录文档中应用多个母版页的信息，请参阅 [将多个母版页应用于记录文档](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >如果您使用的是使用6.3之前的Designer版本创建的自适应表单模板，为了使重音颜色和字体系列属性正常工作，请确保根子表单下的自适应表单模板中存在以下内容：

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. 要保存品牌策略更改，请选择“完成”。

## 记录文档中面板的表格和列布局 {#table-and-column-layouts-for-panels-in-document-of-record}

您的自适应表单可能很长，包含多个表单字段。 您可能不希望将记录文档另存为自适应表单的精确副本。 现在，您可以选择表格或列布局以将一个或多个自适应表单面板保存在记录文档PDF中。

在生成记录文档之前，在面板的设置中，选择该面板的记录文档的布局（表格或列）。 面板中的字段将在记录文档中相应组织。

![面板中的字段在记录文档中的表布局中渲染](assets/dortablelayout.png)

面板中的字段在记录文档中的表布局中渲染

![面板中的字段在记录文档的列布局中渲染](assets/dorcolumnlayout.png)

面板中的字段在记录文档的列布局中渲染

## 记录文档设置 {#document-of-record-settings}

记录文档设置允许您选择要包含在记录文档中的选项。 例如，银行接受表单中的姓名、年龄、社会保险号码和电话号码。 该表单会生成银行帐号和分行详细信息。 您可以选择在记录文档中仅显示名称、社会保险编号、银行帐户和分行详细信息。

组件的记录文档设置位于其属性下。 要访问组件的属性，请选择该组件并单击 ![cmppr](assets/cmppr.png) 在覆盖图中。 这些属性列在侧边栏中，您可以在该侧边栏中找到以下设置。

**字段级设置**

* **从记录文档排除**：将属性设置为true会从记录文档排除字段。 这是名为的可编写脚本的属性 `excludeFromDoR`. 其行为取决于 **若隐藏自DoR排除栏位** 表单级别属性。

* **将面板显示为表格：** 设置属性后，如果面板中的字段少于6个，则面板在记录文档中会显示为表格。 仅适用于面板。
* **从记录文档排除标题：** 设置属性会从记录文档中排除面板/表的标题。 仅适用于面板和表格。
* **从记录文档排除描述：** 设置属性会从记录文档中排除面板/表的描述。 仅适用于面板和表格。
* **[!UICONTROL 分页]** > **[!UICONTROL 地标]**：确定选择将面板放置到的位置。
   * **[!UICONTROL 地标]** > **[!UICONTROL 正在关注上一个]**：将面板放置在父面板中上一个对象的后面。
   * **[!UICONTROL 地标]** > **[!UICONTROL 在内容区域中]** >内容区域名称：将面板放置在指定的内容区域中。
   * **[!UICONTROL 地标]** > **[!UICONTROL 下一个内容区域顶部]**：将面板放在下一个内容区域的顶部。
   * **[!UICONTROL 地标]** > **[!UICONTROL 内容区域顶部]** >内容区域名称：将面板放置在指定内容区域的顶部。
   * **[!UICONTROL 地标]** > **[!UICONTROL 在页面]** >母版页名称：将面板放置在指定页面上。 如果未自动插入分页符， [!DNL AEM Forms] 添加分页符。
   * **[!UICONTROL 地标]** > **[!UICONTROL 下一页顶部]**：将面板放在下一页的顶部。 如果未自动插入分页符， [!DNL AEM Forms] 添加分页符。
   * **[!UICONTROL 地标]** > **[!UICONTROL 页面顶部]** >母版页名称：呈现指定的页面时，将面板放置在页面的顶部。 如果未自动插入分页符， [!DNL AEM Forms] 添加分页符。
* **[!UICONTROL 分页]** > **[!UICONTROL 之后]**：确定放置面板后要填充的区域。以下字段在 **[!UICONTROL 之后]** 部分：
   * **[!UICONTROL 之后]** > **[!UICONTROL 继续填充父项]**：继续合并所有要填充到父面板中的剩余对象的数据。
   * **[!UICONTROL 之后]** > **[!UICONTROL 转到下一个内容区域]**：在放置面板后开始填充下一个内容区域。
   * **[!UICONTROL 之后]** > **[!UICONTROL 转到内容区域]** >内容区域名称：放置面板后，开始填充指定的内容区域。
   * **[!UICONTROL 之后]** > **[!UICONTROL 转到下一页]**：在放置面板后开始填充下一页。
   * **[!UICONTROL 之后]** > **[!UICONTROL 转到页面]** >页面名称：放置面板后开始填充指定页面。
* **[!UICONTROL 分页]** > **[!UICONTROL 溢出]**：为跨页面的面板或表设置溢出。 以下字段在 **[!UICONTROL 溢出]** 部分：
   * **[!UICONTROL 溢出]** > **[!UICONTROL 无]**：开始填充下一页。 如果未自动插入分页符， [!DNL AEM Forms] 添加分页符。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 转到内容区域]** >内容区域名称：开始填充指定的内容区域。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 转到页面]** >页面名称：开始填充指定的页面。

有关如何在记录文档中应用分页符和应用多个母版页的信息，请参阅 [在记录文档中应用分页符](#apply-page-breaks-in-dor) 和 [将多个母版页应用于记录文档](#apply-multiple-master-pages-dor).

**表单级别设置**

* **包括DoR中未绑定的字段：** 设置属性后，记录文档中包含来自基于架构的自适应表单的未绑定字段。 默认情况下，它为true。
* **若隐藏自DoR排除栏位：** 设置属性以从中排除隐藏字段 [!UICONTROL 记录文档] 在提交表单时。 当您启用时 [在服务器上重新验证](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)，服务器会先重新计算隐藏字段，然后再将这些字段从 [!UICONTROL 记录文档].

## 在记录文档中应用分页符 {#apply-page-breaks-in-dor}

您可以使用多种方法在记录文档中应用分页符。

要将分页符应用于记录文档，请执行以下操作：

1. 选择面板并选择 ![配置](/help/forms/using/assets/configure.png)
1. 展开 **[!UICONTROL 记录文档]** 以查看属性。

1. 在 **[!UICONTROL 分页]** 部分，选择 ![文件夹](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 地标]** 字段。
1. 选择 **[!UICONTROL 下一页顶部]** 并选择 **[!UICONTROL 选择]**. 您还可以选择 **[!UICONTROL 页面顶部]**，选择母版页，然后选择 **[!UICONTROL 选择]** 以应用分页符。
1. 选择 ![保存](/help/forms/using/assets/save_icon.png) 以保存属性。

所选面板将移至下一页。

## 将多个母版页应用于记录文档 {#apply-multiple-master-pages-dor}

如果您选择的自定义XDP模板包含多个母版页，则这些页的属性将显示在 [!UICONTROL 内容] 的部分 [!UICONTROL 记录文档] 选项卡。 有关更多信息，请参阅 [自定义记录文档中的品牌信息](#customize-the-branding-information-in-document-of-record).

通过将不同的母版页应用于自适应表单的组件，可以将多个母版页应用于记录文档。 使用 [分页](#document-of-record-settings) 文件属性的部分，以应用多个母版页。

以下是如何将多个母版页应用于记录文档的示例：您将包含四个母版页的XDP模板上载到 [!DNL AEM Forms] 服务器。 [!DNL AEM Forms] 默认情况下将模板属性应用于记录文档。 [!DNL AEM Forms] 还将模板中的第一个母版页属性应用于记录文档。

要将第二个母版页属性应用于面板，而将第三个母版页属性应用于后续面板，请执行以下步骤：

1. 选择要应用第二个母版页的面板，然后选择 ![配置](assets/cmppr.png).
1. 在 **[!UICONTROL 分页]** 部分，选择 ![文件夹](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 地标]** 字段。
1. 选择 **[!UICONTROL 第页]**，选择第二个母版页并选择 **[!UICONTROL 选择]**.
AEM Forms将第二个母版页应用于自适应表单中的面板和所有后续面板。
1. 在 **[!UICONTROL 分页]** 部分，选择 ![文件夹](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 之后]** 字段。
1. 选择 **[!UICONTROL 转到页面]**，选择第三个母版页并选择 **[!UICONTROL 选择]**.
1. 选择 ![保存](/help/forms/using/assets/save_icon.png) 以保存属性。
AEM Forms将第三个母版页应用于自适应表单中的面板和所有后续面板。


## 使用记录文档时的主要注意事项 {#key-considerations-when-working-with-document-of-record}

处理自适应表单的记录文档时，请牢记以下注意事项和限制。

* 记录文档模板不支持富文本。 因此，任何富文本在静态自适应表单中或者由最终用户填写的信息中都会以纯文本的形式出现在记录文档中。
* 自适应表单中的文档片段未出现在记录文档中。 但是，支持自适应表单片段。
* 不支持为基于XML架构的自适应表单生成的记录文档中的内容绑定。
* 当用户请求呈现记录文档时，记录文档的本地化版本是应区域设置的要求创建的。 记录文档的本地化与自适应表单的本地化同时发生。 有关记录文档和自适应表单本地化的更多信息，请参阅 [使用AEM翻译工作流将自适应表单和记录文档本地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
