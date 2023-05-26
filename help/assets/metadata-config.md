---
title: 元数据功能的配置和管理。
description: 配置和管理 [!DNL Experience Manager Assets] 与元数据添加和管理相关的功能。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 4%

---

# 中元数据功能的配置和管理 [!DNL Assets] {#config-metadata}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | 本文 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每个资源的元数据。 它允许更轻松地分类和组织资产，并且有助于寻找特定资产的人员。 利用使用资源保留和管理元数据的功能，您可以根据资源的元数据自动组织和处理资源。 [!DNL Adobe Experience Manager Assets] 允许管理员配置和自定义元数据功能，以修改默认的Adobe方案。

## 编辑元数据架构 {#metadata-schema}

有关详细信息，请参阅 [编辑元数据架构表单](metadata-schemas.md#edit-metadata-schema-forms).

## 在中注册自定义命名空间 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中添加自己的命名空间 [!DNL Experience Manager]. 正如预定义的命名空间一样，例如 `cq`， `jcr`、和 `sling`，您可以为存储库元数据和XML处理使用命名空间。

1. 访问“节点类型管理”页 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. 要访问“命名空间管理”页，请单击 **[!UICONTROL 命名空间]** 页面顶部的。
1. 要添加命名空间，请单击 **[!UICONTROL 新]** 页面底部的。
1. 在XML命名空间约定中指定自定义命名空间。 以URI的形式指定ID，并为ID指定关联的前缀。 单击“**[!UICONTROL 保存]**”。

## 配置批量元数据更新的限制 {#bulk-metadata-update-limit}

要防止出现拒绝服务(DOS)情况， [!DNL Enterprise Manager] 限制Sling请求中支持的参数数量。 一次更新多个资源的元数据时，您可能达到限制，并且元数据未针对更多资源进行更新。 Enterprise Manager在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

要更改限制，请访问 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 并更改 **[!UICONTROL 最大POST参数]** 在 **[!UICONTROL Apache Sling请求参数处理]** osgi配置。

## 元数据配置文件 {#metadata-profiles}

元数据配置文件允许您将默认元数据应用到文件夹中的资源。 创建元数据配置文件并将其应用到文件夹。 您稍后上传到文件夹的任何资源都会继承您在元数据配置文件中配置的默认元数据。

### 添加元数据配置文件 {#adding-a-metadata-profile}

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]** 并单击 **[!UICONTROL 创建]**.
1. 输入用户档案的标题，例如 `Sample Metadata`，然后单击 **[!UICONTROL 创建]**. 此 [!UICONTROL 编辑表单] 此时将显示元数据配置文件的。

   ![编辑元数据表单](assets/metadata-edit-form.png)

1. 单击某个组件并在中配置其属性 **[!UICONTROL 设置]** 选项卡。 例如，单击 **[!UICONTROL 描述]** 组件并编辑其属性。

   ![在元数据配置文件中设置组件](assets/metadata-profile-component-setting.png)

   编辑以下属性 **[!UICONTROL 描述]** 组件：

   * **[!UICONTROL 字段标签]**：元数据属性的显示名称。 仅供用户参考。

   * **[!UICONTROL 映射到属性]**：此属性的值提供资产节点的相对路径或名称，资产节点会保存在存储库中。 该值应始终以开头 `./` 因为它指示路径在资产的节点下。

   ![映射到元数据配置文件中的属性设置](assets/metadata-profile-setting-map-property.png)

   您为指定的值 **[!UICONTROL 映射到属性]** 作为属性存储在资产的元数据节点下。 例如，如果您指定 `./jcr:content/metadata/dc:desc` 作为的名称 **[!UICONTROL 映射到属性]**， [!DNL Assets] 存储值 `dc:desc` 在资产的元数据节点上。 Adobe建议只将一个字段映射到元数据架构中的给定属性。 否则，系统会选取映射到资产的最新添加字段。

   * **[!UICONTROL 默认值]**：使用此属性为元数据组件添加默认值。 例如，如果您指定“My description”，则此值将分配给属性 `dc:desc` 在资产的元数据节点上。

   ![在元数据配置文件中设置默认描述](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >向新元数据属性添加默认值(该属性不存在于 `/jcr:content/metadata` 节点)不会将属性及其值显示在资产的 [!UICONTROL 属性] 默认页面。 要查看资产的新资产，请执行以下操作 [!UICONTROL 属性] 页面，修改相应的架构表单。

1. （可选）在 **[!UICONTROL 构建表单]** 选项卡，添加更多组件到 [!UICONTROL 编辑表单]，并在中配置其属性 **[!UICONTROL 设置]** 选项卡。 以下属性位于 **[!UICONTROL 构建表单]** 选项卡：

| 组件 | 属性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 章节标题] | 字段标签， <br> 描述 |
| [!UICONTROL 单行文本] | 字段标签， <br> 映射到属性， <br> 默认值 |
| [!UICONTROL 多值文本] | 字段标签， <br> 映射到属性， <br> 默认值 |
| [!UICONTROL 数字] | 字段标签， <br> 映射到属性， <br> 默认值 |
| [!UICONTROL 日期] | 字段标签， <br> 映射到属性， <br> 默认值 |
| [!UICONTROL 标准标记] | 字段标签， <br> 映射到属性， <br> 默认值， <br> 描述 |

