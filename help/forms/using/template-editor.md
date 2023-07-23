---
title: 自适应表单模板
seo-title: Adaptive Form Templates
description: 使用模板编辑器通过定义基本结构和初始表单内容来创建自适应表单模板。
seo-description: Create adaptive form templates by defining the basic structure and initial form content using the Template Editor.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
feature: Adaptive Forms
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 1%

---

# 自适应表单模板{#adaptive-form-templates}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/template-editor.html) |
| AEM 6.5 | 本文 |



在创作表单时，可在编辑器中添加字段和组件以定义表单结构、内容和操作。 您可以在 `guideRootPanel` 表单容器的。 使用模板编辑器，您可以创建一个模板，其中包含作者可用于创建表单的基本结构和初始内容。

例如，您希望所有表单作者在注册表单中都拥有特定的文本框、导航按钮和提交按钮。 您可以创建一个模板，其中包含作者可用来创建与其他注册表单一致的表单的组件。 当作者使用模板创建自适应表单时，新表单会继承您在模板中指定的结构和组件。 通过模板编辑器，您可以：

* 在结构层中添加表单的页眉和页脚组件。
* 提供表单的初始内容。
* 指定主题、提交操作。

## 使用模板 {#working-with-templates}

您可以从“工具”菜单导航到，访问模板编辑器 **Adobe Experience Manager >工具>模板**. 在此，模板在启用可编辑模板的文件夹中进行组织。 AEM提供了一个全局文件夹来组织模板。 但是，默认情况下不启用它。 您可以请求管理员启用全局文件夹或为模板创建新文件夹。 有关如何创建文件夹的详细信息，请参阅 [模板文件夹](/help/sites-developing/page-templates-editable.md).

点击打开文件夹后，您将找到创建按钮，该按钮允许为自适应表单创建新模板。

### 创建模板 {#create-template}

创建文件夹后，打开该文件夹并执行以下步骤以创建模板：

1. 在“模板”控制台中，点按 **创建** 在您创建的文件夹内。
1. 在“选择模板类型”部分中，选择 **自适应表单模板** 并点按 **下一个**.

1. 在模板详细信息部分，提供模板标题并点按 **创建**.
您可以提供在表单创作时可以选择所创建模板时看到的描述和缩略图。

1. 点按 **完成** 以返回到控制台，或点按 **打开** 以在编辑器中打开模板。

### 模板编辑器用户界面 {#template-editor-ui}

在打开模板进行编辑时，您可以看到以下AEM Editor组件：

* **页面工具栏**
包含以下选项：

   * **切换侧面板**：用于显示或隐藏侧栏。
   * **页面信息**：用于指定发布/取消发布时间、缩略图、客户端库、页面策略和页面设计客户端库等信息。
   * **模拟器**：用于模拟和自定义不同设备的外观。
   * **图层选择器：** 允许您更改图层。
您可以选择 **结构** 图层或 **初始内容** 图层。 结构层允许您添加和自定义页眉和页脚。 初始内容层允许您自定义表单内容。

   * **预览：** 允许您预览模板在发布时的外观。 您可以使用“图层选择器”和“预览”来切换编辑和预览模式。

* **侧栏：** 提供“内容”、“属性”、“资产”和“组件”浏览器。
* **组件工具栏：** 选择某个组件后，您将看到一个工具栏，通过该工具栏可自定义该组件。
* **页面**：添加内容以创建模板的区域。

参见 [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md) 了解触屏UI编辑器。

### 编辑模板 {#editing-a-template}

自适应表单模板使用两层创建：

* 结构
* 初始内容

图层选择器位于屏幕右上角的“预览”选项旁边。

### 结构 {#structure}

在模板编辑器中选择结构层时，您可以看到自适应表单容器的上方和下方的布局容器。 作者可以将这些布局容器用于页眉和页脚。 您可以添加、编辑或自定义页眉和页脚。 将自适应表单标题组件拖放到自适应表单容器上方的布局容器中，以自定义模板标题。 将自适应表单页脚组件拖放到自适应表单容器下的布局容器中，以自定义模板页脚。

