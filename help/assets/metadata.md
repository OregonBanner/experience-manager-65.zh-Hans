---
title: 在中管理数字资产的元数据 [!DNL Adobe Experience Manager]。
description: 了解元数据的类型， [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 以及如何根据资产的元数据自动组织和处理资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d070f5dca569dfb90d3034b74c2940fd68d8ceab
workflow-type: tm+mt
source-wordcount: '2421'
ht-degree: 18%

---


# 管理数字资产的元数据 {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 为每个资产保留元数据。 它可以更轻松地对资产进行分类和组织，并帮助寻找特定资产的用户。 With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. 利用资产的元数据保留和管理功能，您可以根据资产的元数据自动组织和处理资产。

## 元数据及其来源 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 它会添加到资产中，并 [!DNL Experience Manager] 在您上传资产时进行处理。 您可以编辑现有元数据，向现有字段添加新的元数据属性。 组织需要可控、可靠的元数据词汇。 因 [!DNL Experience Manager Assets] 此不允许按需添加新元数据属性。 只有管理员和开发人员才能添加包含元数据的新属性或字段。 用户可以用元数据填充现有字段。

以下方法可用于向数字资产添加元数据：

* 首先，创建资产的本机应用程序会向其添加一些元数据。 例如， [Acrobat向PDF文件](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) 添加一些元数据，或者相机向照片添加一些基本元数据。 在生成资产时，您可以在本机应用程序中添加元数据。 例如，可以在Adobe [Lightroom中添加IPTC元数据](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html)。

* 在将资产上传到之 [!DNL Experience Manager]前，您可以使用用于创建资产的本机应用程序或使用某些其他元数据编辑应用程序来编辑和修改元数据。 当您将资产上传到Experience Manager时，会处理元数据。 例如，了解如何在中 [使用元数据 [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) ，并查 [看中的标记面板 [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html)[!DNL Adobe Exchange]。

* 在中 [!DNL Experience Manager Assets]，您可以在属性页面中手动添加或编辑资产的 [!UICONTROL 元数据] 。

* 在资产上 [传到DAM](/help/assets/metadata-config.md#metadata-profiles) 时，您 [!DNL Experience Manager Assets] 可以利用的元数据用户档案功能自动添加元数据。

## 在 [!DNL Experience Manager Assets] {#add-edit-metadata}

要在用户界面中编辑资产的元数 [!DNL Assets] 据，请执行以下步骤：

1. 执行下列操作之一：

   * 从界面 [!DNL Assets] 中，选择资产，然后单击工 **[!UICONTROL 具栏中的]** 视图“属性”。
   * 从资产缩略图中，选择 **[!UICONTROL 视图属性]** 快速操作。
   * 在资产页面中，单击工 **[!UICONTROL 具栏中]**![的视图](assets/do-not-localize/info-circle-icon.png) 属性资产信息图标。

   资产页面会显示资产的所有元数据。 将资产上传（摄取）到时，会提取元数据 [!DNL Experience Manager]。

   ![选择资产的属性以视图其元数据](assets/asset-metadata.png)

   *图：在资产属性页面上编辑或添 [!UICONTROL 加元] 数据。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有元数据集。 您可以在字段中输入一个值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为XMP数据的一部分写回原始二进制文件。 元数据回写工作流会将元数据添加到原始二进制文件中。 对现有属性（如）所做的更 `dc:title`改将被覆盖，新属性(包括自定义属 `cq:tags`性，如)将随模式添加。

支持并支持技术要求中描述的平台和文件格式 [的XMP写回。](/help/sites-deploying/technical-requirements.md)

## 编辑多个资产的元数据属性 {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] 允许您同时编辑多个资产的元数据，以便快速将通用元数据更改批量传播到资产。 您还可以批量编辑多个集合的元数据。 使用属性页可以对多个资产或收藏集执行元数据更改：

* 将元数据属性更改为通用值
* 添加或修改标记

要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用 [模式编辑器](metadata-config.md#folder-metadata-schema)。

>[!NOTE]
>
>批量编辑方法适用于文件夹或集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](search-assets.md#metadataupdates)。

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，单 **[!UICONTROL 击]** “属性”以打开选定资产的属性页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最常见的父表单。 换言之，属性页面仅显示所有单个资产的属性页面中通用的元数据字段。

1. 修改各个选项卡下选定资产的元数据属性。
1. 要视图特定资产的元数据编辑器，请在列表中取消选择其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在属性页面中，您可以通过取消选择资产来从资产列表中删除资产。 默认情况下，资产列表会选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. 要为资产选择其他元数据模式，请单 **[!UICONTROL 击工]** 具栏中的设置，然后选择所需的模式。
1. 保存更改。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 导入元数据 {#import-metadata}

[!DNL Assets] 允许您使用CSV文件批量导入资产元数据。 您可以通过导入CSV文件，对最近上传的资产或现有资产进行批量更新。 您还可以通过CSV格式从第三方系统批量摄取资产元数据。

元数据导入是异步的，不会影响系统性能。 如果选中了工作流标志，则XMP写回活动会占用大量资源同时更新多个资产的元数据。 在精益服务器使用期间计划此类导入，以便不影响其他用户的性能。

>[!NOTE]
>
>要在自定义命名空间上导入元数据，请首先注册命名空间。

1. 导航到用 [!DNL Assets] 户界面，然后单 **[!UICONTROL 击工]** 具栏中的创建。
1. 从菜单中，选择元 **[!UICONTROL 数据]**。
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. 选择包含元数据的 CSV 文件。
1. 指定以下参数。 请参阅metadata-import- [sample-file.csv上的示例CSV文件](/help/assets/assets/metadata-import-sample-file.csv)。

   | 元数据导入参数 | 描述 |
   |:---|:---|
   | [!UICONTROL 批量大小] | 要为其导入元数据的批处理中的资产数。 默认值为 50。最大值为100。 |
   | [!UICONTROL 字段分隔符] | 默认值 `,` 为（逗号）。 您可以指定任何其他字符。 |
   | [!UICONTROL 多值分隔符] | 元数据值的分隔符。 默认值为 `|`. |
   | [!UICONTROL 启动工作流] | 默认为False。 当设置为 `true` 且默认的启动器设置对DAM元数 [!UICONTROL 据回写工作流(将元数据写入二进制XMP数据] )有效时。 启用启动工作流会减慢系统速度。 |
   | [!UICONTROL 资产路径列名称] | 定义包含资产的CSV文件的列名。 |

1. Click **[!UICONTROL Import]** from the toolbar. 导入元数据后，通知会显示在“通知”收 [!UICONTROL 件箱] 中。

1. 要验证导入是否正确，请导航到资产的“ [!UICONTROL 属性] ”页面，然后验证字段中的值。

要在导入元数据时添加日期和时间戳，请 `YYYY-MM-DDThh:mm:ss.fff-00:00` 使用日期和时间格式。 日期和时间以24小时 `T`格 `hh` 式的小时数分隔，以纳秒 `fff` 为单位，以及时 `-00:00` 区偏移。 例如， `2020-03-26T11:26:00.000-07:00` 2020年3月26日太平洋标准时间上午11点26分00秒。

>[!CAUTION]
>
>如果日期格式不匹配， `YYYY-MM-DDThh:mm:ss.fff-00:00`则不设置日期值。 导出的元数据CSV文件的日期格式为 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要导入它，请通过添加由表示的纳秒值将其转换为可接受的格式 `fff`。

## Export metadata {#export-metadata}

您可以以CSV格式导出多个资产的元数据。 元数据以异步方式导出，不会影响系统性能。 要导出元数据 [!DNL Experience Manager] ，请遍历资产节点及其子节点的 `jcr:content/metadata` 属性，并在CSV文件中导出元数据属性。

批量导出元数据的几个用例包括：

* 迁移资产时，将元数据导入第三方系统。
* 与更广泛的项目团队共享资产元数据。
* 测试或审核元数据以确保合规性。
* 将元数据外部化，以单独进行本地化。

1. 选择包含要导出元数据的资产的资产文件夹。 从工具栏中，选择导 **[!UICONTROL 出元数据]**。

1. 在元数 [!UICONTROL 据导出] 对话框中，指定CSV文件的名称。 要导出子文件夹中资产的元数据，请选择“在子 **[!UICONTROL 文件夹中包含资产”]**。

   ![用于导出文件夹中所有资产的元数据的界面和选](assets/export_metadata_page.png "项用于导出文件夹中所有资产的元数据的界面和选项")

1. 选择所需选项。 提供文件名，并根据需要提供日期。

1. 在要导 **[!UICONTROL 出的属性字段中]** ，指定是要导出全部属性还是要导出特定属性。 如果选择要导出的选择性属性，请添加所需的属性。

1. 在工具栏中，单击“ **[!UICONTROL 导出]**”。 系统会显示一条消息，确认已导出元数据。 关闭消息。

1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. 单击&#x200B;**[!UICONTROL 关闭]**。

   ![用于下载包含批量导出的元数据的CSV文件的对话框](assets/csv_download.png)

   *图：用于下载包含批量导出的元数据的CSV文件的对话框。*

## 编辑集合的元数据 {#collections-metadata}

有关详细信息，请 [参阅视图和编辑集合元数据](/help/assets/manage-collections.md#view-edit-collection-metadata) , [以及批量编辑多个集合的元数据](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk)。

## Apply a metadata profile to folders {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

当您将元数据配置文件分配给文件夹之后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。这就意味着您只能为每个文件夹分配一个元数据配置文件。因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果您为文件夹分配了一个不同的元数据配置文件，新配置文件就会取代之前的配置文件。此前存在的文件夹资产将保持不变。新用户档案将应用于稍后添加到该文件夹的资产。

在用户界面中，卡名称中显示的用户档案名称会指示已为其分配用户档案的文件夹。

![卡视图显示应用于文件夹的元数据用户档案](assets/metadata-profile-card-view-display.png)

您可以将元数据用户档案应用于特定文件夹或全局应用于所有资产。

您可以重新处理文件夹中的资产，该文件夹中已经存在稍后更改的元用户档案。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理文件夹中的资产，该文件夹中已经有您稍后更改的现有视频用户档案。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

### Apply metadata profiles to folders from [!UICONTROL Profiles] user interface {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

请按照以下步骤应用元数据用户档案:

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. 选择您要应用到一个或多个文件夹的元数据配置文件。
1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 从“属性”将元数据用户档案应用到文 [!UICONTROL 件夹] {#applying-metadata-profiles-to-folders-from-properties}

1. In the left rail, click **[!UICONTROL Assets]** then navigate to the folder that you want to apply a metadata profile to.
1. 在文件夹中，单击复选标记以将其选中，然后单击“属 **[!UICONTROL 性”]**。

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the popup menu and click **[!UICONTROL Save]**.

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### Remove a metadata profile from folders {#removing-a-metadata-profile-from-folders}

当您将元数据配置文件从文件夹删除之后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。但是，此前对文件夹中的文件所做的处理均予以保留。

您可以从工具菜单或文件夹的属性 **[!UICONTROL 中]** ，将元数据 **[!UICONTROL 用户档案]** 从文件夹删除。

#### Remove metadata profiles from folders via Profiles user interface {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. 选择您要从一个或多个文件夹删除的元数据配置文件。
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   您可以确认元数据用户档案不再应用于文件夹，因为该名称不再显示在文件夹名称的下方。

#### 通过“属性”将元数据用户档案从文件夹删除 {#removing-metadata-profiles-from-folders-via-properties}

1. 单击标 [!DNL Experience Manager] 志并导航 **[!UICONTROL 资产]** ，然后导航到您要从中删除元数据用户档案的文件夹。
1. 在文件夹中，单击复选标记以将其选中，然后单击“属 **[!UICONTROL 性”]**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

## 提示和限制 {#best-practices-limitations}

* 通过用户界面进行的元数据更新会更改命名空间中的元数据 `dc` 属性。 通过HTTP API进行的任何更新都会更改命名空间中的元数据属 `jcr` 性。 了 [解如何使用HTTP API更新元数据](/help/assets/mac-api-assets.md#update-asset-metadata)。

* 用于导入资产元数据的CSV文件采用非常特定的格式。 要节省工作和时间并避免出现意外错误，您可以开始使用导出的CSV文件格式创建CSV。

* 使用CSV文件导入元数据时，所需的日期格式为日 `YYYY-MM-DDThh:mm:ss.fff-00:00`期。 如果使用了任何其他格式，则不设置日期值。 导出的元数据CSV文件的日期格式为 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要导入它，请通过添加由表示的纳秒值将其转换为可接受的格式 `fff`。

>[!MORELIKETHIS]
>
>* [元数据概念和理解](metadata-concepts.md)。
>* [编辑多个集合的元数据属性](manage-collections.md#editing-collection-metadata-in-bulk)
>* [在Experience Manager资产中导入和导出元数据](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


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
