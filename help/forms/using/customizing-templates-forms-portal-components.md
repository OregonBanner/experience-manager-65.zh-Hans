---
title: 自定义表单门户组件的模板
description: AEM Forms用户界面允许用户向表单添加元数据。 自定义元数据可增强用户在表单列表和搜索贵组织时的体验。
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# 自定义表单门户组件的模板{#customizing-templates-for-forms-portal-components}

## 前提条件 {#prerequisites}

[管理表单元数据](../../forms/using/manage-form-metadata.md)

HTML和CSS工作知识

## 概述 {#overview}

通过AEM Forms用户界面，可将元数据添加到任何表单。 自定义元数据可增强用户在列出和搜索组织表单时的体验。

Forms Portal允许您在表单列表中使用自定义元数据。 在为资源创建自定义模板时，您可以修改其布局并在CSS样式集中使用自定义元数据。

执行以下步骤，为各种Forms Portal组件创建自定义模板。

## 创建自定义模板 {#creating-a-nbsp-custom-template}

1. 在/apps下创建sling：Folder节点

   添加“fpContentType”属性。 根据要为其定义自定义模板的组件，为属性指定适当的值。

   * 搜索和列表程序组件：&quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交组件：

      * 草稿部分： /libs/fd/fp/draftsTemplate
      * 提交部分：/libs/fd/fp/submissionsTemplate

   * 链接组件： /libs/fd/fp/linkTemplate

   添加要在选择布局模板时显示的标题。

   >[!NOTE]
   >
   >标题可以不同于您创建的sling：Folder的节点名称。

   下图描述了Search &amp; Lister组件的配置。
   ![创建sling：Folder](assets/1.png)

1. 在此文件夹中创建一个文件template.html作为自定义模板。
1. 编写自定义模板并使用如下所述的自定义元数据。

## 工作示例 {#working-example}

以下是自定义模板的示例实现，其中Forms Portal为Search &amp; Lister组件获取了自定义Geometrixx政府卡布局。

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

任何Forms Portal组件的自定义模板都包含可重复和不可重复条目。 可重复条目是用于列出的基本实体。 可重复条目的示例包括Search &amp; Lister、Drafts &amp; Submissions和Link组件。

Forms Portal为占位符提供了一个语法以显示自定义/OOTB元数据。 占位符在显示表单、草稿或提交的结果之后填充。

要包含可重复条目，请配置属性的值 **数据可重复** 到 **true**.

*在所讨论的示例中，自定义模板的顶部存在两个Div元素。 第一个带有“__FP_boxes-container”CSS类，可用作所列出表单的容器元素。 第二个具有“__FP_boxes”CSS类的模板用于基本实体，在本例中为“表单”。 此&#x200B;**数据可重复**Div元素中存在的属性具有值&#x200B;**true**.*

每个占位符都有一个专用的OOTB元数据集。 要在表单上的特定位置显示自定义元数据，请添加 **${metadata_prop} 属性** 在那个地方。

*在此示例中，元数据属性在多个实例中使用。 例如，它用于&#x200B;**描述**，**name**，**formUrl**，**htmlStyle**，**pdfUrl**，**pdf样式**、和&#x200B;**路径**按照规定的方式进行。*

## 开箱即用的元数据 {#out-of-the-box-metadata}

各种Forms Portal组件提供了一组排他性的OOTB元数据，您可以将这些元数据用于列出。

### 搜索和列表组件 {#search-amp-lister-component}

* **标题：** 表单标题
* **name**：表单名称（大多与标题相同）
* **描述**：表单描述
* **formUrl**：用于将表单渲染为HTML的URL
* **pdfUrl**：用于将表单渲染为PDF的URL
* **资产类型**：资源的类型。 有效值包括 **表单**，**PDF表单**， **打印表单**、和 **自适应表单**

* **htmlStyle**&#x200B;和 **pdf样式**：分别用于呈现的HTML图标和PDF图标的显示样式。 有效值为&#39;&#39;**__FP_display_none**”或空白。