![结构层中的布局容器](assets/header-layer-selector.png)

结构层中的布局容器

**答：** 标题组件的布局容器 **B.** 页脚组件的布局容器

将自适应表单标题组件拖放到自适应表单容器上方的布局容器中。 添加组件后，您可以指定其属性，以便添加徽标并提供其标题。

同样，将页脚组件拖放到自适应表单容器下方的布局容器中时，您可以提供版权信息和公司详细信息。

![在结构层中添加了页眉和页脚](assets/header-and-footer.png)

在结构层中添加了页眉和页脚

#### 结构层中的锁定/解锁组件 {#locking-unlocking-components-in-the-structure-layer}

在选定结构层的情况下编辑模板时，可以解锁模板的页眉和页脚。 如果在模板中解锁了组件，则表单作者可以在使用该模板的自适应表单中编辑该组件。 锁定组件会阻止表单作者在自适应表单中进行编辑。 “锁定”选项在组件工具栏中可用。

例如，在模板中添加标题组件。 选择组件后，您会在组件工具栏中看到一个锁定选项。 通常，页眉包括公司名称和徽标，并且您不希望表单作者更改模板中的徽标和页眉。 在使用模板创建的自适应表单中，标题组件处于锁定状态，表单作者无法更改徽标和公司名称。

>[!NOTE]
>
>不建议单独锁定或解锁页眉组件中的图像或徽标。 您可以解锁标头组件。

### 初始内容 {#initial-content}

选择“初始内容”选项后，模板的自适应表单容器会像要编辑的自适应表单一样打开。 与创作自适应表单一样，您可以指定初始设置，例如选择主题和提交操作。

表单作者可将其用作创建表单的基础。 内容流结构在模板的“初始内容”层中指定。 要切换到编辑表单模板的初始内容，请在页面工具栏中的预览之前，点按 ![画布下拉列表](assets/canvas-drop-down.png) **>初始内容**.
![模板编辑器中的初始内容层](assets/initial-content-layer.png)

模板编辑器中的初始内容层，显示为指定属性而选择的自适应表单容器。

![初始内容](assets/initial-content-layer-1.png)

在初始内容层中，创建作者用作基础的自适应表单模板。 创作模板与创作表单类似，只是使用侧栏中提供的选项。 侧栏提供内容、属性、资源和组件浏览器。

