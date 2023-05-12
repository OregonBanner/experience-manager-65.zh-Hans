---
title: 管理数字资产的元数据
description: 了解元数据类型以及如何管理资产的元数据，以便轻松组织和处理资产。
contentOwner: AG
mini-toc-levels: 1
feature: Tagging, Metadata
role: Architect, Leader
exl-id: c630709a-7e8b-417c-83a4-35ca9be832a0
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2359'
ht-degree: 11%

---

# 管理数字资产的元数据 {#managing-metadata-for-digital-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-metadata.html?lang=en) |
| AEM 6.5 | 本文 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每个资产的元数据。 它允许更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。 能够从上传到的文件中提取元数据 [!DNL Experience Manager Assets]，元数据管理与创意工作流集成。 通过使用资产保留和管理元数据的功能，您可以根据资产的元数据自动组织和处理资产。

## 元数据及其源 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 它会添加到资产和 [!DNL Experience Manager] 在您上传资产时，会处理该资产。 您可以编辑现有元数据，向现有字段添加新的元数据属性。 组织需要可控且可靠的元数据词汇。 因此 [!DNL Experience Manager Assets] 不允许按需添加新元数据属性。 只有管理员和开发人员才能添加包含元数据的新属性或字段。 用户可以使用元数据填充现有字段。

可以使用以下方法将元数据添加到数字资产：