1. 单击 **[!UICONTROL 完成]**. 元数据配置文件将添加到中的配置文件列表 **[!UICONTROL 元数据配置文件]** 页面。<br>

   ![元数据配置文件页面中添加了元数据配置文件](assets/MetadataProfiles-page.png)

### 复制元数据配置文件 {#copying-a-metadata-profile}

1. 从 **[!UICONTROL 元数据配置文件]** 页面上，选择一个元数据配置文件以制作该配置文件的副本。

   ![复制元数据配置文件](assets/metadata-profile-edit-copy-option.png)

1. 单击 **[!UICONTROL 复制]** 工具栏中。
1. 在 **[!UICONTROL 复制元数据配置文件]** 对话框，为元数据配置文件的新副本输入标题。
1. 单击 **[!UICONTROL 复制]**. 元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

   ![元数据配置文件页面中添加了元数据配置文件的副本](assets/copy-metadata-profile.png)

### 删除元数据配置文件 {#deleting-a-metadata-profile}

1. 从 **[!UICONTROL 元数据配置文件]** 页面上，选择要删除的配置文件。

1. 单击 **[!UICONTROL 删除元数据配置文件]** 工具栏中。
1. 在对话框中，单击 **[!UICONTROL 删除]** 以确认删除操作。 元数据配置文件将从列表中删除。

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## 文件夹的元数据架构 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 允许您为资源文件夹创建元数据架构，这些架构定义文件夹属性页面中显示的布局和元数据。

### 添加文件夹元数据架构表单 {#add-a-folder-metadata-schema-form}

使用文件夹元数据架构Forms编辑器为文件夹创建和编辑元数据架构。

1. In [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 文件夹元数据架构]**.
1. 在 [!UICONTROL 文件夹元数据架构Forms] 页面，单击 **[!UICONTROL 创建]**.
1. 指定表单的名称，然后单击 **[!UICONTROL 创建]**. 新架构表单列在 [!UICONTROL 架构Forms] 页面。

### 编辑文件夹元数据架构表单 {#edit-folder-metadata-schema-forms}

您可以编辑新添加或现有元数据架构表单，其中包含以下内容：

* 选项卡
* 选项卡中的表单项目。

您可以将这些表单项映射/配置到CRX存储库中元数据节点内的字段。 您可以将新选项卡或表单项添加到元数据架构表单。

1. 在“架构Forms”页面中，选择您创建的表单，然后选择 **[!UICONTROL 编辑]** 选项。
1. 在“文件夹元数据架构编辑器”页面中，单击 `+` 以向表单中添加选项卡。 要重命名选项卡，请单击默认名称，并在下指定新名称 **[!UICONTROL 设置]**.

   ![custom_tab](assets/custom_tab.png)

   要添加更多选项卡，请单击 `+`. 要删除，请单击 `X` 在选项卡上。

1. 在活动选项卡中，从 **[!UICONTROL 构建表单]** 选项卡。

   ![adding_components](assets/adding_components.png)

   如果创建多个选项卡，请单击特定选项卡以添加组件。

1. 要配置组件，请选择该组件并在 **[!UICONTROL 设置]** 选项卡。

   如有必要，请从以下位置删除组件 **[!UICONTROL 设置]** 选项卡。

   ![configure_properties](assets/configure_properties.png)

1. 要保存更改，请选择 **[!UICONTROL 保存]** 工具栏中。

#### 用于构建表单的组件 {#components-to-build-forms}

此 **[!UICONTROL 构建表单]** 选项卡列出了您在文件夹元数据架构表单中使用的表单项。 此 **[!UICONTROL 设置]** 选项卡显示您在选项中选择的每个项目的属性 **[!UICONTROL 构建表单]** 选项卡。 以下是中可用的表单项目列表 **[!UICONTROL 构建表单]** 选项卡：

| 组件名称 | 描述 |
|---|---|
| [!UICONTROL 章节标题] | 为常用组件列表添加章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。 它以字符串形式存储。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。 它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。 保存资源时，此参数将作为POST参数发送。 |

#### 编辑表单项目 {#editing-form-items}

要编辑表单项目的属性，请单击该组件，然后在组件中编辑以下属性的全部或子集 **[!UICONTROL 设置]** 选项卡。

**[!UICONTROL 字段标签]**：在文件夹的属性页面上显示的元数据属性的名称。