参见 [侧栏](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>选择“存储内容”或“存储PDF”作为“提交操作”时，您将获得一个用于指定存储路径的选项。 如果在模板中指定路径，则使用该模板创建的所有表单都具有相同的路径。 您可以指定正确的存储路径，或确保表单作者对其进行更新，以防止每个表单中的数据存储在同一位置。

#### 创建带有选项卡和面板的自适应表单模板  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

例如，要创建具有以下选项卡的模板：

* 常规信息
* 专业信息

您已添加徽标、提供标题，并在结构图层中添加了页脚。 锁定页眉和页脚，以阻止表单作者在使用模板创建表单时编辑它们。

将图层从“结构”更改为“初始内容”，然后开始将内容添加到表单中。 要创建选项卡式结构，请在自适应表单容器的guideRootPanel中添加一个子面板。 要添加面板，请执行以下操作：

* 您可以通过点按 **+** 按钮 **将组件拖动到此处** 选项。

* 您可以从组件浏览器中将面板组件拖放到侧栏中。
* 您可以添加的子面板 `guideRootPanel` （从组件工具栏）。

要创建“常规信息”和“专业信息”选项卡，请在的子面板中添加两个面板 `guideRootPanel`. 选择面板并点按 ![cmppr](assets/cmppr.png) 以打开侧栏中的属性。 将元素名称更改为 `general-info` 和 `professional-info`和职称分别作为“一般信息”和“专业信息”。 在侧栏中，点按内容以打开内容浏览器。 在表单对象选项卡中，选择 `guideRootPanel`. 在编辑器中，选择guideRootPanel。 点按 ![cmppr](assets/cmppr.png) 以打开其属性。 在“面板布局”字段中，选择 **顶部选项卡** 并点按 **完成**. 应用选项卡式模板结构。

#### 在选项卡中添加内容 {#adding-content-in-tabs}

![在自适应表单模板中添加字段](assets/template-edit-initial-content.png)

在添加面板并将其结构为选项卡后，您可以在选项卡内添加字段。 在编辑器中选择选项卡时，您会看到 **将组件拖动到此处** 选项。 您可以拖放组件，例如文本框、列表项和按钮。 您可以从侧栏中的组件浏览器拖放组件。

每个组件都具有可增强数据捕获和处理的属性。 例如，您可以启用 **必填字段** 组件的属性。 您的作者可以指定客户在跳过填写必填字段时看到的消息。 在中指定消息 **必填字段消息** 属性。

在示例模板中，“姓名”、“电话号码”和“出生日期”字段添加到“一般信息”选项卡中。 在“专业信息”选项卡中，添加了“当前雇用”、“雇佣类型”、“教育资格”字段。

添加字段后，您可以添加“提交”和“重置”等按钮。

### 启用模板 {#enabling-the-template}

创建模板时，模板会添加为草稿。 启用模板以将其用于创建自适应表单。 启用模板：

1. 导航到 **Adobe Experience Manager >工具>模板**，然后打开已在其中创建模板的文件夹。

1. 您创建的模板将标记为草稿。
1. 选择模板并点按 **启用** 工具栏中。
创建自适应表单时，如果系统要求您选择模板，您会看到模板已列出。

## 导入或导出模板 {#importing-or-exporting-a-template}

表单可与其模板配合使用。 下载使用自定义模板创建的自适应表单时，不会下载该模板。 在其他AEM Forms实例上导入表单时，表单导入时不包含其模板。 如果表单已导入，但其模板不可用，则不会呈现表单。 您可以从以下位置打包自定义模板 `/conf` 中的节点 `https://<server>:<port>/crx/packmgr`，并将其移植到要上传表单的AEM Forms实例中。

## 使用模板创建自适应表单 {#creating-an-adaptive-form-using-the-template}

创建并启用模板后，创建自适应表单时可在表单管理器中找到该模板。 要使用模板和创建自适应表单，请参阅 [创建自适应表单](../../forms/using/creating-adaptive-form.md).

## 更改现成模板的显示选项  {#change-display-option-of-out-of-the-box-templates}

您可以为自适应表单创建自定义模板，以定义基本结构和初始内容。 AEM Forms还为自适应表单提供了一组现成的模板。 您可以选择显示或隐藏模板。

执行以下步骤可显示和隐藏模板：

1. 登录到AEM Forms创作实例并导航到 **工具** > **操作** > **Web控制台**.

   >[!NOTE]
   >
   >AEM Web控制台的URL是https://&#39;[服务器]：[端口]&#39;/system/console/configMgr

1. 找到并打开 **FormsManager配置** 设置：

   * 要显示或隐藏现成的自适应表单模板，请选中或取消选中 **包括现成的AF和AD模板** 选项。
   * 要显示或隐藏在AEM 6.0 Forms或AEM 6.1 Forms版本中添加但现在已弃用的现成自适应表单模板，请选中或取消选中 **包含AEM 6.0 AF模板** 选项。 如果选中此选项，则需要 **包括现成的AF和AD模板** 要启用的配置。

1. 单击“**保存**”。现成模板的显示选项已更改。

## 推荐 {#recommendations}

* 在模板编辑器中修改表单的属性时，请勿使用BindReference属性。
* 如果要添加断点，请在创作自适应表单模板时创建断点。
有关断点的详细信息，请参见 [响应式布局](/help/sites-authoring/responsive-layout.md).
