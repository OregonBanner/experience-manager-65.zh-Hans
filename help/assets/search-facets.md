---
title: 搜索彩块化以过滤搜索结果
description: 如何在 [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2417'
ht-degree: 17%

---

# 搜索 Facet {#search-facets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=en) |
| AEM 6.5 | 本文 |

在企业范围内部署 [!DNL Adobe Experience Manager Assets] 具有存储多个资产的能力。 有时，如果您仅使用 [!DNL Experience Manager].

使用“过滤器”面板中的搜索彩块化，为您的搜索体验添加更多粒度，并使搜索功能更高效、更通用。 搜索彩块化可添加多个维度（谓词），以便您执行更复杂的搜索。 “过滤器”面板包含一些标准Facet。 您还可以添加自定义搜索彩块化。

总之，搜索彩块化允许您以多种方式而不是按单个预先确定的分类顺序来搜索资产。 您可以轻松地向下展开到所需的详细信息级别，以便进行更集中的搜索。

例如，如果要查找图像，则可以选择想要位图还是矢量图像。 您可以通过为图像指定MIME类型，进一步缩小搜索范围。 同样，在搜索文档时，可以指定格式，例如PDF或MS Word。

## 添加谓词 {#adding-a-predicate}

“筛选器”面板中显示的搜索彩块化在基础搜索表单中使用谓词进行定义。 要显示更多或不同的Facet，您可以向默认表单中添加谓词，或使用包含您选择的Facet的自定义表单。

对于全文搜索，请将 **[!UICONTROL 全文]** 谓词。 使用属性谓词，可搜索与您指定的单个属性匹配的资产。 使用“选项”谓词，可搜索与特定属性的一个或多个值匹配的资产。 添加“日期范围”谓词，以搜索在指定日期范围内创建的资产。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索Forms]**.
1. 从 [!UICONTROL 搜索Forms] 页面，选择 **[!UICONTROL 资产管理搜索边栏]**，然后单击 **[!UICONTROL 编辑]** ![编辑图标](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >使用预配置的 [!DNL Assets] 早期版本中的“管理搜索边栏”，请执行以下步骤：
   >
   >1. 导航到 `/conf/global/settings/dam/search/facets/assets/jcr:content/items` 在CRXDE中。
   >1. 删除 `type` 节点。
   >1. 从路径 `/libs/settings/dam/search/facets/assets/jcr:content/items`，复制节点 `asset`, `directory`, `typeor`, `excludepaths`和 `searchtype` 路径。
   >1. 保存更改。


1. 在 [!UICONTROL 编辑搜索Forms] ，请从 **[!UICONTROL 选择谓词]** 选项卡。 例如，拖动 **[!UICONTROL 属性谓词]**.

   ![选择和移动谓词以自定义搜索过滤器](assets/drag_predicate.png)

   *图：选择和移动谓词以自定义搜索过滤器。*

1. 在 [!UICONTROL 设置] 选项卡，输入谓词的字段标签、占位符文本和描述。 为要与谓词关联的元数据属性指定有效名称。 中的标题标签 [!UICONTROL 设置] 选项卡，用于标识所选谓词的类型。

1. 在[!UICONTROL 属性名称]字段中，为要与谓词关联的元数据属性指定有效名称。该名称是执行搜索时所依据的名称。例如，输入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。

   您还可以从选择对话框中选择现有节点。

   ![将元数据属性与属性名称字段中的谓词关联](assets/property_settings.png)

   将元数据属性与属性名称字段中的谓词关联

1. 单击 **[!UICONTROL 预览]** ![预览](assets/do-not-localize/preview_icon.png) 以生成在添加谓词后显示的“过滤器”面板的预览。
1. 在预览模式下查看谓词的布局。

   ![在提交更改之前预览搜索表单](assets/preview-1.png)

   在提交更改之前预览搜索表单

1. 要关闭预览，请单击 **[!UICONTROL 关闭]** ![close](assets/do-not-localize/close.png) 的双曲余切值。
1. 单击 **[!UICONTROL 完成]** 来保存设置。
1. 导航到 [!DNL Assets] 用户界面。 属性谓词已添加到面板。
1. 在文本框中输入要搜索的资产的描述。 例如，输入 `Adobe`. 执行搜索时，描述与 `Adobe` 在搜索结果中列出。

## 添加“选项”谓词 {#adding-an-options-predicate}

“选项”谓词允许您在“过滤器”面板中添加多个搜索选项。 您可以在过滤器面板中选择一个或多个选项来搜索资产。 例如，要根据文件类型搜索资产，请配置搜索表单中的“图像”、“多媒体”、“文档”和“存档”等选项。 配置这些选项后，当您在“过滤器”面板中选择“图像”选项时，会对GIF、JPEG、PNG等类型的资产执行搜索。

要将选项映射到相应的属性，请为选项创建节点结构，并在“选项”谓词的“属性名称”属性中提供父节点的路径。 父节点的类型应为 `sling`: `OrderedFolder`. 选项的类型应为 `nt:unstructured`. 选项节点应具有属性 `jcr:title` 和 `value` 已配置。

的 `jcr:title` 属性是“过滤器”面板中显示的选项的用户友好名称。 的 `value` 字段来匹配指定的属性。

当您选择一个选项时，将根据 `value` 选项节点及其子节点的属性（如果有）。 系统会遍历选项节点下的整个树，并且 `value` 使用OR操作组合每个子节点的属性以构成搜索查询。

例如，如果您为文件类型选择“图像”，则资产的搜索查询将通过使用 OR 操作组合 `value` 属性来构建。**********`jcr:content/metadata/dc:format`

![文件类型的值属性（如CRXDE中所示）用于搜索查询正常工作](assets/filetype-value-property.png)

文件类型的值属性（如CRXDE中所示）用于搜索查询正常工作

您可以通过指定相应的键值对在JSON文件中定义选项，而不是为CRXDE存储库中的选项手动创建节点结构。 在&#x200B;**[!UICONTROL 属性名称]**&#x200B;字段中指定 JSON 文件的路径。例如，您可以定义键值对、`image/bmp`、`image/gif`、`image/jpeg` 和 `image/png`，并指定它们的值，如以下示例 JSON 文件中所示。在 **[!UICONTROL 属性名称]** 字段中，您可以指定此文件的CRXDE路径。

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

如果要使用现有节点，请使用选择对话框指定它。

>[!NOTE]
>
>“选项”谓词是一个自定义包装器，其中包含用于演示所述行为的属性谓词。 目前，没有REST端点可在本地支持该功能。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索Forms]**.
1. 从 **[!UICONTROL 搜索Forms]** 页面，选择 **[!UICONTROL 资产管理搜索边栏]**，然后单击 **[!UICONTROL 编辑]**.
1. 在“编 **[!UICONTROL 辑搜索表单]** ”页中，将“选 **[!UICONTROL 项谓词]** ”从“选 **** 择谓词”选项卡拖至主窗格。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，输入属性的标签和名称。例如，要根据资产的格式搜索资产，请为标签指定用户友好名称，例如&#x200B;**[!UICONTROL 文件类型]**。在属性字段中指定执行搜索时所依据的属性，例如 `jcr:content/metadata/dc:format.`
1. 执行下列操作之一：

   * 在 **[!UICONTROL 属性名称]** 字段中，提及JSON文件的路径，在该路径中为选项定义节点并指定相应的键值对。
   * 单击 `+` “选项”(Options)字段旁的符号，用于指定要在“过滤器”(Filters)面板中提供的选项的显示文本和值。 要添加其他选项，请单击 `+` 符号，然后重复该步骤。

