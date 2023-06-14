---
title: 使用xtype（经典UI）
description: 了解AEM可用的所有xtype
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 0%

---

# 使用xtype（经典UI）{#using-xtypes-classic-ui}

本页介绍了Adobe Experience Manager (AEM)中可用的所有xtype。

在ExtJS语言中，xtype是给类指定的符号名称。 您可以阅读的“组件XTypes”段落 [ExtJS 2概述](https://www.sencha.com/learn/overview-of-extjs-2) ，详细了解xtype是什么及其使用方式。

有关AEM中所有可用小部件的完整信息，请参阅 [构件API文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

要了解在AEM中使用了给定xtype的组件，您可以在CRXDE中使用以下Xpath查询，方法是将“checkbox”替换为您感兴趣的xtype：

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>本页介绍在经典UI中ExtJS xtype的使用。
>
>Adobe建议您采用标准、现代、 [触屏优化UI](/help/sites-developing/touch-ui-concepts.md) 基于 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

请在下面找到Adobe Experience Manager中可用的xtype列表：

* 注释

  [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

  “对话框”是一种特殊类型的窗口，正文中有一个表单，页脚中有一个按钮组。 它通常用于编辑内容，但也可以只显示信息。

* 数组存储

  [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

  以前称为“SimpleStore”。

  用于创建的小帮助程序类 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)从阵列数据更轻松。 ArrayStore将自动配置 [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

  [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

  DAM管理中使用的资产编辑器。

* assetreferencesearchdialog

  [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

  AssetReferenceSearchDialog是一个对话框，在页面引用资产或标记时会弹出该对话框。

* blueprintconfig

  [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

  BlueprintConfig提供了一个面板，用于查看Blueprint的活动副本并编辑此Blueprint属性（同步触发器和同步操作）。

* blueprintstatus

  [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

  BlueprintStatus提供了一个面板来查看和编辑Blueprint及其活动副本关系。 浏览是通过 [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)，编辑通过 [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) 和a [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* 框

  [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

  任何的基类 [组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 即按框大小，使用宽度和高度。

  BoxComponent为调整大小和定位提供了自动的框模型调整，并且将在组件渲染模型中正常工作。

* browsedialog

  [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

  BrowseDialog允许用户浏览存储库以选择路径。 它通常通过 [浏览字段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

  [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

  **已弃用：使用 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 相反**

* bulkeditor

  [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

  BulkEditor提供了用于编辑搜索结果的搜索引擎和网格。

  BulkEditor必须插入HTML表单中（导入功能所必需的）。 这完全适用于 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

  [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

  BulkEditorForm提供 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) 被HTML表单包围。 这是 [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)，导入按钮需要HTML表单。

* 按钮

  [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

  简单按钮类

* 按钮组

  [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

  一组按钮的容器。

* 图表

  [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

  CQ.Ext.chart包提供了使用基于Flash的图表实现数据可视化的功能。 每个图表都直接绑定到CQ.Ext.data.Store，从而启用图表的自动更新。 要更改图表的外观，请参阅 [图表样式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 和 [额外样式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 配置选项。

* 复选框

  [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

  单个复选框字段。 可用作传统复选框字段的直接替代。

* 复选框组

  [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

  分组容器 [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) 控件。

* clearcombo

  [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

  ClearableComboBox是一个不可编辑的组合框，带有用于清除其值的触发器。

* colorfield

  [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

  ColorField允许用户直接或使用 [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

  [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

  ColorList允许用户从可编辑列表中选择颜色。

* 颜色菜单

  [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

  包含 [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) 组件。

* 调色板

  [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

  用于选择颜色的简单调色板类。 面板可以渲染到任何容器。

* 组合

  [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

  支持自动完成、远程加载、寻呼和许多其他功能的组合框控件。

  ComboBox的工作方式与传统HTML类似 &lt;select> 字段。 不同之处在于 [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)，您必须指定 [隐藏名称](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 创建隐藏输入。

* 组件

  [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

  所有外部组件的基类。 组件的所有子类都可参与创建、渲染和销毁的自动化外部组件生命周期，该生命周期由 [容器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 类。 组件可以通过添加到容器中 [个项目](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 创建容器时的配置选项。

* componentextracter

  [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

  ComponentExtractor允许用户从网站/页面提取组件。

* 组件选择器

  [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

  可用组件的分组、有序选择。

* 组件样式

  [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

  [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

  基于面板的复杂表单字段的基类，包括一个表单字段或一组表单字段。

* 容器

  [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

  任何的基类 [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 可能包含其他组件的组件。 容器处理包含项目的基本行为，即添加、插入和删除项目。

  最常用的容器类包括 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)， [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 和 [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

  [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

  ContentFinder是一个专门化的两列 [视区](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) 左侧包含实际的Content Finder ，右侧包含内容框架。

* contentfindertab

  [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

  ContentFinderTab是一个专用面板，提供了在的选项卡面板中使用的功能。 [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). 通常，它配有搜索表单（查询框）和用于显示搜索的数据视图。

* cq.workflow.model.combo

  [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

  工作流模型组合是自定义的 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 其中显示了可用工作流模型的列表。

* cq.workflow.model.selector

  [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

  WorkflowModelSelector将WorkflowModelCombo与工作流的缩略图图像以及创建和编辑工作流模型的按钮组合在一起。

* createsitesizard

  [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

  CreateSiteWizard是创建(MSM)站点的分步向导。

* createversiondialog

  [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

  CreateVersionDialog是一个允许创建新版本页面的对话框。

* customcontentpanel

  [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

  CustomContentPanel是一种特殊类型的面板，用于 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)：其内容可从不同的URL检索并提交给对话框中的其他字段。

* 循环

  [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

  包含菜单的专用SplitButton [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) 元素。 单击时，按钮将自动循环显示每个菜单项，从而提升按钮的 [更改](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 事件(或调用按钮的 [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 函数（如果提供）。

* 数据视图

  [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

  一种使用自定义布局模板和格式显示数据的机制。 数据视图使用 [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) 作为其内部模板机制，并绑定到 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 以便当存储区中的数据发生变化时，视图会自动更新以反映这些变化。

* datefield

  [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

  提供带有以下内容的日期输入字段 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 下拉列表和自动日期验证。

* 日期菜单

  [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

  包含 [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) 组件。

* 日期选取器

  [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

  弹出日期选取器。 此类由 [日期字段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 类，允许浏览和选择有效日期。

* datetime

  [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

  DateTime允许用户通过组合输入日期和时间 [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) 和 [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* 对话框

  [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

  “对话框”是一种特殊类型的窗口，正文中有一个表单，页脚中有一个按钮组。 它通常用于编辑内容，但也可以只显示信息。

* dialogfieldset

  [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

  DialogFieldSet [字段集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) 在中使用 [对话框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

  [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

  用于创建 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) 配置了 [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) 和 [cq.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) 与进行交互 [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) 服务器端 [提供商](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) 更简单。

* displayfield

  [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

  未验证且未提交的仅用于显示的文本字段。

* 编辑栏

  [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

  EditBar允许用户使用栏上的按钮编辑内容。

  虽然此处未列出，但EditBar具有 [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* 编辑器

  [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

  一个基本编辑器字段，可根据需要处理显示/隐藏操作，并具有一些内置的大小和事件处理逻辑。

* editorgrid

  [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

  此类扩展 [GridPanel类](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 提供选定单元格的编辑功能 [列](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). 可编辑列通过提供 [编辑者](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 在 [列配置](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* 编辑滚动

  [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

  “编辑”“变换”允许用户通过双击编辑内容，并通过上下文菜单提供更多编辑操作。 当鼠标滚动到内容上方时，可编辑区域以框架表示。

* feedimporter

  [cq.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

  FeedImporter允许用户导入RSS或Atom信息源，并为每个信息源条目创建页面。

* 字段

  [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

  提供默认事件处理、大小调整、值处理和其他功能的表单字段的基类。

* 字段集

  [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

  用于将物料分组到的标准容器 [表单](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)....

* fileuploaddialogbutton

  [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

  FileUploadDialogButton创建一个按钮，用于打开通过FileUploadField上传文件的新对话框。 可以在编辑对话框内使用，上传必须以单独的表单进行。

* fileuploadfield

  [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

  FileUploadField允许用户选择要上载的单个文件。

* findreplacedialog

  [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

  FindReplaceDialog是一个用于在页面及其子页面中查找和替换令牌的对话框。

* 闪光灯

  [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* 网格

  [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

  此类表示基于组件的网格控件的主界面，以表格形式的行和列表示数据。

* groupingstore

  [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

  一种专门的存储实施，它提供按可用字段之一对记录进行分组。 这通常与 [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) 以证明已分组的GridPanel的数据模型。

* heavymovedialog

  [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

  HeavyMoveDialog是用于移动页面及其子页面的对话框，也考虑重新激活之前激活的页面（“繁重”移动）。

* 隐藏

  [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

  一个基本隐藏字段，用于在需要在表单提交中传递的表单中存储隐藏值。

* 历史按钮

  [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

  HistoryButton是一个小型帮助程序类，可轻松提供后退和前进按钮。 通常需要两个相关的实例：前进按钮实例是一个链接到后退按钮实例的简单按钮，用于处理历史记录。

* htmleditor

  [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

  提供轻量级HTML编辑器组件。 Safari不支持某些工具栏功能，这些功能将在需要时自动隐藏。 在适用的情况下，这些选项会在配置选项中注明。

  编辑器的工具栏按钮在 [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) 属性。

* iframedialog

  [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

  一个简单的对话框，其中显示iframe的内容并允许iframe中的表单。

* iframepanel

  [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

  包含iframe的面板。 可轻松创建iframe、iframe加载事件和访问iframe的内容。

* inlinetextfield

  [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

  InlineField是一个文本字段，当焦点不在时显示为标签。

* jsonstore

  [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

  用于创建的小帮助程序类 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)从JSON数据更轻松。 JsonStore将自动配置 [cq.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* 标签

  [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

  基本标签字段。

* languagecopydialog

  [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

  LanguageCopyDialog是用于复制语言树的对话框。

* linkchecker

  [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

  LinkChecker是一种检查站点中外部链接的工具。

* listview

  [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

  CQ.Ext.list.ListView是 [网格](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 喜欢视图。

* livecopyproperties

  [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

  LiveCopyProperties提供了一个面板，用于查看和编辑Live Copy属性（关系继承、同步触发器和同步操作）。

* lvbooleancolumn

  [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

  呈现布尔数据字段的列定义类。 请参阅 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 配置选项 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 了解更多详细信息。

* 左列

  [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

  此类封装列配置数据，以便在初始化 [列表视图](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

  [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

  根据默认区域设置或配置的呈现传递日期的列定义类 [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). 请参阅 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 配置选项 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 了解更多详细信息。

* lvnumbercolumn

  [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

  根据ID格式呈现数值数据字段的Column定义类 [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 字符串。 请参阅 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 配置选项 [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 了解更多详细信息。

* mediabrowsedialog

  [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

  **已弃用：使用 [内容查找器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) 以浏览介质。**

  MediaBrowseDialog是用于浏览媒体库的对话框。

* 菜单

  [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

  菜单对象。 这是可向其添加菜单项的容器。 当您希望基于其他组件(例如 [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 例如)。

  菜单可能包含 [菜单项](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)、或常规 [组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* menubaseitem

  [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

  呈现到菜单中的所有项目的基类。 BaseItem提供默认渲染、激活状态管理和所有菜单组件共享的基本配置选项。

* menucheckitem

  [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

  添加一个菜单项，默认情况下该菜单项包含复选框，但也可以是单选按钮组的一部分。

* menuitem

  [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

  所有需要菜单相关功能（如子菜单）且不是静态显示项目的菜单项的基类。 项扩展了的基本功能 [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) 通过添加特定于菜单的激活并单击“处理”。

* menuseparator

  [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

  在菜单中添加分隔条，用于划分菜单项的逻辑组。 通常，您要在调用add()或在项目配置中使用“ — ”添加其中之一，而不是直接创建一个。

* menutextitem

  [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

  向菜单添加静态文本字符串，通常用作标题或组分隔符。

* 元数据

  [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

  元数据提供了一组字段，用于确定例如在资产编辑器页面上使用的元数据字段所需的信息。

  它提供以下字段：

* 多字段

  [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

  MultiField是用于编辑多值属性的表单字段的可编辑列表。

* mvt

  [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

  多变量测试组件可用于定义和编辑显示为交替横幅的一组图像。 按横幅收集点进率统计数据。

* 通知收件箱

  [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

  NotificationInbox允许用户订阅WCM操作和管理通知。

* 数字字段

  [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

  提供自动击键筛选和数字验证的数字文本字段。

* offlineimporter

  [cq.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

  OfflineImporter是一种用于将Microsoft Word文档导入并转换为AEM页面的工具。 此功能允许使用文字处理器离线编辑内容。

* ownerdraw

  [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

  OwnerDraw可以包含自定义HTML代码（直接输入或从URL检索）。

* 分页

  [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

  随着记录数量的增加，浏览器渲染记录所需的时间也会增加。 分页用于减少与客户端交换的数据量。

* 面板

  [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

  面板是一个容器，具有特定的功能和结构组件，使其成为面向应用程序的用户界面的完美构建基块。

  由于面板继承自 [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* 段落引用

  [cq.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

  段落引用字段允许浏览页面并选择其中一个段落。 它由一个触发器字段和一个关联的段落浏览对话框组成。

* 密码

  [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

  密码类似于 [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) 但保留其私密值，允许用户输入敏感数据。

* pathcompletion

  [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

  **已弃用：使用 [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) 相反**

* pathfield

  [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

  PathField是一个输入字段，专为路径完成和打开按钮的路径而设计 [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) 用于浏览服务器存储库。 它还可以浏览页面段落以生成高级链接。

* 进度

  [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

  可更新的进度条组件。 进度条支持两种不同的模式：手动和自动。

  在手动模式下，您负责显示、更新(通过 [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar))，并根据需要从您自己的代码中清除进度条。 当您想要显示进度时，此方法最为合适。

* 属性网格

  [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

  一种专用网格实现，旨在模拟开发IDE中通常看到的传统属性网格。 网格中的每一行都表示某个对象的属性，并且数据作为一组名称/值对存储在中 [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

  [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

  PropertyGrid是用于显示和编辑对象属性的通用网格。

* quicktip

  [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

  @xtype quicktip可在标记中指定并由全局自动管理的用于工具提示的专用工具提示类 [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) 实例。 有关其他用法的详细信息和示例，请参阅快速提示类标头。

* 无线电

  [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

  单无线电场。 与复选框相同，但为便于自动设置输入类型而提供。 如果为组中的每个单选按钮指定相同的名称，则浏览器会自动处理单选按钮分组。

* 无线组

  [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

  分组容器 [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) 控件。

* 引用对话框

  [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

  “引用”对话框是一个用于在页面上显示引用的对话框。

* restoretreedialog

  [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

  RestoreTreeDialog是用于恢复树早期版本的对话框。

* restoreversiondialog

  [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

  RestoreVersionDialog是用于恢复页面的早期版本的对话框。

* 富文本

  [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

  富文本提供了一个表单字段，用于编辑样式化文本信息（富文本）。

  富文本组件当前提供以下功能：

* rolloutplan

  [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

  RolloutPlan提供了一个用于观看页面转出进度的对话框。 转出计划由启动 [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutwizard

  [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

  RolloutWizard提供了一个用于转出页面的向导。 转出向导启动 [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

  [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

  SearchField提供了一个搜索字段，该字段在可用于搜索存储库的下拉列表中提供结果。

* 选择

  [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

  通过选择，用户可以在多个选项之间进行选择。 这些选项可以是配置的一部分，也可以从JSON响应加载。 所选内容可以呈现为下拉列表(select)或组合框(select plus free text entry)。

* sidekick

  [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

  该Sidekick是一个浮动帮助程序，为用户提供用于页面编辑的常用工具。

* siteadmin

  [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

  SiteAdmin是一个提供WCM管理功能的控制台。

* Siteimporter

  [cq.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

  SiteImporter允许用户导入完整的网站并创建初始项目。

* sizefield

  [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

  SizeField允许用户输入宽度和高度（例如，图像的宽度和高度）。

* 滑块

  [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

  支持垂直或水平方向、键盘调整、可配置的对齐、轴单击和动画的滑块。 可以作为项目添加到任何容器中。 用法示例： ...

* 幻灯片

  [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

  幻灯片放映提供了一个组件，该组件可用于定义和编辑一组可以视为幻灯片放映的图像和图像标题。

  幻灯片放映组件基于 [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) 组件。

* smartfile

  [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

  SmartFile是一种智能文件上传程序。

  如果安装了Flash插件（版本>= 9），则使用SWFupload库执行上载，这为处理上载提供了一种便利的方法。

* smartimage

  [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

  SmartImage是一种智能图像上传程序。 它提供用于处理上传图像的工具，例如用于定义图像映射的工具和图像裁剪器。

  请注意，该组件主要设计用于单独的对话框选项卡。

* 分隔符

  [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

  用于在布局中提供可缩放的空间。

* 回旋

  [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

  旋转图标是用于数字、日期或时间值的触发器字段。 通过使用提供的上下触发器、滚轮或按键，可以增加或减少值。

* 拆分按钮

  [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

  一个拆分按钮，它提供了一个内置的下拉箭头，该箭头可以单独触发事件和按钮的默认单击事件。 通常，这将用于显示一个下拉菜单，其中为主按钮操作提供了其他选项，但任何自定义处理程序都可以提供arrowclick实施。

* 静态

  [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

  “静态”可用于显示任意文本或HTML。

* statistics

  [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

  统计信息以图表形式显示页面展示。 利用小组件，可选择期间，应显示期间的统计数据。

* 存储

  [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

  Store类封装的客户端缓存 [记录](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) 为组件提供输入数据的对象，例如 [网格面板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)，则 [组合框](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)，或 [数据视图](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* suggestfield

  [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

  SuggestField根据用户的输入为其提供建议。

* 切换器

  [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

  切换器为控制台中的标题栏提供了一个按钮组，用于在“网站”、“数字资产”、“工具”、“工作流”和“安全性”之间切换。

* tableedit

  [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

  **已弃用：使用 [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) 而是。**

* tableedit2

  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

  TableEdit2提供了用于创建表的构件。

* 表格面板

  [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

  基本选项卡容器。 TabPanels的使用方式与标准完全相同 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) 对于布局目的，但对包含子组件([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container))。

* 标记

  [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

  ```
  CQ.tagging.TagInputField
  ```

  是用于输入标记的表单构件。 它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。

* 文本区域

  [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

  多行文本字段。 可用作传统文本区域字段的直接替代，并增加了对自动调整大小的支持。

* 文本按钮

  [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

  TextButton提供了一个文本链接，该链接具有 [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

  [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

  基本文本字段。 可用作传统文本输入的直接替代项，或用作更复杂的输入控件(例如 [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) 和 [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox))。

* 缩略图

  [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* 时间字段

  [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

  提供带有时间下拉列表和自动时间验证的时间输入字段。 用法示例： ...

* 笔尖

  [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

  @xtype提示：这是的类 [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) 和 [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) 提供了所有基于提示的类所需的基本布局和定位。 此类可直接用于简单的静态定位刀尖。

* 标题分隔符

  [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

  在菜单中添加分隔条，用于划分菜单项的逻辑组。 分隔符还可以带有标题。

* 工具栏

  [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

  “基本工具栏”类。 尽管 [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) （对于工具栏）为 [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)、工具栏元素（工具栏容器的子项）可以是几乎任何类型的组件。 工具栏元素可以通过其构造函数显式创建。

* 工具提示

  [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

  一种标准工具提示实施，用于在将鼠标悬停在目标元素上时提供其他信息。 @xtype工具提示。

* treegrid

  [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

  @xtype treegrid

* 树皮素

  [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

  TreePanel提供树结构数据的树结构UI表示形式。

  [树节点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)添加到TreePanel的可以每个都包含应用程序在其 [属性](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) 属性。

* 触发器

  [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

  为TextFields提供了一个方便的包装器，用于添加可单击的触发器按钮（默认情况下看起来像组合框）。 触发器没有默认操作，因此您必须通过覆盖来分配一个函数以实施触发器点击处理程序 [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). 您可以直接创建TriggerField，因为它呈现的方式与组合框完全相同。

* 上传

  [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

  UploadDialog允许用户将文件上传到存储库创建新的UploadDialog。

* 用户信息

  [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

  工具栏项，以显示当前用户名并允许用户操作，如编辑用户属性和模拟。

* 视区

  [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

  表示可查看的应用程序区域（浏览器视区）的专用容器。

  视区将其自身呈现到文档正文中，并自动将其自身大小调整为浏览器视区的大小并管理窗口大小调整。 只能创建一个视区。

* 窗口

  [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

  专门用作应用程序窗口的面板。 Windows是浮动的， [可调整大小](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)、和 [可拖动](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 默认情况下。 Windows可以 [最大化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) 以填充视区，恢复为原来的大小，并可以 [最小化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

  [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

  用于创建的小帮助程序类 [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)从XML数据更轻松。 XmlStore将自动配置 [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

  **cqinclude** 包含来自存储库中不同路径的小组件定义的伪xtype。 它最常用于页面对话框。 此xtype没有实际的JavaScript构件类。 它由CQ.Util类的formatData()函数处理。 有关更多信息，请参阅此知识库文章。
