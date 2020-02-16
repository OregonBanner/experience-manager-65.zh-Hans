---
title: 搜索彩块化
description: 本文介绍如何在AEM中创建、修改和使用搜索彩块化。
uuid: 213bec95-2f9a-49d2-a45b-0c7d1bb4fbf8
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 4c03f218-6c0c-4482-b10e-a6ccddb30d57
translation-type: tm+mt
source-git-commit: 62cc3282f8d8bc77f072de1d027484bd93efa38a

---


# 搜索彩块化 {#search-facets}

了解如何在AEM中创建、修改和使用搜索彩块化。

Adobe Experience Manager(AEM)资产的企业级部署能够存储许多资产。 有时，如果您仅使用AEM的通用搜索功能，则查找正确的资产可能既费时又费力。

使用“筛选器”面板中的搜索彩块化为搜索体验添加更多粒度，使搜索功能更高效、用途更广。 搜索彩块化可添加多个维度（谓词），使您能够执行更复杂的搜索。 “滤镜”面板包括一些标准彩块化。 您还可以添加自定义搜索彩块化。

总而言之，搜索彩块化允许您以多种方式而不是按单一、预先确定的分类顺序搜索资产。 您可以轻松向下展开到所需的详细信息级别，以便进行更具针对性的搜索。

例如，如果要查找图像，则可以选择是要位图还是要矢量图像。 您可以通过为图像指定MIME类型进一步缩小搜索范围。 同样，在搜索文档时，可以指定格式，例如PDF或MS Word。

## 添加谓词 {#adding-a-predicate}

在“筛选器”面板中显示的搜索彩块化是使用谓词在基础搜索表单中定义的。 要显示更多或不同的彩块化，您可向默认表单添加谓词，或使用包含您选择的彩块化的自定义表单。

对于全文搜索，请向表单中添加“全文”谓词。 使用“属性”谓词可搜索与您指定的单个属性匹配的资产。 使用“选项”谓词可搜索与特定属性的一个或多个值匹配的资产。 添加“日期范围”谓词以搜索在指定日期范围内创建的资产。

1. 点按／单击AEM徽标，然后转到工具 **** >常规 **[!UICONTROL >搜]** 索表单 ****。
1. 在“搜索表单”页面中，选择“资 **[!UICONTROL 产管理员搜索边栏]**”，然后点 **按** Edit ![](assets/aemassets_edit.png)aemassets_edit。

   ![找到并选择资产管理搜索边栏](assets/assets_admin_searchrail.png)

   找到并选择资产管理搜索边栏

   >[!NOTE]
   >
   >要使用先前AEM版本中预配置的资产管理搜索边栏中的 **文件夹搜索功能** ，请执行以下步骤：
   >
   >1. 在CRXDE *中导航到/conf/global/settings/dam/search/facets/assets/jcr:content/items* 。
   >1. 删除 **类型节** 点。
   >1. 从路径 */libs/settings/dam/search/facets/assets/jcr:content/items*，将节点资产、目录、类型、排除路径和 **searchtype****** ，复制到步骤1中提到的路径。
   >1. 保存更改。


1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. For example, drag **[!UICONTROL Property Predicate]**.

   ![拖放谓词以自定义搜索筛选器](assets/drag_predicate.png)

   拖放谓词以自定义搜索筛选器

1. 在设置选项卡中，输入谓词的字段标签、占位符文本和说明。 为要与谓词关联的元数据属性指定有效名称。

   设置选项卡中的标题标签标识所选谓词的类型。

   ![使用“设置”选项卡提供谓词的所需选项](assets/settings.png)

   使用“设置”选项卡提供谓词的所需选项

1. 在“属 **[!UICONTROL 性名称]** ”字段中，为要与谓词关联的元数据属性指定有效名称。 它是执行搜索时所依据的名称。 例如，输入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。

   您还可以从选择对话框中选择现有节点。

   ![将元数据属性与属性名称字段中的谓词关联](assets/property_settings.png)

   将元数据属性与属性名称字段中的谓词关联