1. 确保取消选中&#x200B;**[!UICONTROL 单选]**，以允许用户一次为文件类型选择多个选项（例如，“图像”、“文档”、“多媒体”和“存档”）。如果选中&#x200B;**[!UICONTROL 单选]**，则用户一次只能为文件类型选择一个选项。

   ![“选项”谓词中的可用字段](assets/options_predicate.png)

   “选项”谓词中的可用字段

1. 在 **[!UICONTROL 描述]** 字段，输入可选描述，然后单击 **[!UICONTROL 完成]**.
1. 导航到“搜索”面板。 “选项”谓词已添加到 **搜索** 的上界。 选项 **[!UICONTROL 文件类型]** 显示为复选框。

## 添加多值属性谓词 {#adding-a-multi-value-property-predicate}

使用多值属性谓词，您可以搜索资产以查找多个值。 假设您在 [!DNL Assets] 并且每个图像的元数据都包含与产品关联的SKU号。 您可以使用此谓词根据多个SKU编号搜索产品图像。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索Forms]**.
1. 在搜索Forms页面上，选择 **[!UICONTROL 资产管理搜索边栏]**，单击 **[!UICONTROL 编辑]** ![编辑图标](assets/do-not-localize/aemassets_edit.png).
1. 在“编辑搜索表单”页中，将&#x200B;**[!UICONTROL 多值属性谓词]**&#x200B;从&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡拖到主窗格。
1. 在 **[!UICONTROL 设置]** 选项卡，输入谓词的标签和占位符文本。 在属性字段中指定执行搜索时所依据的属性名称，例如 `jcr:content/metadata/dc:value`. 您还可以使用选择对话框来选择节点。
1. 确保选中&#x200B;**[!UICONTROL 分隔符支持]**。在&#x200B;**[!UICONTROL 输入分隔符]**&#x200B;字段中，指定要用于分隔各个值的分隔符。默认情况下，指定逗号为分隔符。您可以指定其他分隔符。
1. 在 **描述** 字段，输入可选描述，然后单击 **[!UICONTROL 完成]**.
1. 导航到 [!DNL Assets] 用户界面。 **[!UICONTROL 多值属性]**&#x200B;谓词已添加到面板。
1. 在由分隔符分隔的多值字段中指定多个值并执行搜索。 此谓词会获取与您指定的值精确匹配的文本。

