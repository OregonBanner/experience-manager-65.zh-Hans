---
title: 自定义表单门户组件的模板
seo-title: 自定义表单门户组件的模板
description: 在表单列表中显示自定义元数据
seo-description: 在表单列表中显示自定义元数据
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# 自定义表单门户组件的模板{#customizing-templates-for-forms-portal-components}

## 前提条件 {#prerequisites}

[管理表单元数据](../../forms/using/manage-form-metadata.md)

HTML和CSS的工作知识

## 概述 {#overview}

AEM Forms用户界面允许您向任何表单添加元数据。 自定义元数据可在列出和搜索组织表单时增强用户体验。

Forms门户允许您在表单列表中使用自定义元数据。 在为资产创建自定义模板时，您可以修改其布局并将自定义元数据与CSS样式集结合使用。

请执行以下步骤，为各种Forms门户组件创建自定义模板。

## Creating a custom template {#creating-a-nbsp-custom-template}

1. 在/apps下创建sling:Folder节点

   添加“fpContentType”属性。 根据要为其定义自定义模板的组件，为属性指定适当的值。

   * 搜索和制表人组件： &quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交组件：

      * 草稿部分： /libs/fd/fp/draftsTemplate
      * 提交部分： /libs/fd/fp/submissions模板
   * 链接组件： /libs/fd/fp/linkTemplate

   添加您希望在选择布局模板时显示的标题。

   >[!NOTE]
   >
   >标题可以与sling:Folder的节点名称不同。

   下图描述了“搜索和制表人”组件的配置。
   ![创建sling:Folder](assets/1.png)

1. 在此文件夹中创建一个文件template.html以用作自定义模板。
1. 编写自定义模板并使用自定义元数据，如下所述。

## 工作示例 {#working-example}

以下是自定义模板的示例实现，在该模板中，Forms门户为搜索和制表人组件获取自定义GeometrixxGov卡布局。

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## 自定义模板的技术规范 {#technical-specifications-for-custom-templates}

任何Forms门户组件的自定义模板都包括可重复和不可重复的条目。 可重复条目是列表的基本实体。 可重复条目的示例包括搜索和制表人、草稿和提交以及链接组件。

Forms门户为占位符提供显示自定义/OOTB元数据的语法。 在显示表单、草稿或提交结果后，将填充占位符。

要包含可重复的条目，请将可重复数据 **属性的值** 配置 **为true**。

*在所讨论的示例中，自定义模板的顶部有两个Div元素。 第一个CSS类具有“__FP_boxes-容器”，它用作所列表单的容器元素。 第二个具有“__FP_boxes”CSS类，是基本实体的模板，本例中为表单。 Div元&#x200B;**素中存在**的数据可重复属性的值&#x200B;**为true**。*

每个占位符都有一个独占的OOTB元数据集。 要在表单的特定位置显示自定义元数据，请 **在该位置添加${metadata** _prop}属性。

*在示例中，元数据属性用于多个实例。 例如，它以指定&#x200B;**方式**、**名称**、formUrl **、**htmlStyleUrl、****************pdfUrlPdfPdfStyle、pdfStylePad、PPathPathPath和使用。*

## 开箱即用的元数据 {#out-of-the-box-metadata}

各种Forms门户组件提供专有的OOTB元数据集，您可以使用这些元数据进行列表。

### 搜索和制表人组件 {#search-amp-lister-component}

* **标题：** 表单的标题
* **name**: 表单的名称（大多与标题相同）
* **描述**: 表单的说明
* **formUrl**: 用于将表单呈现为HTML的URL
* **pdfUrl**: 用于将表单渲染为PDF的URL
* **assetType**: 资产的类型。 有效值包 **括**“表单&#x200B;**”、“PDF**&#x200B;表单 **”、“**&#x200B;打印表单 **”和“自适应表单”**

* **htmlStyle**&#x200B;和 **pdfStyle**: 显示分别用于渲染的HTML和PDF图标的样式。 有效值&#x200B;**为“__FP_display_none**”或空。

