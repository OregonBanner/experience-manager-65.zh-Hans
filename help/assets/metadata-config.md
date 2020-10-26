---
title: 元数据功能的配置和管理。
description: 与元数据添 [!DNL Experience Manager Assets] 加和管理相关的配置和管理功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 12%

---


# 配置和管理 [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 为每个资产保留元数据。 它可以更轻松地对资产进行分类和组织，并帮助寻找特定资产的用户。 利用资产的元数据保留和管理功能，您可以根据资产的元数据自动组织和处理资产。 [!DNL Adobe Experience Manager Assets] 允许管理员配置和自定义元数据功能以修改默认的Adobe功能。

## 编辑元数据模式 {#metadata-schema}

有关详细信息，请参 [阅编辑元数据模式表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中添加您自己的命名空间 [!DNL Experience Manager]。 正如存在预定义的命名空间 `cq`, `jcr`如、 `sling`和，您可以对存储库元数据和XML处理进行命名空间。

1. 访问节点类型管理页 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`面。
1. 要访问命名空间管理页面，请 **[!UICONTROL 单击]** 页面顶部的命名空间。
1. 要添加命名空间, **[!UICONTROL 请单]** 击页面底部的“新建”。
1. 在XML命名空间约定中指定自定义命名空间。 以URI的形式指定ID，并为ID指定关联前缀。 单击&#x200B;**[!UICONTROL 保存]**。

## 配置批量元数据更新的限制 {#bulk-metadata-update-limit}

为防止出现类似拒绝服务(DOS)的情况， [!DNL Enterprise Manager] 请限制Sling请求中支持的参数数。 在一次性更新多个资产的元数据时，您可能会达到限制，并且不会更新更多资产的元数据。 Enterprise Manager在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

## 元数据配置文件 {#metadata-profiles}

元数据用户档案允许您将默认元数据应用到文件夹内的资产。创建元数据用户档案并将其应用到文件夹。您随后上传到文件夹的任何资产都会继承您在元数据用户档案中配置的默认元数据。

### 添加元数据用户档案 {#adding-a-metadata-profile}

1. 导航到工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]** >元 **[!UICONTROL 数据用户档案，然]** 后单 **[!UICONTROL 击创建]**。
1. 例如，输入用户档案的标题， `Sample Metadata`然后单击创 **[!UICONTROL 建]**。 The [!UICONTROL Edit Form] for the metadata profile is displayed.

   ![编辑元数据表单](assets/metadata-edit-form.png)

1. Click a component and configure its properties in the **[!UICONTROL Settings]** tab. For example, click the **[!UICONTROL Description]** component and edit its properties.

   ![在元数据用户档案中设置组件](assets/metadata-profile-component-setting.png)

   Edit the following properties for the **[!UICONTROL Description]** component:

   * **[!UICONTROL 字段标签]**:元数据属性的显示名称。 仅供用户参考。

   * **[!UICONTROL 映射到属性]**:此属性的值提供资产节点在存储库中保存的相对路径或名称。 该值应始终与开始 `./` ，因为它指示该路径位于资产的节点下。

   ![映射到元数据用户档案中的属性设置](assets/metadata-profile-setting-map-property.png)

   您为&#x200B;**[!UICONTROL 映射到属性]**&#x200B;指定的值会作为属性存储在资产的元数据节点下。例如，如果指定 `./jcr:content/metadata/dc:desc` 为映射到属 **[!UICONTROL 性的名称]**, [!DNL Assets] 则会将该 `dc:desc` 值存储在资产的元数据节点。

   * **[!UICONTROL 默认值]**：使用此属性可为元数据组件添加默认值。For example, if you specify &quot;My description&quot; then this value is assigned to the property `dc:desc` at the asset&#39;s metadata node.

   ![在元数据用户档案中设置默认描述](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >向新元数据属性添加默认值（在中尚不存在）。 `/jcr:content/metadata` 节点)默认情况下不在资产的“属性”页面上显示属性及其值。 要视图资产的“属性”页面 [!UICONTROL 上的] 新属性，请修改相应的模式表单。

1. （可选）从“构建表单”选项卡中向“编辑表单”添 **[!UICONTROL 加更多组件]** ，然后在“设置”选项卡中配置 **[!UICONTROL 其属性]** 。 “构建表单”选项卡中提供 **[!UICONTROL 以下属性]** :

| 组件 | 属性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 章节标题] | 字段标签，说 <br> 明 |
| [!UICONTROL 单行文本] | 字段标签 <br> 、映射到属性、 <br> 默认值 |
| [!UICONTROL 多值文本] | 字段标签 <br> 、映射到属性、 <br> 默认值 |
| [!UICONTROL 数字] | 字段标签 <br> 、映射到属性、 <br> 默认值 |
| [!UICONTROL 日期] | 字段标签 <br> 、映射到属性、 <br> 默认值 |
| [!UICONTROL 标准标记] | 字段标签 <br> 、映射到属性、 <br> 默认值、说 <br> 明 |

1. 单击&#x200B;**[!UICONTROL 完成]**。The Metadata Profile is added to the list of profiles in the **[!UICONTROL Metadata Profiles]** page.<br>

   ![元数据用户档案添加到元数据用户档案页](assets/MetadataProfiles-page.png)

### 复制元数据用户档案 {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a metadata profile to make a copy of it.

   ![复制元数据用户档案](assets/metadata-profile-edit-copy-option.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. 在&#x200B;**[!UICONTROL 复制元数据配置文件]**&#x200B;对话框中，为元数据配置文件的新副本输入标题。
1. 单击&#x200B;**[!UICONTROL 复制]**。元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

   ![在“元数据用户档案”页面中添加的元数据用户档案的副本](assets/copy-metadata-profile.png)

### 删除元数据用户档案 {#deleting-a-metadata-profile}

1. 在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择要删除的配置文件。

1. 单击 **[!UICONTROL 工具栏中的]** “删除元数据”用户档案。
1. In the dialog, click **[!UICONTROL Delete]** to confirm the delete operation. The metadata profile is deleted from the list.

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

## 文件夹的元数据模式 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 允许您为资产文件夹创建元数据架构，这些架构定义了文件夹属性页面中显示的布局和元数据。

### 添加文件夹元数据模式表单 {#add-a-folder-metadata-schema-form}

使用文件夹元数据模式Forms编辑器创建和编辑文件夹的元数据模式。

1. 在界 [!DNL Experience Manager] 面中，转至 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >文件 **[!UICONTROL 夹元数]**&#x200B;据模式。
1. 在“文件 [!UICONTROL 夹元数据模式”] “Forms”页 **[!UICONTROL 面上，单击]**“创建”。
1. Specify a name for the form, and click **[!UICONTROL Create]**. 新的模式表单列在 [!UICONTROL 模式Forms] 。

### Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

您可以编辑新添加的或现有的元数据模式表单，其中包括：

* 选项卡
* 选项卡中的表单项目

您可以将这些表单项映射到／配置到CRX存储库中元数据节点内的字段。 可以向元数据架构表单中添加新的选项卡或表单项目。

1. 在“模式Forms”页面中，选择您创建的表单，然后从工具栏 **[!UICONTROL 中选]** 择编辑选项。
1. 在“文件夹元数据模式编辑器”页 `+` 面中，单击以向表单添加选项卡。 要重命名选项卡，请单击默认名称，并在“设置”下指定新 **[!UICONTROL 名称]**。

   ![custom_tab](assets/custom_tab.png)

   要添加更多选项卡，请单击 `+`。 单击 `X` 选项卡以将其删除。

1. 在活动选项卡中，从构建表单选项卡中添加一个或 **[!UICONTROL 多个组件]** 。

   ![adding_components](assets/adding_components.png)

   如果创建多个选项卡，请单击特定选项卡以添加组件。

1. To configure a component, select it and modify its properties in the **[!UICONTROL Settings]** tab.

   如果需要，请从“设置”选项卡中 **[!UICONTROL 删除组]** 件。

   ![configure_properties](assets/configure_properties.png)

1. 单击 **[!UICONTROL 工具栏]** 中的保存以保存更改。

#### 用于构建表单的组件 {#components-to-build-forms}

The **[!UICONTROL Build Form]** tab lists form items that you use in your folder metadata schema form. The **[!UICONTROL Settings]** tab displays the attributes for each item that you select in the **[!UICONTROL Build Form]** tab. 下面是“构建表单”选项卡中可用的表 **[!UICONTROL 单项的列表]** :

| 组件名称 | 描述 |
|---|---|
| [!UICONTROL 章节标题] | 添加一列表常用组件的章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。 它将作为字符串存储。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。在保存资产时，它将作为POST参数发送。 |

#### 编辑表单项 {#editing-form-items}

要编辑表单项的属性，请单击该组件，然后在设置选项卡中编辑以下全部属性或一 **[!UICONTROL 部分]** 属性。

**[!UICONTROL 字段标签]**:在文件夹的属性页面上显示的元数据属性的名称。

**[!UICONTROL 映射到属性]**:此属性指定保存文件夹节点的CRX存储库中的相对路径。 It starts with &quot;**./**&quot; ，表示路径位于文件夹的节点下。

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`:将该值作为属性存储在文件夹的元数据节点 `dc:title`。

* `./jcr:created`:在文件夹的节点上显示JCR属性。 如果您在CRXDE中配置这些属性，Adobe建议您将它们标记为“禁用编辑”，因为它们是受保护的。 否则，在保存 `Asset(s) failed to modify`资产的属性时，会出现错误“”。

要确保在元数据模式表单中正确显示组件，请勿在属性路径中包含空格。

**[!UICONTROL JSON路径]**:使用它指定JSON文件的路径，在该路径中为选项指定键值对。

**[!UICONTROL 占位符]**:使用此属性可指定与元数据属性相关的占位符文本。

**[!UICONTROL 选择]**:使用此属性指定列表中的选项。

**[!UICONTROL 描述]**：使用此属性可添加对元数据组件的简短描述。

**[!UICONTROL 类]**:属性关联的对象类。

### Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

您可以从“文件夹元数据模式”Forms页删除文件夹元数据模式表单。 要删除表单，请选择表单，然后单击工具栏中的删除选项。

![delete_form](assets/delete_form.png)

### 分配文件夹元数据模式 {#assign-a-folder-metadata-schema}

您可以从“文件夹元数据模式”Forms页或在创建文件夹时，将文件夹元数据模式分配给文件夹。

如果为文件夹配置元数据模式，则模式表单的路径将存储在文件夹 `folderMetadataSchema` 节点下的属性中 `./jcr:content`。

#### 从“文件夹元数据”模式页面分配给模式 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 在界 [!DNL Experience Manager] 面中，转至 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >文件 **[!UICONTROL 夹元数]**&#x200B;据模式。
1. 从“文件夹元数据模式Forms”页面，选择要应用于文件夹的模式表单。
1. 在工具栏中，单 **[!UICONTROL 击“应用到文件夹”]**。

1. 选择要应用模式的文件夹，然后单击“应 **[!UICONTROL 用]**”。 如果已在文件夹上应用元数据模式，则会显示一条警告消息，通知您将覆盖现有元数据模式。 单击“ **[!UICONTROL 覆盖]**”。
1. 打开应用元数据模式的文件夹的元数据属性。

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 创建文件夹时分配模式 {#assign-a-schema-when-creating-a-folder}

您可以在创建文件夹时分配文件夹元数据模式。 如果系统中至少存在一个文件夹元数据模式，则“创建文件夹”对话框中会显 **[!UICONTROL 示额外的列表]** 。 您可以选择所需的模式。 默认情况下，不选择模式。

1. 在用户 [!DNL Experience Manager Assets] 界面中，单击工 **[!UICONTROL 具栏]** 中的创建。
1. 指定文件夹的标题和名称。
1. 从文件夹元数据模式列表中，选择所需的模式。 然后，单击“ **[!UICONTROL 创建]**”。

   ![select_模式](assets/select_schema.png)

1. 打开应用元数据模式的文件夹的元数据属性。
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

### 使用文件夹元数据模式 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹属性。A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. 要查看文件夹元数据架构表单，请选择此选项卡。

在各个字段中输入元数据值，然 **[!UICONTROL 后单击]** “保存”以存储这些值。 您指定的值存储在CRX存储库的文件夹节点中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示和限制 {#best-practices-limitations}

* 要在自定义命名空间上导入元数据，请首先注册命名空间。
* 属性选取器显示用于模式编辑器和搜索表单的属性。 属性选取器不会从资产中选取元数据属性。
* 升级到6.5之前，您可能已存在先前存在的元数据用户档案 [!DNL Experience Manager] 。升级后，如果在“元数据用户档案”选项卡的“文件夹属 [!UICONTROL 性] ”中应  用此用户档案，则不会显示元数据表单字段。 但是，如果应用新创建的元数据用户档案，则表单字段将显示但不可用（如预期）。 功能不会丢失，但如果要查看（不可用）表单字段，请编辑并保存现有元数据用户档案。

>[!MORELIKETHIS]
>
>* [元数据概念和理解](metadata-concepts.md)。
>* [编辑多个集合的元数据属性](manage-collections.md#editing-collection-metadata-in-bulk)。
>* [在Experience Manager资产中导入和导出元数据](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)。
>* [用户档案处理元数据、图像和视频](processing-profiles.md)。
>* [组织数字资产以使用处理用户档案的最佳实践](/help/assets/organize-assets.md)。
>* [XMP写回](/help/assets/xmp-writeback.md)。