## 添加“标记”谓词 {#adding-a-tags-predicate}

利用标记谓词，可对资产执行基于标记的搜索。 默认情况下， [!DNL Assets] 根据您指定的标记，搜索资产中一个或多个标记匹配项。 换句话说，搜索查询使用指定的标记执行OR操作。 但是，您可以使用“匹配所有标记”选项来搜索包含您指定的所有标记的资产。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索Forms]**.
1. 从搜索Forms页面中，选择 **[!UICONTROL 资产管理搜索边栏]** 然后单击 **[!UICONTROL 编辑]** ![编辑图标](assets/do-not-localize/aemassets_edit.png).
1. 在“编辑搜索表单”页面中，将 **[!UICONTROL 标记谓词]** 从“选择谓词”选项卡转到主窗格。
1. 在设置选项卡中，输入谓词的占位符文本。 在属性字段中指定执行搜索时所依据的属性名称，例如 *jcr:content/metadata/cq:tags*. 或者，您也可以从选择对话框中选择CRXDE中的节点。
1. 配置此谓词的根标记路径属性，以填充“标记”列表中的各种标记。
1. 选择&#x200B;**[!UICONTROL 显示“匹配所有标记”选项]**，以搜索包含您指定的所有标记的资产。

1. 在 **[!UICONTROL 描述]** 字段，输入可选描述，然后单击 **[!UICONTROL 完成]**.
1. 导航到“搜索”面板。 的 **[!UICONTROL 标记]** 谓词已添加到“搜索”面板。
1. 指定要根据哪些标记来搜索资产，或从建议列表中进行选择。

1. 选择 **[!UICONTROL 全部匹配]** 搜索包含您指定的所有标记的匹配项。

## 添加其他谓词 {#adding-other-predicates}

与添加“属性”谓词或“选项”谓词的方式类似，您可以向“搜索”面板添加以下其他谓词：