1. Tap/click the **[!UICONTROL Preview]** ![preview](assets/preview.png) to generate a preview of the Filters panel as it appears after you add the predicate.
1. 在“预览”模式下查看谓词的布局。

   ![在提交更改之前预览搜索表单](assets/preview-1.png)

   在提交更改之前预览搜索表单

1. To close the preview, tap/click the **[!UICONTROL Close]** ![close](assets/close.png) on the upper-right corner of the preview.
1. Tap **[!UICONTROL Done]** to save the settings.
1. 导航到资产用户界面中的“搜索”面板。属性谓词已添加到面板。
1. 在文本框中输入对要搜索的资产的描述。例如，输入“Adobe”。执行搜索时，其描述与“Adobe”匹配的资产便会列在搜索结果中。

## 添加“选项”谓词 {#adding-an-options-predicate}

“选项”谓词允许您在“筛选器”面板中添加多个搜索选项。 您可以在“筛选器”面板中选择一个或多个选项以搜索资产。 例如，要根据文件类型搜索资产，请在搜索表单中配置“图像”、“多媒体”、“文档”和“存档”等选项。 配置这些选项后，当您在“滤镜”面板中选择“图像”选项时，将对GIF、JPEG、PNG等类型的资产执行搜索。

要将选项映射到相应的属性，请为选项创建一个节点结构，并在“选项”谓词的“属性名称”属性中提供父节点的路径。 The parent node should be of type `sling`: `OrderedFolder`. The options should be of type `nt:unstructured`. The option nodes should have the properties `jcr:title` and `value` configured.

The `jcr:title` property is a user-friendly name for the option that is displayed on the Filters panel. `value` 字段会用在查询中以匹配指定的属性。

当您选择一个选项时，会根据该选项节点及其子节点（如果有）的 `value` 属性来执行搜索。系统会遍历该选项节点下的整个树，并通过使用 OR 运算将每个子节点的 `value` 属性组合到一起，以构成搜索查询。

For example, if you select &quot;Images&quot; for file types, the search query for the assets is built by combining the `value` property using an OR operation. For example, the search query for images is built by combining the results matched for *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, and *image/tiff* for the property `jcr:content/metadata/dc:format` using an OR operation.

![CRXDE中所示的文件类型的值属性用于搜索查询](assets/chlimage_1-418.png)

CRXDE中所示的文件类型的值属性用于搜索查询

您可以通过指定相应的键值对，在JSON文件中定义选项，而不是手动为CRXDE存储库中的选项创建节点结构。 在“属性名称”字段中指定JSON文 **[!UICONTROL 件的路径]** 。 例如，您可以定义键值对、 `image/bmp`、 `image/gif`、 `image/jpeg`和 `image/png` ，并指定它们的值，如以下示例JSON文件中所示。 在“属 **[!UICONTROL 性名称]** ”字段中，可以指定此文件的CRXDE路径。

```JSON
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
>“选项”谓词是一个自定义包装器，其中包含用于演示所描述行为的属性谓词。 目前，没有 REST 端点可在本机支持该功能。

1. 点按AEM徽标，然后转到工具> **[!UICONTROL 常规>搜索表单]**。
1. 在“搜索 **[!UICONTROL 表单]** ”页面中，选择 **[!UICONTROL 资产管理员搜索边栏]**，然后点按编辑图标。
1. In the **[!UICONTROL Edit Search Form]** page, drag **[!UICONTROL Options Predicate]** from the **[!UICONTROL Select Predicate]** tab to the main pane.
1. In the **[!UICONTROL Settings]** tab, enter a label and a name for the property. For example, to search assets based on their format, specify a user-friendly name for the label, for example **[!UICONTROL File Type]**. Specify the property based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:format.`
1. 执行下列操作之一：

   * 在“属 **[!UICONTROL 性名称]** ”字段中，提及JSON文件的路径，在该路径中您为选项定义节点并指定相应的键值对。
   * 点按或单击“ `+` 选项”字段旁边的符号，以指定要在“滤镜”面板中提供的选项的显示文本和值。 要添加其他选项，请点按／单击 `+` 符号，然后重复该步骤。

