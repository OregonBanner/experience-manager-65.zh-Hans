---
title: 创建表单门户页面
seo-title: Creating a forms portal page
description: Forms Portal为Web开发人员提供了组件，以便在使用Adobe Experience Manager (AEM)创作的网站上创建和自定义表单门户。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 2%

---

# 创建表单门户页面{#creating-a-forms-portal-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | 本文 |

Forms门户组件为Web开发人员提供了组件，以便在使用Adobe Experience Manager (AEM)创作的网站上创建和自定义表单门户。 有关表单门户的快速概述，请参阅 [在门户上发布表单的简介](../../forms/using/introduction-publishing-forms.md).

## 前提条件 {#prerequisites}

默认情况下，Forms门户组件不可用。 确保按照中的说明启用以下Forms Portal组件类别 [启用Forms Portal组件](/help/forms/using/enabling-forms-portal-components.md).

**文档服务** 包括“搜索和列表程序”、“链接”以及“草稿和提交”组件。

**文档服务谓词** 包括日期谓词、全文谓词、属性谓词和标记谓词组件。 这些组件用于在搜索和列表程序组件中配置搜索。

在AEM站点页面上启用它们后，这些组件类别即可在组件浏览器中使用。

![组件浏览器中的AEM Forms portal组件](assets/component-categories.png)

Forms portal组件类别

## 搜索和列表组件 {#search-amp-lister-component}

在Document Services组件类别下提供的“搜索和列表器”组件用于在页面上列出表单，并对列出的表单实施搜索。 该组件包括两个窗格：

* 列出表单的列表窗格。
* 搜索窗格，可在其中添加搜索功能。

您可以将搜索和列表程序组件从组件浏览器中的Document Services组件类别拖放到页面上。 添加组件后，该组件将类似于以下内容。

![页面中的Search &amp; Lister组件](assets/fp-grid-viw.png)

具有网格布局的页面中的搜索和列表组件

### 列表窗格 {#list-pane}

“列表”窗格是列出表单的区域。 搜索和列表程序组件提供了各种配置选项，可用于控制“列表”窗格中表单的显示。

要配置“列表”窗格，请选择“搜索和列表程序”组件，然后选择 ![settings_icon](assets/settings_icon.png). 此 **[!UICONTROL 编辑组件]** 对话框打开。

![编辑模式下的列表窗格](assets/edit-list.png)

编辑模式下的列表窗格

此 **编辑** 该对话框包含几个选项卡，提供了下表所述的配置选项。 选择 **确定** 以保存配置（完成时）。

<table>
 <tbody>
  <tr>
   <th>选项卡</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>资源文件夹</strong></code></td>
   <td>添加项目</td>
   <td>配置使用AEM Forms UI上传资源的文件夹。 默认情况下，其中列出了所有上传的资源。 有关AEM Forms UI的更多信息，请参阅 <a href="../../forms/using/introduction-managing-forms.md" target="_blank">管理表单简介</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>显示器</strong></code></p> </td>
   <td>标题文本</td>
   <td>Search &amp; Lister组件的标题。 默认标题为 <strong>Forms门户。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>资源的布局。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用高级搜索</td>
   <td>启用后，将隐藏高级搜索图标。</td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用文本搜索</td>
   <td>启用后，将隐藏全文搜索栏。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>结果</strong></code></td>
   <td>每页结果数</td>
   <td>配置要在页面上显示的最大表单数。</td>
  </tr>
  <tr>
   <td> </td>
   <td>结果文本</td>
   <td><p>配置结果文本（例如，601的1-12） <strong>结果</strong>)。 默认值为 <strong>结果</strong>.</p> <p>例如，如果您指定 <strong>Forms </strong>在此字段中共有601个表单，结果文本更改为601个中的1-12个 <strong>Forms。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>页面文本</td>
   <td><p>配置页面文本(例如， <strong>页面 </strong>1/51)。 默认值为 <strong>页面</strong>.</p> <p>例如，如果您指定 <strong>申请表 </strong>在此字段中且共有51页，页面文本将更改为 <strong>申请表 </strong>1/51。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Of 文本</td>
   <td><p>替换单词 <strong>之</strong> 指定文本（第1页） <strong>之 </strong>51)。 默认值为 <strong>之</strong>.</p> <p>例如，如果您指定 <strong>/ </strong>在此字段中，文本将更改为第1页 <strong>/ </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>表单链接</strong></code></td>
   <td>呈现类型</td>
   <td>根据指定的渲染类型控制表单的列表。 可用的选项包括PDF和HTML。 例如，如果选择“仅HTML”作为渲染类型，则会过滤掉PDF forms。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML配置文件</td>
   <td>配置用于渲染的HTML配置文件。 下拉列表中列出了所有可用的配置文件。</td>
  </tr>
  <tr>
   <td> </td>
   <td>提交URL</td>
   <td><p>配置提交表单数据的servlet。</p> <p><strong>注意：</strong> <em>可以在多个位置指定表单的提交URL，其优先顺序如下：</em></p>
    <ol>
     <li><em>表单中嵌入的提交URL（在提交按钮中）具有最高优先级。</em></li>
     <li><em>AEM Forms UI中提到的提交URL具有第二高优先级。</em></li>
     <li><em>Forms Portal中提到的提交URL的优先级最低。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML渲染操作工具提示</td>
   <td>配置工具提示的文本，当鼠标悬停在指针上方时，将显示该文本 <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML5图标)。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF渲染操作工具提示</td>
   <td>配置工具提示的文本，当鼠标悬停在指针上方时，将显示该文本 <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF图标)。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>样式</strong></code></td>
   <td>样式类型</td>
   <td>可让您指定 <strong>无样式，默认样式</strong>，或 <strong>自定义样式 </strong>以列出表单。</td>
  </tr>
  <tr>
   <td> </td>
   <td>自定义样式路径</td>
   <td>如果选择“自定义”作为“样式类型”，请浏览以指定自定义CSS的路径，否则选择“默认”。</td>
  </tr>
 </tbody>