| 谓词名称 | 描述 | 属性 |
|---|---|---|
| [!UICONTROL 全文] | 此搜索谓词用于在整个资产节点上执行全文搜索。 它已映射为jcr:contains运算符。 如果要对资产节点的特定部分执行全文搜索，可以指定相对路径。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 路径浏览器] | 此搜索谓词用于在预配置的根路径的文件夹和子文件夹中搜索资产 | <ul><li>占位符</li><li>根路径</li><li>描述</li></ul> |
| [!UICONTROL 路径] | 使用它按位置筛选结果。 您可以指定不同的路径作为选项。 | <ul><li>标签</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 发布状态] | 此搜索谓词用于根据资产的发布状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 相对日期] | 此搜索谓词用于根据资产创建的相对日期搜索资产。 例如，您可以配置选项，如2个月前、3周前等。 | <ul><li>标签</li><li>属性名称</li><li>相对日期</li></ul> |
| [!UICONTROL 范围] | 此搜索谓词用于搜索位于指定范围内的资产。 在“搜索”面板中，您可以指定范围的最小值和最大值。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 日期范围] | 此搜索谓词用于搜索在日期属性的指定范围内创建的资产。 在“搜索”面板中，您可以使用日期选取器指定开始和结束日期。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>范围文本（从）</li><li>范围文本（至）</li><li>描述</li></ul> |
| [!UICONTROL 日期] | 此搜索谓词用于根据日期属性对资产进行基于滑块的搜索。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 文件大小] | 此搜索谓词用于根据资产的大小搜索资产。 它是一个基于滑块的谓词，您可以从可配置节点中选择滑块选项。 默认选项在CRXDE存储库的/libs/dam/options/predicates/filesize中定义。 文件大小以字节为单位提供。 | <ul><li>标签</li><li>属性名称</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 上次修改的资源] | 此搜索谓词用于搜索最近修改的资产 | <ul><li>属性名称</li><li>属性值</li><li>描述</li></ul> |
| [!UICONTROL 发布状态] | 此搜索谓词用于根据资产的发布状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 评分] | 此搜索谓词用于根据资产的平均评级搜索资产 | <ul><li>标签</li><li>属性名称</li><li>选项路径</li><li>描述</li></ul> |
| [!UICONTROL 到期状态] | 此搜索谓词用于根据资产的到期状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 隐藏] | 此搜索谓词用于定义用于搜索资产的隐藏字段属性 | <ul><li>属性名称</li><li>属性值</li><li>描述</li></ul> |

## 恢复默认搜索彩块化 {#restoring-default-search-facets}

默认情况下，会显示锁图标 ![锁闭图标](assets/do-not-localize/lock_closed_icon.svg) 出现在之前 **[!UICONTROL 资产管理搜索边栏]** 在 **[!UICONTROL 搜索Forms]** 页面。 针对“搜索Forms”页面上的选项的锁定图标表示默认设置保持不变且未进行自定义。 图标 ![锁闭图标](assets/do-not-localize/lock_closed_icon.svg) 如果您向表单中添加搜索彩块化，则表示默认表单已被修改，则会消失。

![“锁定”图标](assets/locked_admin_rail.png)

要恢复默认搜索彩块化，请执行以下步骤：

1. 选择 **[!UICONTROL 资产管理搜索边栏]** 在 **[!UICONTROL 搜索Forms]** 页面。
1. 单击 **[!UICONTROL 删除]** ![删除大纲](assets/do-not-localize/deleteoutline.png) 中。
1. 在确认对话框中，单击 **[!UICONTROL 删除]** 删除自定义更改。

   在删除对搜索彩块化的自定义更改后， ![锁闭图标](assets/do-not-localize/lock_closed_icon.svg) 重新显示之前 **[!UICONTROL 资产管理搜索边栏]** 在 **[!UICONTROL 搜索Forms]** 页面。

## 用户权限 {#user-permissions}

如果您未分配管理员角色，下面是您执行涉及搜索彩块化的编辑、删除和预览操作所需的权限列表。

| 操作 | 权限 |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL 编辑] | 对 `/apps` CRXDE中的节点 |
| [!UICONTROL 删除] | 对 `/apps` CRXDE中的节点 |
| [!UICONTROL 预览] | 对 `/var/dam/content` 节点。 此外，还具有 `/apps` 节点。 |

>[!MORELIKETHIS]
>
>* [扩展资产搜索功能](searchx.md)
>* [搜索资产](search-assets.md)

