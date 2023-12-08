---
title: 自适应表单片段
description: 自适应表单提供一种机制，可创建在任何自适应表单中使用的表单区段，例如面板或一组字段。 您还可以将现有面板另存为片段。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 2f276e9d-b3c1-48f7-a94a-bdf7eb15a031
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '2359'
ht-degree: 3%

---

# 自适应表单片段{#adaptive-form-fragments}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html) |
| AEM 6.5 | 本文 |

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

虽然每个表单都针对特定目的而设计，但大多数表单中都存在一些通用区段，例如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 每次创建新表单时，表单开发人员都需要创建这些常用区段。

自适应表单提供了一种便捷的机制，只需像创建面板或一组字段一样创建表单片段一次，即可在自适应表单中重复使用。 这些可重用的独立区段称为自适应表单片段。

## 创建片段 {#create-a-fragment}

您可以从头开始创建自适应表单片段，或将面板作为片段保存在现有的自适应表单中。

### 从头开始创建片段 {#create-fragment-from-scratch}

1. 在 https:// [*hostname*] 处登录 AEM Forms 作者实例： [*端口*] /aem/forms.html。
1. 按 **一下创建 > 自适应表单片段** 。
1. 指定片段的标题、名称、描述和标记。

   >[!NOTE]
   >
   >请确保为片段指定唯一的名称。 如果已存在另一个同名片段，则创建片段失败。

1. 单击以打开 **表单模型** 选项卡，然后从 **选择自** 下拉菜单，为片段选择以下模型之一：

   * **无**：指定从头开始创建片段，而不使用任何表单模型。

     >[!NOTE]
     >
     > 在基于核心组件的自适应Forms中，您可以在表单中多次使用单个表单片段。 它支持基于无和基于架构的表单片段。

   * **表单模板**：指定使用上传到AEM Forms的XDP模板创建片段。 选择适当的XDP模板作为片段的表单模型。

   ![使用表单模板作为模型创建自适应表单](assets/form-template-model.png)

   还会显示选定表单模板中标记为片段的子表单。 您可以从下拉列表中选择自适应表单片段的子表单。

   ![从指定的表单模板中选择子表单](assets/fragment-subform.png)

   此外，您还可以通过在下拉框中指定子表单的SOM表达式，使用在表单模板中未标记为片段的子表单创建自适应表单片段。

   * **XML架构**：指定使用上载到AEM Forms的XML架构创建片段。 您可以上传或从可用的XML架构中选择作为片段的表单模型。

   ![创建基于XML架构的自适应表单片段作为模型](assets/xml-schema-model.png)

   您还可以通过从下拉框中选择所选架构中存在的complexType来创建自适应表单片段。

   ![从指定的XML架构模型中选择复杂类型](assets/complex-type.png)

1. 单击 **创建** 然后单击 **打开** 以在编辑模式下使用默认模板打开片段。

在编辑模式下，您可以将任何自适应表单组件从AEM Sidekick拖放到片段上。 有关自适应表单组件的信息，请参阅 [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md).

此外，如果您选择了XML架构或XDP表单模板作为片段的表单模型，则内容查找器中会显示一个显示表单模型层次结构的新选项卡。 它可让您将表单模型元素拖放到片段上。 添加的表单模型元素被转换为表单组件，同时保留关联XDP或XSD的原始属性。

### 将面板另存为片段 {#save-panel-as-a-fragment}

1. 打开自适应表单，其中包含要另存为自适应表单片段的面板。
1. 在面板工具栏中，单击 **[!UICONTROL 另存为片段]**. 另存为片段对话框随即打开。

   >[!NOTE]
   >
   >如果要另存为片段的面板包含子面板，则生成的片段将包含这些子面板。

1. 在片段创建对话框中，指定以下信息：

   * **名称**：片段的名称。 默认值为面板的元素名称。 它是必填字段。
     >[!NOTE]
     >
     >请确保为片段指定唯一的名称。 如果已存在另一个同名片段，则创建片段失败。

   * **标题**：片段的标题。 默认值为面板的标题。

   * **描述**：片段的描述。

   * **标记**：片段的标记元数据。

   * **目标路径**：将保存片段的存储库路径。 如果不指定路径，则会在包含自适应表单的节点旁边创建与片段名称相同的节点。 片段将保存在此节点中。

   * **表单模型**：根据自适应表单的表单模型，此字段显示 **XML架构**， **表单模板**，或 **无**. 它是不可编辑的字段。

   * **片段模型根**：仅在基于XSD的自适应表单中显示。 它指定片段模型的根。 您可以选择 **/** 或XSD复杂类型。 请注意，只有在选择复杂类型作为片段模型根时，才能在另一个自适应表单中重用片段。
如果您选择 **/** 作为片段模型根，根中的完整XSD树在自适应表单数据模型选项卡中可见。 对于复杂类型片段模型根，自适应表单数据模型选项卡中仅显示选定复杂类型的后代。 如果您创建片段并选择复杂类型作为 **片段模型根**，无论在何处使用该复杂类型，您都可以将其用在同一个表单内或跨多个表单使用。

   * **XSD参照**：仅在基于XSD的自适应表单中显示。 它显示XML方案的位置。

   * **XDP参照**：仅在基于XDP的自适应表单中显示。 它显示XDP表单模板的位置。

   ![save-fragment](assets/save-fragment.png)

   “另存为片段”对话框