1. Ensure that **[!UICONTROL Single Select]** is cleared to let the user select multiple options for file types at a time (for example, Images, Documents, Multimedia, and Archives). If you select **[!UICONTROL Single Select]**, the user can select only one option for file types at a time.

   ![“选项”谓词中的可用字段](assets/options_predicate.png)

   “选项”谓词中的可用字段

1. 在&#x200B;**[!UICONTROL 描述]**&#x200B;字段中，输入可选描述，然后单击&#x200B;**[!UICONTROL 完成]**。
1. 导航到“搜索”面板。“选项”谓词已添加到“搜 **索** ”面板。 “文件类型” **[!UICONTROL 的选项将显示]** 为复选框。

## 添加多值属性谓词 {#adding-a-multi-value-property-predicate}

通过“多值属性”谓词，您可以搜索多个值的资产。 请考虑在AEM资产中有多个产品的图像，并且每个图像的元数据包括与产品关联的SKU编号的情况。 您可以使用此谓词根据多个SKU编号搜索产品图像。

1. 单击AEM徽标，然后转到工具 **** >常 **[!UICONTROL 规]** >搜 **[!UICONTROL 索表单]**。
1. 在“搜索表单”页面上，选择“ **[!UICONTROL 资产管理员搜索边栏]**”，然后点 **[!UICONTROL 按]** Edit ![](assets/aemassets_edit.png)aemassets_edit。
1. 在“编辑搜索表单”页中，将多值属 **[!UICONTROL 性谓词从“选择谓]****** 词”选项卡拖到主窗格。
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. 您还可以使用选择对话框选择节点。
1. 确保选 **[!UICONTROL 择“Delimiter Support]** （分隔符支持）”。 在“输入 **[!UICONTROL 分隔符]** ”字段中，指定分隔符以分隔各个值。 默认情况下，逗号指定为分隔符。 您可以指定其他分隔符。
1. In the **Description** field, enter an optional description and then tap **[!UICONTROL Done]**.
1. 导航到“资产”用户界面中的“过滤器”面板。 The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 在由分隔符分隔的“多值”字段中指定多个值并执行搜索。 此谓词将获取与您指定的值精确匹配的文本。

## 添加标记谓词 {#adding-a-tags-predicate}

标记谓词允许您对资产执行基于标记的搜索。 默认情况下，AEM资产会根据您指定的标记搜索资产中一个或多个标记匹配项。 换句话说，搜索查询使用指定的标记执行OR操作。 但是，您可以使用“匹配所有标记”选项来搜索包含您指定的所有标记的资产。

1. 单击AEM徽标，然后转到工具 **** >常 **[!UICONTROL 规]** >搜 **[!UICONTROL 索表单]**。
1. 在“搜索表单”页面中，选择“资 **[!UICONTROL 产管理员搜索边栏]** ”，然后点 **[!UICONTROL 按]** Edit ![](assets/aemassets_edit.png)aemassets_edit。
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. 在设置选项卡中，输入谓词的占位符文本。 Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. 或者，也可以从选择对话框中在CRXDE中选择节点。
1. 配置此谓词的根标记路径属性，以在标记列表中填充各种标记。
1. 选择 **[!UICONTROL 显示匹配所有标记选项]** ，以搜索包含您指定的所有标记的资产。

   ![“标记”谓词的典型设置](assets/tags_predicate.png)

   “标记”谓词的典型设置

1. In the **[!UICONTROL Description]** field, enter an optional description and then click/tap **[!UICONTROL Done]**.
1. 导航到“搜索”面板。 The **[!UICONTROL Tags]** predicate is added to the Search panel.
1. 指定要根据其搜索资产或从建议列表中进行选择的标记。

   ![键入标记名称时AEM提供的建议](assets/chlimage_1-419.png)

   键入标记名称时AEM提供的建议

1. 选择 **[!UICONTROL “全部匹配]** ”以搜索包含您指定的所有标记的匹配项。

## 添加其他谓词 {#adding-other-predicates}

按照与添加“属性”谓词或“选项”谓词相似的方法，您还可以将以下谓词添加到“搜索”面板：