>[!NOTE]
>
>切记在自定义样式表中使用__FP_display_none类。

* **downloadUrl**：用于下载资产的URL。

支持本地化、排序和使用用户界面上的配置属性（仅限搜索和列表程序）：

1. **本地化支持**：要本地化任何静态文本，请使用属性 `${localize-YOUR_TEXT}` 并使本地化的值可用（如果尚不存在）。
   *在所讨论的示例中，属性 `${localize-Apply}` 和 `${localize-Download}` 用于本地化“应用”和“下载”文本。*

1. **支持排序**：单击HTML元素可对搜索结果排序。 要在表格布局中实施排序，请在特定表标题上添加“data-sortKey”属性。 此外，添加其值作为要排序的元数据。
例如，对于网格视图中的“Title”标头，“data-sortKey”标头的值为“title”。 单击标题可对特定列中的值进行排序。

1. **使用配置属性**：搜索和列表组件具有多种可在用户界面中使用的配置。 例如，要显示通过“编辑”对话框保存的HTML工具提示文本，请使用 `${config-htmlLinkText}` 属性。 **同样，对于PDF工具提示文本，请使用** `${config-pdfLinkText}` 属性。

### 链接组件 {#link-component}

* **标题：** 表单标题
* **formUrl**：用于将表单渲染为HTML的URL
* **目标**：链接的目标属性。 有效值为“_blank”和“_self”。
* **linkText**：链接标题

### 草稿和提交组件 {#drafts-amp-submissions-component}

* **路径**：草稿/提交元数据节点的路径。 将其与。HTML扩展名一起用作打开草稿或提交的URL。
* **contextpath**：AEM实例的上下文路径
* **首字母**：保存为草稿或提交的自适应表单标题的第一个字母（大写）。
* **formName**：自适应表单的标题，已另存为草稿或已提交。
* **draftID**：列出的草稿的ID（仅在草稿部分的模板中使用）。
* **submitID**：列出的提交的ID（仅用于提交部分的模板中）。
* **状态**：已提交表单的状态。 （仅在“提交”部分的模板中使用）。
* **描述**：与草稿或提交关联的自适应表单的描述。
* **diffTime**：当前时间和草稿的最后一次保存操作之间的差异。 或者，显示当前时间和上次提交操作的提交时间之差。
* **图标类**：用于显示草稿/提交内容的第一字母的CSS类。 Forms Portal包含以下类，这些类提供各种不同颜色的背景。
* **所有者**：创建草稿/提交的用户。
* **今天**：在DD中创建草稿或提交文件的日期:MM:yyyy格式。
* **TimeNow**：在HH中创建草稿或提交文件的时间:MM:SS 24小时格式

*注意:*

1. 对于“草稿和提交”组件下“草稿”部分中的删除选项，请将CSS类命名为“__FP_deleteDraft”。 此外，还包含属性“draftID”和值 **${draftID}**，即相应草稿的草稿ID。

1. 在创建链接以打开草稿和提交时，您可以指定 **${path}.html** 作为 **href** 定位标记的属性。

![草稿和提交节点](assets/raw-image-with-index.png)

**A**. 容器元素

**B.** 具有固定层级的“路径”元数据，用于获取为每个表单存储的缩略图。

**C.** 用于每个表单的模板部分的数据可重复属性

**D.** 要本地化“应用”字符串

**E.** 使用配置属性pdfLinkText

**F.** 使用“pdfUrl”元数据

## 提示、技巧和已知问题 {#tips-tricks-and-known-issues}

1. 请勿在任何自定义模板中使用单引号(&#39;)。
1. 对于自定义元数据，请将此属性存储在 **jcr：content/metadata** 仅节点。 如果将其存储在任何其他位置，Forms Portal将无法显示元数据。
1. 确保任何自定义元数据或现有元数据的名称不包含冒号( ： )。 如果是，则无法在用户界面上显示它。
1. **数据可重复** 对于以下任何项目没有任何意义： **链接** 组件。 Adobe建议您避免在链接组件的模板中使用此属性。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出网页上的表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)