1. 单击&#x200B;**确定**。

   面板保存在存储库中的指定位置或默认位置。 在自适应表单中，面板被替换为片段的快照。 如下所示，“常规信息”面板及其子面板“个人信息和地址”将另存为片段。

   要编辑片段，请单击 **[!UICONTROL 面板工具栏中的编辑资源]** 。 该片段会在新的选项卡或窗口中以编辑模式打开。

   ![编辑片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 配置片段外观 {#configure-fragment-appearance}

您在自适应表单中插入的任何片段都显示为占位符图像。 占位符在片段中最多显示十个子面板的标题。 您可以将AEM Forms配置为显示完整的片段，而不是占位符图像。

执行以下步骤以在表单中显示完整的片段：

1. 转到 AEM web 控制台配置页面 https： [*主机*] ： [*端口*] /system/console/configMgr。

1. Search 并单击 **[!UICONTROL 自适应表单并交互式通信 Web 渠道配置]** ，以在编辑模式下打开它。
1. 禁用 **[!UICONTROL &quot;在替代片段]** 时启用占位符&quot; 复选框可显示完整的片段，而不是占位符图像。

### 在自适应表单中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您创建的自适应表单片段显示在AEM内容查找器的自适应表单片段选项卡中。 要在自适应表单中插入自适应表单片段，请执行以下操作：

1. 在编辑模式下打开自适应表单，您要在其中插入自适应表单片段。
1. 单击 **资产** ![assets浏览器](assets/assets-browser.png) 在侧栏中。 在资产浏览器中，选择 **自适应表单片段** 从下拉菜单中查找。

   您还可以选择显示所有自适应表单片段或根据其表单模型（表单模板、XML架构或基本）进行筛选。

1. 将自适应表单片段拖放到自适应表单上。

   >[!NOTE]
   >
   >自适应表单片段未在自适应表单内进行创作。 此外，在基于JSON的自适应表单中不能以相反的方式使用基于XSD的片段。

自适应表单片段在自适应表单中通过引用插入，并与独立的自适应表单片段同步。 这意味着当您更新自适应表单片段时，更改会反映在使用片段的所有自适应表单中。

### 在自适应表单中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以通过单击 **嵌入资源： &lt;*fragmentname*>** 按钮进行添加，如以下示例图像所示。

![在自适应表单中嵌入表单片段](assets/embed-fragment.png)

>[!NOTE]
>
>嵌入的片段不再与独立片段链接。 您可以从自适应表单中编辑嵌入片段中的组件。

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以创建嵌套的自适应表单片段，这意味着您可以将片段拖放到另一个片段中，并且可以具有嵌套的片段结构。

### 更改片段 {#change-fragments}

您可以使用替换或更改自适应表单片段 **选择片段资源** 自适应表单片段面板的“编辑组件”对话框中的属性。

### 为自适应表单片段生成记录文档 {#generate-DOR-for-fragments}

记录文档(DOR)帮助您以打印或文档格式保留表单信息。 因此，它可以帮助您以后随时跟踪有关客户的信息，您还可以使用记录文档以PDF格式将表单和内容存档在一起。 [了解如何为自适应表单片段生成记录文档](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

### 在自适应表单中多次使用表单片段 {#using-form-fragment-mutiple-times-in-af}

您可以在自适应表单中多次使用基于架构的表单片段，以唯一地保存每个表单片段字段的数据。 例如，您可以使用地址表片段收集地址详细信息，以便在贷款申请表中永久性、通信和显示生活地址。

![在自适应表单中使用多个片段](/help/forms/using/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> * 如果您在自适应表单中多次使用基于无的表单片段，则会在片段的字段之间同步数据。 基于核心组件的表单片段中不会出现数据同步问题，在这种情况下，您可以在表单中多次使用基于架构或基于无的片段。

## 数据绑定的片段自动映射 {#auto-mapping-of-fragments-for-data-binding}

当您使用XFA表单模板或XSD复杂类型创建自适应表单片段并将片段拖放到自适应表单时，XFA片段或XSD复杂类型会自动替换为相应的自适应表单片段，其片段模型根映射到XFA片段或XSD复杂类型。

您可以通过编辑组件对话框更改片段资源及其绑定。

>[!NOTE]
>
>您还可以从AEM内容查找器中的自适应表单片段库拖放绑定的自适应表单片段，并从自适应表单片段面板的“编辑组件”对话框中提供正确的绑定引用。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI对自适应表单片段执行多项操作。

1. 转到 `https://[hostname]:'port'/aem/forms.html`.

1. 单击 **选择** 在AEM Forms UI工具栏中，选择一个自适应表单片段。 工具栏显示您可以对选定的自适应表单片段执行的以下操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>打开</p> </td>
   <td><p>在编辑模式下打开选定的自适应表单片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>查看属性</p> </td>
   <td><p>打开属性面板。 从“属性”面板中，您可以查看和编辑属性、生成预览并上传所选片段的缩略图图像。 有关更多信息，请参阅 <a href="../../forms/using/manage-form-metadata.md" target="_blank">管理元数据</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>复制</p> </td>
   <td><p>复制选定的片段。 工具栏中会显示“粘贴”按钮。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载选定的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>预览</p> </td>
   <td><p>提供选项，用于将XML文件中的数据与片段合并，以HTML形式预览片段或自定义预览。 有关更多信息，请参阅 <a href="/help/forms/using/previewing-forms.md" target="_blank">预览表单</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>开始审核/管理审核</p> </td>
   <td><p>允许启动和管理选定片段的审核。 有关详细信息，请参阅 <a href="../../forms/using/create-reviews-forms.md" target="_blank"> 创建和管理评论 </a> 。 <br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>创建词典</p> </td>
   <td><p>生成用于本地化所选片段的字典。 有关更多信息，请参阅 <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">本地化自适应表单</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>发布/取消发布</p> </td>
   <td><p>发布/取消发布选定的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>删除</p> </td>
   <td><p>删除选定片段。 <br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 本地化包含片段的自适应表单 {#localizing-adaptive-form-containing-fragments}

要本地化包含自适应表单片段的自适应表单，您需要单独本地化片段和表单。 其目的是将片段本地化一次并在多个自适应表单中重复使用。

>[!NOTE]
>
>片段中的本地化键不会显示在自适应表单的 XLIFF 文件中。

## 使用片段时要记住的要点 {#key-points-to-remember-when-working-with-fragments}

* 确保片段名称是唯一的。 如果存在具有相同名称的现有片段，则创建片段失败。
* 在基于XDP的自适应表单中，如果您将面板另存为包含其他XDP片段的片段，则生成的片段将自动绑定到子XDP片段。 如果存在基于XSD的自适应表单，则生成的片段将绑定到架构根。
* 创建自适应表单片段时，会创建一个片段节点，该节点与CRXDe Lite中自适应表单的guideContainer节点类似。
* 不支持使用其他表单数据模型的自适应表单中的片段。 例如，基于XDP的片段在基于XSD的自适应表单中不受支持，反之亦然。
* 自适应表单片段可通过AEM内容查找器中的自适应表单片段选项卡使用。
* 通过引用插入或在自适应表单中嵌入独立自适应表单片段中的任何表达式、脚本或样式都会保留。
* 您无法从自适应表单中编辑通过引用插入的自适应表单片段。 要编辑，请编辑独立的自适应表单片段或将片段嵌入自适应表单中。
* 发布自适应表单时，您需要发布在自适应表单中通过引用插入的独立自适应表单片段。
* 重新发布更新的自适应表单片段时，更改会反映在使用片段的自适应表单已发布实例中。
* 包含验证组件的自适应表单不支持匿名用户。 此外，不 reommended 在自适应表单片段中使用验证组件。
* （ **仅** Mac）要确保表单片段功能在所有方案中都能正常工作，请将以下条目添加到/private/etc/hosts 文件中：
  `127.0.0.1 <Host machine>`**主机计算机** ：部署 AEM Forms 的 Apple Mac 计算机。

## 引用片段 {#reference-fragments}

提供了可用于创建表单的参考自适应表单片段。 有关更多信息，请参阅 [引用片段](../../forms/using/reference-adaptive-form-fragments.md).