| 谓词名称 | 描述 | 属性 |
|---|---|---|
| [!UICONTROL 全文] | 此搜索谓词用于对整个资产节点执行全文搜索。 它映射为jcr:contains运算符。 如果要对资产节点的特定部分执行全文搜索，则可以指定相对路径。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 路径浏览器] | 此搜索谓词用于在预配置的根路径中搜索文件夹和子文件夹中的资产 | <ul><li>占位符</li><li>根路径</li><li>描述</li></ul> |
| [!UICONTROL 路径] | 使用它可以按位置筛选结果。 可以指定不同的路径作为选项。 | <ul><li>标签</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 发布状态] | 此搜索谓词用于根据资产的发布状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 相对日期] | 此搜索谓词用于根据创建资产的相对日期搜索资产. 例如，您可以配置选项，如2个月前、3周前等。 | <ul><li>标签</li><li>属性名称</li><li>相对日期</li></ul> |
| [!UICONTROL 范围] | 此搜索谓词用于搜索特定范围内的资产。在“搜索”面板中，可以指定范围的最小值和最大值。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 日期范围] | 此搜索谓词用于搜索在日期属性的指定范围内创建的资产。在“搜索”面板中，您可以使用日期选择器指定开始和结束日期。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>范围文本（始于）</li><li>范围文本（止于）</li><li>描述</li></ul> |
| [!UICONTROL 日期] | 此搜索谓词用于根据日期属性进行基于滑块的资产搜索。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 文件大小] | 此搜索谓词用于根据资产的大小搜索资产. 它是一个基于滑块的谓词，您可以从可配置节点中选择滑块选项。 默认选项在CRXDE存储库中的/libs/dam/options/predicates/filesize中定义。 文件大小以字节为单位提供。 | <ul><li>标签</li><li>属性名称</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 上次修改的资源] | 此搜索谓词用于搜索最近修改的资产 | <ul><li>属性名称</li><li>属性值</li><li>描述</li></ul> |
| [!UICONTROL 发布状态] | 此搜索谓词用于根据资产的发布状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 评级] | 此搜索谓词用于根据资产的平均评级搜索资产 | <ul><li>标签</li><li>属性名称</li><li>选项路径</li><li>描述</li></ul> |
| [!UICONTROL 到期状态] | 此搜索谓词用于根据资产的到期状态搜索资产 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 隐藏] | 此搜索谓词用于定义用于搜索资产的隐藏字段属性 | <ul><li>属性名称</li><li>属性值</li><li>描述</li></ul> |

## 恢复默认搜索彩块化 {#restoring-default-search-facets}

默认情况下，“搜索表单”页面中的“资 **[!UICONTROL 产管理员搜索边栏]** ”前会 **[!UICONTROL 显示“锁定”图标]** 。 如果您向该表单中添加搜索彩块化，该锁图标便会消失，以指示默认表单已被修改。

![“搜索表单”页面上某个选项的锁图标表示默认设置保持不变且未自定义。](assets/locked_admin_rail.png)

“搜索表单”页面上某个选项的锁图标表示默认设置保持不变且未自定义。

要恢复默认搜索facet，请执行以下步骤：

1. 在“搜 **[!UICONTROL 索表单”页面中]** ，选择“资 **[!UICONTROL 产管理员]** ”“搜索边栏”。
1. 点按 **[!UICONTROL 工具栏]** 中的删除。
   ![deleteoutline](assets/deleteoutline.png)
1. 在确认对话框中，点按 **[!UICONTROL 删除]** ，以删除自定义更改。

   After you delete the custom changes to search facets, the Lock icon reappears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.

## 用户权限 {#user-permissions}

如果未为您分配管理员角色，则以下是您需要执行与搜索彩块化相关的编辑、删除和预览操作的权限列表。

| 操作 | 权限 |
|---|---|
| [!UICONTROL 编辑] | Read and Write permissions on the `/apps` node in CRXDE |
| [!UICONTROL 删除] | 在CRXDE中对节点具有读取、写入和 `/apps` 删除权限 |
| [!UICONTROL 预览] | 在CRXDE中对节点具有读取、写入和 `/var/dam/content` 删除权限。 Also, Read and Write permissions on `/apps` node. |

>[!MORELIKETHIS]
>
>* [扩展资产搜索功能](searchx.md)
>* [搜索资产](search-assets.md)