>[!NOTE]
>
>切记在自定义样式表中使用__FP_display_none类。

* **downloadUrl**: 下载资产的URL。

支持在用户界面上本地化、排序和使用配置属性（仅限搜索和制表人）:

1. **本地化支持**: 要本地化任何静态文本，请 `${localize-YOUR_TEXT}` 使用属性并使本地化值可用（如果尚不存在）。
   *在讨论的示例中，属性`${localize-Apply}`和用`${localize-Download}`于本地化“应用”和“下载”文本。*

1. **支持排序**: 单击HTML元素对搜索结果进行排序。 要在表布局中实现排序，请在特定表标题上添加“data-sortKey”属性。 此外，将其值添加为要排序的元数据。
例如，对于网格视图中的“标题”标题，“data-sortKey”标题的值为“标题”。 单击标题可对特定列中的值进行排序。

1. **使用配置属性**: “搜索和制表人”组件具有多个可在用户界面上使用的配置。 例如，要显示通过编辑对话框保存的HTML工具提示文本，请使用属 `${config-htmlLinkText}` 性。 **同样，对于PDF工具提示文本，请使用属性**`${config-pdfLinkText}` 。

### 链接组件 {#link-component}

* **标题：** 表单的标题
* **formUrl**: 用于将表单呈现为HTML的URL
* **目标**: 链接的目标属性。 有效值为“_blank”和“_self”。
* **linkText**: 链接标题

### 草稿和提交组件 {#drafts-amp-submissions-component}

* **路径**: 草稿／提交元数据节点的路径。 将其与。HTML扩展名一起用作URL以打开草稿或提交。
* **contextPath**: AEM实例的上下文路径
* **firstLetter**: 自适应表单标题的首字母（大写），已保存为草稿或提交。
* **formName**: 自适应表单的标题，已保存为草稿或已提交。
* **draftID**: 所列草稿的ID（仅在“草稿”部分的模板中使用）。
* **submitID**: 列出的提交的ID（仅在“提交”部分的模板中使用）。
* **状态**: 已提交表单的状态。 （仅在“提交”部分的模板中使用）。
* **描述**: 与草稿或提交关联的自适应表单的说明。
* **diffTime**: 草稿的当前时间与上次保存操作之间的差异。 或者，当前时间与上次提交操作之间用于提交的时间的差异。
* **iconClass**: CSS类用于显示草稿／提交的第一个字母。 Forms门户网站包括以下各类课程，它们提供各种彩色背景。
* **所有者**: 创建草稿／提交的用户。
* **今天**: 草稿或提交的创建日期，格式为DD:MM:YYYY。
* **TimeNow**: 草稿或提交的创建时间，以HH:MM:SS 24小时格式表示

*注意:*

1. 对于“草稿和提交”组件下“草稿”部分中的删除选项，将CSS类命名为“__FP_deleteDraft”。 此外，还包含属性“draftID”，其值 **为${draftID}**，它是相应草稿的草稿ID。

1. 在创建指向打开的草稿和提交的链接时， **可以指定${path** }.html作为锚点标 **签的href** 属性的值。

![草稿和提交节点](assets/raw-image-with-index.png)

**A**. 容器元素

**B.** 具有固定层次结构的“路径”元数据，以获取为每个表单存储的缩略图。

**C.用于** 每个表单的模板部分的数据可重复属性

**D.** To localize &quot;Apply&quot;字符串

**E.使用** configuration属性pdfLinkText

**F.** 使用“pdfUrl”元数据

## 提示、技巧和已知问题 {#tips-tricks-and-known-issues}

1. 请勿在任何自定义模板中使用单引号(&#39;)。
1. 对于自定义元数据，请仅将此属性存 **储在jcr:content/metadata节** 点上。 如果将其存储在任何其他位置，Forms门户无法显示元数据。
1. 确保任何自定义元数据或现有元数据的名称不包含冒号(: )。 如果显示，则无法在用户界面上显示。
1. **data-repeatable** 对于Link组件没有任何 **意义** 。 Adobe建议您避免在链接组件的模板中使用此属性。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列表表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)