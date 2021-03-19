---
title: 创建表单门户页面
seo-title: 创建表单门户页面
description: Forms Portal为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
seo-description: Forms Portal为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---


# 创建表单门户页面{#creating-a-forms-portal-page}

Forms门户组件为Web开发人员提供了组件，用于在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义表单门户。 有关表单门户的快速概述，请参阅[在门户上发布表单的简介](../../forms/using/introduction-publishing-forms.md)。

## 前提条件 {#prerequisites}

Forms门户组件在默认情况下不可用。 确保按[启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)中所述启用以下表单门户组件类别。

**文档** 服务包括搜索和制表人、链接以及草稿和提交组件。

**文档服** 务谓词包括日期谓词、全文谓词、属性谓词和标记谓词组件。这些组件用于在搜索和制表人组件中配置搜索。

在AEM站点页面上启用这些组件类别后，这些组件便可在组件浏览器中使用。

![AEM Forms组件浏览器中的门户组件](assets/component-categories.png)

Forms Portal组件类别

## 搜索和制表人组件{#search-amp-lister-component}

“搜索和制表人”组件位于“文档服务”组件类别下，用于在页面上列表表单以及在列出的表单上实现搜索。 该组件包括两个窗格：

* 列表窗格。
* 添加搜索功能的搜索窗格。

您可以将“搜索和制表人”组件从组件浏览器中的“文档服务”组件类别拖放到页面上。 添加组件后，其外观与以下内容类似。

![页面中的搜索和制表人组件](assets/fp-grid-viw.png)

使用网格布局在页面中搜索和制表人组件

### 列表窗格{#list-pane}

“列表”窗格是列出表单的区域。 “搜索和制表人”组件提供了各种配置选项，可用于控制表单在“列表”窗格中的显示。

要配置列表窗格，请点按搜索和制表人组件，然后点按![settings_icon](assets/settings_icon.png)。 将打开&#x200B;**[!UICONTROL 编辑组件]**&#x200B;对话框。

![列表窗格在编辑模式下](assets/edit-list.png)

列表窗格在编辑模式下

**编辑**&#x200B;对话框包括若干选项卡，这些选项卡提供下表所述的配置选项。 完成后，点按&#x200B;**确定**&#x200B;以保存配置。