</table>

### 搜索窗格 {#search-pane}

“搜索”窗格允许您从AEM Sidekick中的“文档服务谓词”类别添加“日期谓词”、“全文谓词”、“属性谓词”和“标记谓词”组件。 这些组件为用户实施搜索功能以对列出的表单执行搜索。

**提示：** *您可以根据预设条件控制表单门户上显示的表单列表，并为最终用户隐藏搜索功能。 要控制表单列表，请使用谓词组件应用搜索过滤器。 您还可以指定默认筛选器值，并从“编辑组件”对话框的“显示”选项卡中禁用搜索。*

![具有日期、全文、属性和标记谓词的搜索面板](assets/search-with-predicates.png)

具有日期、全文、属性和标记谓词的搜索面板

#### 日期谓词 {#date-predicate}

添加日期谓词组件后，可以搜索在指定持续时间内修改的已列出表单。

配置日期谓词组件：

1. 选择组件，然后选择 ![settings_icon](assets/settings_icon.png). 将打开“编辑”对话框。
1. 指定以下内容：

   * **类型：** 唯一可用的选项是 **上次修改日期**

   * **文本：** 日期谓词组件的标签或标题。 默认值为 **上次修改日期。**

   * **开始日期标签：** 开始日期字段的标签或标题
   * **结束日期标签：** 结束日期字段的标签或标题
   * **隐藏：** 要强制使用默认日期过滤器来列出表单，请执行以下操作

1. 选择 **确定**

#### 全文谓词 {#full-text-predicate}

全文谓词组件对表单数据（如名称和描述）实施全文搜索。 用户可以搜索任何文本字符串以返回其名称或描述中包含文本的表单。

配置全文谓词组件：

1. 选择组件，然后选择 ![settings_icon](assets/settings_icon.png). 将打开“编辑”对话框。
1. 在中指定标题 **主标题** 字段。
1. 选择 **确定**

#### 属性谓词 {#properties-predicate}

属性谓词组件实现了基于表单属性（如标题、作者和描述）的表单搜索。

配置属性谓词组件：

1. 选择组件，然后选择 ![settings_icon](assets/settings_icon.png). 将打开“编辑”对话框。
1. 在“常规”选项卡中，指定搜索标签。 默认值为 **属性**

1. 在选项选项卡中，选择 **添加项目。**
1. 从下拉列表中选择一个属性，并在下拉列表下方的字段中为其指定搜索标签。
1. 重复步骤4以添加更多属性。 您还可以指定默认筛选器值，以根据指定的条件列出表单并隐藏属性以供最终用户搜索。 选中属性的“隐藏”复选框，并指定默认筛选值。
例如，如果要显示标题中包含“Travel”的表单，请选择“标题”属性旁边的“隐藏”。 此外，在默认筛选值文本框中指定Travel。

1. 选择 **确定**

#### 标记谓词 {#tags-predicate}

标记谓词组件基于Forms Manager中定义的标记实施表单搜索。

配置标记谓词组件：

1. 选择组件，然后选择 ![settings_icon](assets/settings_icon.png). 将打开“编辑”对话框。
1. 选择“标记”字段旁边的向下箭头按钮。
1. 选择相应的标记
1. 选择 **确定**

选定的标记与用于选择的复选框一起出现在“搜索”窗格中。 用户现在可以根据标记缩小搜索范围。

## 在页面上列出表单 {#list-forms-on-a-page-br}

要在页面上列出表单，请添加 **[!UICONTROL 搜索和列表程序]** 页面组件并配置 **[!UICONTROL 列表窗格]**. 要使最终用户能够搜索包含日期、文本和标记的表单，请添加 **[!UICONTROL 搜索窗格]** 组件。

要从页面上的任何位置链接表单，请使用链接组件。 有关链接组件的详细信息，请参见 [在页面中嵌入链接组件](../../forms/using/embedding-link-component-page.md).

要列出处于草稿状态的表单和已提交的表单，请使用 **[!UICONTROL 草稿和提交]** 组件。 有关更多信息，请参阅 [自定义草稿和提交组件](../../forms/using/draft-submission-component.md).

## 移动设备的友好性 {#mobile-device-friendliness}

Forms Portal Search &amp; Lister组件适合移动设备使用，可相应地进行调整。 所有三种默认视图：网格、卡片、根据站点打开设备重新布局面板，并且网页也会适应。 一个简单的事实是，“搜索和列表程序”只是一个组件，它不控制页面级别的样式。

下图描述在移动设备上打开搜索与列表程序组件时的情况：

![Search and Lister组件的屏幕截图](assets/search_lister.png)

搜索和列表组件

## 自定义表单门户页面 {#customizing-a-forms-portal-page-br}

您可以自定义表单门户页面，为页面提供独特的外观。 您还可以添加元数据以改善搜索体验、更改页面布局以及添加自定义CSS样式。 有关更多信息，请参阅 [自定义Forms Portal组件的模板](../../forms/using/customizing-templates-forms-portal-components.md).

AEM Forms UI允许您将自定义元数据添加到表单。 自定义元数据在向最终用户提供列表和搜索表单体验时非常有用。 有关自定义元数据的详细信息，请参阅 [自定义Forms Portal组件的模板](../../forms/using/customizing-templates-forms-portal-components.md).

forms portal开箱即用地提供渲染操作。 您可以自定义表单门户以添加更多操作。 有关详细信息，请参阅 [正在添加针对表单列表程序项目的自定义操作。](../../forms/using/add-custom-action-form-lister.md)

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出网页上的表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