* 首先，创建资产的本机应用程序会向其中添加一些元数据。 例如， [Acrobat添加了一些元数据](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) 要PDF文件或相机，会向照片中添加一些基本元数据。 在生成资产时，您可以在本机应用程序本身中添加元数据。 例如，您可以 [在Adobe Lightroom中添加IPTC元数据](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* 在将资产上传到 [!DNL Experience Manager]，您可以使用用于创建资产的本机应用程序或使用其他一些元数据编辑应用程序来编辑和修改元数据。 将资产上传到Experience Manager时，会处理元数据。 例如，请参阅如何 [在中使用元数据 [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) 并查看 [标记面板 [!DNL Adobe Bridge]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) in [!DNL Adobe Exchange].

* 在 [!DNL Experience Manager Assets]，您可以在 [!UICONTROL 属性] 页面。

* 您可以利用 [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles) 功能 [!DNL Experience Manager Assets] 以在资产上传到DAM后自动添加元数据。

## 在中添加或编辑元数据 [!DNL Experience Manager Assets] {#add-edit-metadata}

要在 [!DNL Assets] 用户界面中，请执行以下步骤：

1. 执行下列操作之一：

   * 从 [!DNL Assets] 界面，选择资产并单击 **[!UICONTROL 查看属性]** 中。
   * 从资产缩略图中，选择 **[!UICONTROL 查看属性]** 快速操作。
   * 在资产页面中，单击 **[!UICONTROL 查看属性]** ![资产信息图标](assets/do-not-localize/info-circle-icon.png) 中。

   资产页面会显示资产的所有元数据。 将资产上传（摄取）到 [!DNL Experience Manager].

   ![选择资产的属性以查看其元数据](assets/asset-metadata.png)

   *图：在资产中编辑或添加元数据 [!UICONTROL 属性] 页面。*

1. 根据需要，在各种选项卡下对元数据进行编辑，完成后，单击 **[!UICONTROL 保存]** 来保存更改。 单击 **[!UICONTROL 关闭]** 返回 [!DNL Assets] web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则不存在现有的元数据集。 您可以在字段中输入一个值，然后进行保存以添加该元数据属性。

对资产元数据所做的任何更改都会作为资产数据的一部分写回原始二进制文件。 元数据回写工作流会将元数据添加到原始二进制文件。 对现有属性所做的更改(例如 `dc:title`)和新属性(包括 `cq:tags`)。

支持并启用XMP的回写功能，这些功能包括 [技术要求。](/help/sites-deploying/technical-requirements.md)

## 编辑多个资产的元数据属性 {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] 允许您同时编辑多个资产的元数据，以便能够快速批量将常见元数据更改传播到资产。 您还可以批量编辑多个收藏集的元数据。 使用属性页面对多个资产或收藏集执行元数据更改：

* 将元数据属性更改为通用值
* 添加或修改标记

要自定义元数据属性页面（包括添加、修改、删除元数据属性），请使用 [架构编辑器](metadata-config.md#folder-metadata-schema).

>[!NOTE]
>
>批量编辑方法适用于文件夹或收藏集中的可用资产。 对于跨文件夹提供的资产或符合常用条件的资产，可以 [搜索后批量更新元数据](search-assets.md#metadataupdates).

1. 在 [!DNL Assets] 用户界面中，导航到要编辑的资产所在的位置。
1. 选择要编辑其常用属性的资产。
1. 在工具栏中，单击 **[!UICONTROL 属性]** 打开选定资产的属性页面。
1. 在各种选项卡下修改选定资产的元数据属性。
1. 要查看特定资产的元数据，请取消在列表中选择的其余资产。 如果您在 [!UICONTROL 属性] 页面，则不会更新此类资产的元数据。
1. 要为资产选择其他元数据架构，请单击 **[!UICONTROL 设置]** 从工具栏中，选择一个架构。 单击“**[!UICONTROL 保存并关闭]**”。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。单击 **[!UICONTROL 提交]**.

![元数据架构批量应用于多个资产](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 导入元数据 {#import-metadata}

[!DNL Assets] 允许您使用CSV文件批量导入资产元数据。 您可以通过导入CSV文件，对最近上传的资产或现有资产进行批量更新。 您还可以以CSV格式从第三方系统批量摄取资产元数据。

元数据导入是异步的，不会影响系统性能。 如果选中了工作流标记，则由于XMP写回活动，因此同时更新多个资产的元数据可能会占用大量资源。 在精益服务器使用期间规划此类导入，以便不影响其他用户的性能。

>[!NOTE]
>
>要导入自定义命名空间的元数据，请首先注册命名空间。

1. 导航到 [!DNL Assets] 用户界面，然后单击 **[!UICONTROL 创建]** 中。
1. 从菜单中，选择 **[!UICONTROL 元数据]**.
1. 在 **[!UICONTROL 元数据导入]** 页面，单击 **[!UICONTROL 选择文件]**. 选择包含元数据的 CSV 文件。
1. 指定以下参数。 请参阅 [metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv).

   | 元数据导入参数 | 描述 |
   |:---|:---|
   | [!UICONTROL 批量大小] | 要为其导入元数据的批次中的资产数量。 默认值为 50。最大值为100。 |
   | [!UICONTROL 字段分隔符] | 默认值为 `,` （逗号）。 您可以指定任何其他字符。 |
   | [!UICONTROL 多值分隔符] | 元数据值的分隔符。 默认值为 `|`. |
   | [!UICONTROL 启动工作流] | 默认为False。 当设置为 `true` 和默认设置对 [!UICONTROL DAM元数据回写] 工作流(将元数据写入二进制XMP数据)。 启用工作流会减慢系统速度。 |
   | [!UICONTROL 资产路径列名称] | 为包含资产的CSV文件定义列名称。 |

1. 单击 **[!UICONTROL 导入]** 中。 导入元数据后，将在 [!UICONTROL 通知] 收件箱。

1. 要验证导入是否正确，请导航到资产的 [!UICONTROL 属性] ，并验证字段中的值。

要在导入元数据时添加日期和时间戳，请使用 `YYYY-MM-DDThh:mm:ss.fff-00:00` 日期和时间的格式。 日期和时间以 `T`, `hh` 是24小时格式， `fff` 为纳秒，并且 `-00:00` 是时区偏移。 例如， `2020-03-26T11:26:00.000-07:00` 于2020年3月26日11时:26:太平洋标准时间上午00点。

>[!CAUTION]
>
>如果日期格式不匹配 `YYYY-MM-DDThh:mm:ss.fff-00:00`，则不会设置日期值。 导出的元数据CSV文件的日期格式为 `YYYY-MM-DDThh:mm:ss-00:00`. 如果要导入该值，请通过添加表示为的纳秒值，将其转换为可接受的格式 `fff`.

## 导出元数据 {#export-metadata}

您可以以CSV格式导出多个资产的元数据。 元数据是异步导出的，不会影响系统性能。 要导出元数据， [!DNL Experience Manager] 遍历资产节点的属性 `jcr:content/metadata` 及其子节点，并将元数据属性导出为CSV文件。

批量导出元数据的一些用例包括：

* 迁移资产时，在第三方系统中导入元数据。
* 与更广的项目团队共享资产元数据。
* 测试或审核元数据以确保合规性。
* 将元数据外部化，以将其单独本地化。

1. 选择包含要导出元数据的资产的资产文件夹。 在工具栏中，选择 **[!UICONTROL 导出元数据]**.

1. 在 [!UICONTROL 元数据导出] 对话框，请指定CSV文件的名称。 要导出子文件夹中资产的元数据，请选择 **[!UICONTROL 在子文件夹中包含资产]**.

   ![用于导出文件夹中所有资产的元数据的界面和选项](assets/export_metadata_page.png "用于导出文件夹中所有资产的元数据的界面和选项")

1. 选择所需的选项。 提供文件名，并在必要时提供日期。

1. 在 **[!UICONTROL 要导出的属性]** 字段中，指定要导出全部属性还是特定属性。 如果选择要导出的选择性属性，请添加所需的属性。

1. 在工具栏中，单击 **[!UICONTROL 导出]**. 系统会显示一条消息，确认已导出元数据。 关闭消息。

1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。要下载包含元数据的CSV文件，请单击 **[!UICONTROL CSV下载]** 中。 单击&#x200B;**[!UICONTROL 关闭]**。

   ![用于下载包含批量导出元数据的CSV文件的对话框](assets/csv_download.png)

   *图：用于下载包含批量导出元数据的CSV文件的对话框。*

## 编辑收藏集的元数据 {#collections-metadata}

有关详细信息，请参阅 [查看和编辑收藏集元数据](/help/assets/manage-collections.md#view-edit-collection-metadata) 和 [批量编辑多个收藏集的元数据](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk).

## 将元数据配置文件应用到文件夹 {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

当您将元数据配置文件分配给文件夹后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。 这意味着您只能向文件夹分配一个元数据配置文件。 因此，请仔细考虑上传、存储、使用和存档资产所在的文件夹结构。

如果您为文件夹分配了不同的元数据配置文件，则新配置文件会覆盖之前的配置文件。 以前存在的文件夹资产将保持不变。 新配置文件会应用于稍后添加到文件夹的资产。

在用户界面中，如果文件夹分配了配置文件，则卡片名称中会显示配置文件的名称。

![卡片视图显示应用于文件夹的元数据配置文件](assets/metadata-profile-card-view-display.png)

您可以将元数据配置文件应用到特定文件夹或全局应用到所有资产。

您可以重新处理文件夹中已有元数据配置文件（您稍后更改了该配置文件）的资产。 请参阅 [编辑文件夹中的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅 [编辑文件夹中的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

### 将元数据配置文件从 [!UICONTROL 用户档案] 用户界面 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

请按照以下步骤应用元数据配置文件：

1. 单击 [!DNL Experience Manager] 徽标和导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.
1. 选择要应用于一个或多个文件夹的元数据配置文件。
1. 单击 **[!UICONTROL 将元数据配置文件应用到文件夹]** ，然后选择一个或多个用于接收新上传资产的文件夹，并单击 **[!UICONTROL 完成]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 将元数据配置文件从 [!UICONTROL 属性] {#applying-metadata-profiles-to-folders-from-properties}

1. 在左边栏中，单击 **[!UICONTROL 资产]** 然后，导航到要将元数据配置文件应用到的文件夹。
1. 在文件夹中，单击复选标记以将其选中，然后单击 **[!UICONTROL 属性]**.

1. 选择 **[!UICONTROL 元数据配置文件]** 选项卡，从弹出菜单中选择用户档案，然后单击 **[!UICONTROL 保存]**.

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### 从文件夹删除元数据配置文件 {#removing-a-metadata-profile-from-folders}

当您将元数据配置文件从文件夹删除后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。 但是，对文件夹中已发生的文件的任何处理均将保持不变。

您可以从 **[!UICONTROL 工具]** 菜单或 **[!UICONTROL 属性]** 中。

#### 通过配置文件用户界面将元数据配置文件从文件夹删除 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 单击 [!DNL Experience Manager] 徽标和导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.
1. 选择要从一个或多个文件夹删除的元数据配置文件。
1. 单击 **[!UICONTROL 从文件夹删除元数据配置文件]** ，然后选择一个或多个要从中删除配置文件的文件夹并单击 **[!UICONTROL 完成]**.

   您可以确认元数据配置文件不再应用于文件夹，因为该名称不再显示在文件夹名称的下方。

#### 通过属性将元数据配置文件从文件夹删除 {#removing-metadata-profiles-from-folders-via-properties}

1. 单击 [!DNL Experience Manager] 徽标和导航 **[!UICONTROL 资产]** 然后，转到要从中删除元数据配置文件的文件夹。
1. 在文件夹中，单击复选标记以将其选中，然后单击 **[!UICONTROL 属性]**.
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

## 提示和限制 {#best-practices-limitations}

* 通过用户界面更新的元数据更改了 `dc` 命名空间。 通过HTTP API进行的任何更新都会更改 `jcr` 命名空间。 请参阅 [如何使用HTTP API更新元数据](/help/assets/mac-api-assets.md#update-asset-metadata).

* 用于导入资产元数据的CSV文件采用非常特定的格式。 为了节省工作和时间，并避免出现意外错误，您可以开始使用导出的CSV文件格式创建CSV。

* 使用CSV文件导入元数据时，所需的日期格式为 `YYYY-MM-DDThh:mm:ss.fff-00:00`. 如果使用任何其他格式，则不会设置日期值。 导出的元数据CSV文件的日期格式为 `YYYY-MM-DDThh:mm:ss-00:00`. 如果要导入该值，请通过添加表示为的纳秒值，将其转换为可接受的格式 `fff`.

>[!MORELIKETHIS]
>
>* [元数据概念和了解](metadata-concepts.md).
>* [编辑多个收藏集的元数据属性](manage-collections.md#editing-collection-metadata-in-bulk)
>* [在Experience Manager Assets中导入和导出元数据](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