<table>
 <tbody>
  <tr>
   <th>选项卡·</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>资产文件夹</strong></code></td>
   <td>添加项目</td>
   <td>配置使用AEM Forms UI上传资产的文件夹。 默认情况下，它会列表所有上传的资产。 有关AEM Forms UI的详细信息，请参阅<a href="../../forms/using/introduction-managing-forms.md" target="_blank">管理表单简介</a>。</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>显示器</strong></code></p> </td>
   <td>标题文本</td>
   <td>搜索和制表人组件的标题。 默认标题为<strong>Forms Portal。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>资产的布局。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用高级搜索</td>
   <td>启用后，隐藏高级搜索图标。</td>
  </tr>
  <tr>
   <td> </td>
   <td>禁用文本搜索</td>
   <td>启用后，隐藏全文搜索栏。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>结果</strong></code></td>
   <td>每页结果数</td>
   <td>配置要在页面上显示的最大表单数。</td>
  </tr>
  <tr>
   <td> </td>
   <td>结果文本</td>
   <td><p>配置结果文本（例如，601 <strong>结果</strong>中的1-12）。 默认值为<strong>Results</strong>。</p> <p>例如，如果在此字段中指定<strong>Forms </strong>，并且共有601个表单，则结果文本将更改为601个<strong>Forms的1-12个。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>页面文本</td>
   <td><p>配置页面文本（例如，<strong>第</strong>1页，共51页）。 默认值为<strong>Page</strong>。</p> <p>例如，如果在此字段中指定<strong>应用程序表单</strong>，并且有51页，则页面文本将更改为<strong>应用程序表单</strong>1（共51页）。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Of 文本</td>
   <td><p>将</strong>的<strong>字替换为指定的文本（</strong>51的第1页<strong>）。 默认值为<strong>/</strong>。</strong></strong></p> <p>例如，如果在此字段中指定<strong>out of </strong>，则文本将变为</strong>51中的第1页<strong>。</strong></p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>表单链接</strong></code></td>
   <td>呈现类型</td>
   <td>根据指定的渲染类型控制表单列表。 可用选项为PDF和HTML。 例如，如果仅选择HTML作为渲染类型，则会过滤掉PDF forms。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML用户档案</td>
   <td>配置要用于渲染的HTML用户档案。 下拉用户档案中列出了所有可用的列表。</td>
  </tr>
  <tr>
   <td> </td>
   <td>提交URL</td>
   <td><p>配置提交表单数据的Servlet。</p> <p><strong>注意：</strong> <em>可以在多个位置指定表单的提交URL，其优先顺序如下：</em></p>
    <ol>
     <li><em>嵌入在表单中的提交URL（在“提交”按钮中）具有最高优先级。</em></li>
     <li><em>在AEM Forms UI中提及的提交URL具有第二高的优先级。</em></li>
     <li><em>表单门户中提及的提交URL的优先级最低。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML渲染操作工具提示</td>
   <td>配置工具提示的文本，将指针悬停在<img height="16" src="assets/aem6forms_panel-html.png" width="13" />上时显示该文本（HTML5图标）。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF渲染操作工具提示</td>
   <td>配置工具提示的文本，将指针悬停在<img height="16" src="assets/aem6forms_panel-pdf.png" width="14" />上时显示该文本（PDF图标）。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>样式</strong></code></td>
   <td>样式类型</td>
   <td>允许您指定<strong>“无样式”、“默认样式”</strong>或“<strong>自定义样式”</strong>来列出表单。</td>
  </tr>
  <tr>
   <td> </td>
   <td>自定义样式路径</td>
   <td>如果选择“自定”作为“样式类型”，请浏览以指定自定义CSS的路径，否则选择“默认”。</td>
  </tr>
 </tbody>
</table>

### 搜索窗格{#search-pane}

在“搜索”窗格中，您可以从AEM Sidekick的“文档服务谓词”类别添加日期谓词、全文谓词、属性谓词和标记谓词组件。 这些组件实现了搜索功能，以便用户对列出的表单执行搜索。

**提示：** *您可以根据预设条件控制在表单门户上显示的表单的列表，并隐藏最终用户的搜索功能。要控制表单的列表，请使用谓词组件应用搜索过滤器。 您还可以指定默认筛选器值，并从“编辑组件”对话框的“显示”选项卡中禁用搜索。*

![包含日期、全文、属性和标记谓词的搜索面板](assets/search-with-predicates.png)

包含日期、全文、属性和标记谓词的搜索面板

#### 日期谓词 {#date-predicate}

添加日期谓词组件后，可以搜索在指定持续时间内修改的列出表单。

要配置日期谓词组件，请执行以下操作：

1. 点按组件，然后点按![settings_icon](assets/settings_icon.png)。 此时将打开编辑对话框。
1. 指定以下内容：

   * **类型：** 唯一可用的选项是上次 **修改日期**

   * **文本：** 日期谓词组件的标签或题注。默认值为&#x200B;**上次修改日期。**

   * **开始日期标签：** 开始日期字段的标签或题注
   * **结束日期标签：** 结束日期字段的标签或题注
   * **隐藏：要** 强制使用默认日期过滤器来列表表单

1. 点按&#x200B;**确定**

#### 全文谓词 {#full-text-predicate}

全文谓词组件可对表单数据（如名称和说明）实现全文搜索。 用户可以搜索任何文本字符串以返回在其名称或描述中包含文本的表单。

要配置全文谓词组件，请执行以下操作：