**[!UICONTROL 映射到属性]**：此属性指定保存它的CRX存储库中文件夹节点的相对路径。 它始于&quot;**./**“”，表示路径在文件夹的节点下。

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`：将该值作为属性存储在文件夹的元数据节点中 `dc:title`.

* `./jcr:created`：在文件夹的节点显示JCR属性。 如果您在CRXDE中配置这些属性，Adobe建议您将它们标记为“禁用编辑”，因为它们受到保护。 否则，出现错误&#39; `Asset(s) failed to modify`”在保存资产的属性时发生。

要确保组件在元数据架构表单中正确显示，请不要在属性路径中包含空格。

**[!UICONTROL JSON路径]**：使用它指定JSON文件的路径，您可以在其中为选项指定键值对。

**[!UICONTROL 占位符]**：使用此属性指定与元数据属性相关的占位符文本。

**[!UICONTROL 选项]**：使用此属性指定列表中的选项。

**[!UICONTROL 描述]**：使用此属性可添加对元数据组件的简短描述。

**[!UICONTROL 类]**：与属性关联的对象类。

### 删除文件夹元数据架构表单 {#delete-folder-metadata-schema-forms}

您可以从“文件夹元数据架构Forms”页面中删除文件夹元数据架构表单。 要删除表单，请选择该表单，然后单击工具栏中的删除选项。

![delete_form](assets/delete_form.png)

### 分配文件夹元数据架构 {#assign-a-folder-metadata-schema}

您可以从“文件夹元数据架构Forms”页面或在创建文件夹时，将文件夹元数据架构分配给文件夹。

如果为文件夹配置元数据架构，则架构表单的路径将存储在 `folderMetadataSchema` 下的文件夹节点的属性 `./jcr:content`.

#### 从“文件夹元数据架构”页分配给架构 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. In [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 文件夹元数据架构]**.
1. 从“文件夹元数据架构Forms”页面中，选择要应用于文件夹的架构表单。
1. 在工具栏中，单击 **[!UICONTROL 应用到文件夹]**.

1. 选择要应用架构的文件夹，然后单击 **[!UICONTROL 应用]**. 如果元数据架构已应用于文件夹，则会显示一条警告消息，通知您即将覆盖现有的元数据架构。 单击 **[!UICONTROL 覆盖]**.
1. 打开将元数据架构应用到的文件夹的元数据属性。

   ![folder_properties](assets/folder_properties.png)

   要查看文件夹元数据字段，请单击 **[!UICONTROL 文件夹元数据]** 选项卡。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 创建文件夹时分配架构 {#assign-a-schema-when-creating-a-folder}

您可以在创建文件夹时分配文件夹元数据架构。 如果系统中至少存在一个文件夹元数据架构，则会在 **[!UICONTROL 创建文件夹]** 对话框。 您可以选择所需的架构。 默认情况下，未选择架构。

1. 从 [!DNL Experience Manager Assets] 用户界面，单击 **[!UICONTROL 创建]** 工具栏中。
1. 指定文件夹的标题和名称。
1. 从文件夹元数据架构列表中，选择所需的架构。 然后，单击 **[!UICONTROL 创建]**.

   ![select_schema](assets/select_schema.png)

1. 打开将元数据架构应用到的文件夹的元数据属性。
1. 要查看文件夹元数据字段，请单击 **[!UICONTROL 文件夹元数据]** 选项卡。

### 使用文件夹元数据架构 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹属性。A **[!UICONTROL 文件夹元数据]** 选项卡显示在文件夹中 [!UICONTROL 属性] 页面。 要查看文件夹元数据架构表单，请选择此选项卡。

在各个字段中输入元数据值，然后单击 **[!UICONTROL 保存]** 以存储值。 您指定的值存储在CRX存储库的文件夹节点中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示和限制 {#best-practices-limitations}

* 要在自定义命名空间上导入元数据，请先注册命名空间。
* 属性选取器显示架构编辑器和搜索表单中使用的属性。 属性选取器不会从资源中选取元数据属性。
* 在升级到之前，您可能已经存在元数据配置文件 [!DNL Experience Manager] 6.5.升级后，如果在文件夹中应用此类配置文件 [!UICONTROL 属性] 在 [!UICONTROL 元数据配置文件] 选项卡，元数据表单字段不显示。 但是，如果您应用新创建的元数据配置文件，则表单字段会显示，但会按预期不可用。 不会丢失任何功能，但如果您希望查看（不可用）表单字段，请编辑并保存现有的元数据配置文件。

>[!MORELIKETHIS]
>
>* [元数据概念和了解](metadata-concepts.md).
>* [编辑多个收藏集的元数据属性](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Experience Manager Assets中的元数据导入和导出](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [用于处理元数据、图像和视频的用户档案](processing-profiles.md).
>* [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).
>* [XMP写回](/help/assets/xmp-writeback.md).