1. 点按组件，然后点按![settings_icon](assets/settings_icon.png)。 此时将打开编辑对话框。
1. 在&#x200B;**主标题**&#x200B;字段中指定标题。
1. 点按&#x200B;**确定**

#### 属性谓词 {#properties-predicate}

“属性谓词”组件实现了根据表单属性（如标题、作者和说明）搜索表单。

要配置属性谓词组件，请执行以下操作：

1. 点按组件，然后点按![settings_icon](assets/settings_icon.png)。 此时将打开编辑对话框。
1. 在“常规”选项卡中，指定搜索标签。 默认值为&#x200B;**Properties**

1. 在“选项”选项卡中，点按&#x200B;**添加项目。**
1. 从下拉列表中选择一个属性，并在下拉列表下的字段中为它指定搜索标签。
1. 重复第4步以添加更多属性。 您还可以根据指定的条件为表单指定默认筛选器值，并隐藏属性以供最终用户搜索。 为属性选中“隐藏”复选框，然后指定默认筛选器值。
例如，如果要显示其标题中包含“Travel”的表单，请选择“标题”属性旁的“隐藏”。 此外，指定&quot;在默认筛选器值中移动&quot;文本框。

1. 点按&#x200B;**确定**

#### 标记谓词 {#tags-predicate}

标记谓词组件可根据Forms Manager中定义的标记实现表单搜索。

要配置标记谓词组件，请执行以下操作：

1. 点按组件，然后点按![settings_icon](assets/settings_icon.png)。 此时将打开编辑对话框。
1. 点按“标记”字段旁边的向下箭头按钮。
1. 选择适当的标记
1. 点按&#x200B;**确定**

选定的标记会与要选择的复选框一起显示在“搜索”窗格中。 用户现在可以根据标记缩小搜索范围。

## 列表表单在页面{#list-forms-on-a-page-br}

要在页面上列表表单，请向页面添加&#x200B;**[!UICONTROL 搜索和制表人]**&#x200B;组件，并配置&#x200B;**[!UICONTROL 列表窗格]**。 要使最终用户能够使用日期、文本和标记搜索表单，请添加&#x200B;**[!UICONTROL 搜索窗格]**&#x200B;组件。

要从页面上的任意位置链接表单，请使用链接组件。 有关链接组件的详细信息，请参阅[在页面](../../forms/using/embedding-link-component-page.md)中嵌入链接组件。

要列表处于草稿状态的表单和已提交的表单，请使用&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;组件。 有关详细信息，请参阅[自定义草稿和提交组件](../../forms/using/draft-submission-component.md)。

## 移动设备友好性{#mobile-device-friendliness}

Forms Portal Search &amp; Lister组件对移动设备友好，并相应调整。 所有三个默认视图:网格、卡、面板根据打开网站的设备重新发布，但网页也会调整。 简单的事实是，Search &amp; Lister仅是一个组件，不控制页面级别样式。

下图描述了在移动设备上打开时的“搜索和制表人”组件：

![搜索和制表人组件的屏幕截图](assets/search_lister.png)

搜索和制表人组件

## 自定义表单门户页面{#customizing-a-forms-portal-page-br}

您可以自定义表单门户页面，为页面提供不同的外观。 您还可以添加元数据以改进搜索体验、更改页面布局和添加自定义CSS样式。 有关详细信息，请参阅[自定义Forms Portal组件的模板](../../forms/using/customizing-templates-forms-portal-components.md)。

AEM Forms UI允许您向表单添加自定义元数据。 自定义元数据对于向最终用户提供列表和搜索表单体验非常有用。 有关自定义元数据的详细信息，请参阅[自定义Forms Portal组件的模板](../../forms/using/customizing-templates-forms-portal-components.md)。

开箱即用的表单门户提供渲染操作。 您可以自定义表单门户以添加更多操作。 有关详细信息，请参阅[添加对表单制表人项目的自定义操作。](../../forms/using/add-custom-action-form-lister.md)

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列表表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
