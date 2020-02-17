---
title: 文件夹元数据架构
description: 了解如何在AEM资产中为资产文件夹创建元数据架构
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
uuid: bf8d066c-0f23-4d18-9ce9-860fa505dea2
discoiquuid: 23009e50-a026-4823-8e4c-7a313a11b38c
docset: aem65
translation-type: tm+mt
source-git-commit: 62cc3282f8d8bc77f072de1d027484bd93efa38a

---


# Folder metadata schema {#folder-metadata-schema}

Adobe Experience Manager(AEM)资产允许您为资产文件夹创建元数据架构，这可定义在文件夹属性页面中显示的布局和元数据。

## 添加文件夹元数据架构表单 {#add-a-folder-metadata-schema-form}

使用文件夹元数据架构表单编辑器可创建和编辑文件夹的元数据架构。

1. 点按／单击AEM徽标，然后转到工具 **** >资 **[!UICONTROL 产]** >文件夹 **[!UICONTROL 元数据架构]**。
1. 在“文件夹元数据架构表单”页中，点按／单击 **[!UICONTROL 创建]**。
1. 指定表单的名称，然后点按／单击创 **[!UICONTROL 建]**。 新架构表单列在“架构表单”页中。

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

您可以编辑新添加的或现有的元数据架构表单，该表单包括：

* 选项卡
* 选项卡中的表单项目

您可以将这些表单项映射到／配置到CRX存储库中元数据节点内的字段。 可以向元数据架构表单中添加新的选项卡或表单项目。

1. 在“架构表单”页中，选择您创建的表单，然后点按／单击工具栏中 **[!UICONTROL 的编辑]** 图标。
1. 在“文件夹元数据架构编辑器”页中，点 `+` 按以向表单添加选项卡。 要重命名选项卡，请点按／单击默认名称，然后在“设置”下指定新 **[!UICONTROL 名称]**。

   ![custom_tab](assets/custom_tab.png)

   要添加更多选项卡，请点按 `+`。 点 `X` 按选项卡以删除它。

1. 在活动选项卡中，从构建表单选项卡中添加一个或 **[!UICONTROL 多个组件]** 。

   ![adding_components](assets/adding_components.png)

   如果创建多个选项卡，请点按／单击特定选项卡以添加组件。

1. To configure a component, select it and modify its properties in the **[!UICONTROL Settings]** tab.

   如果需要，请从“设置”选项卡中删 **[!UICONTROL 除组]** 件。

   ![configure_properties](assets/configure_properties.png)

1. 点按／单 **[!UICONTROL 击工具栏]** 中的保存以保存更改。

### 用于构建表单的组件 {#components-to-build-forms}

The **[!UICONTROL Build Form]** tab lists form items that you use in your folder metadata schema form. The **[!UICONTROL Settings]** tab displays the attributes for each item that you select in the **[!UICONTROL Build Form]** tab. 以下是“构建表单”选项卡中可用的表 **[!UICONTROL 单项目列表]** :

| 组件名称 | 描述 |
|---|---|
| [!UICONTROL 章节标题] | 为公用组件列表添加章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。 它将作为字符串存储。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。在保存资产时，它将作为POST参数发送。 |

### 编辑表单项 {#editing-form-items}

要编辑表单项的属性，请点按／单击组件，然后在设置选项卡中编辑以下全部或一部分属 **[!UICONTROL 性]** 。

**[!UICONTROL 字段标签]**:在文件夹的属性页面上显示的元数据属性的名称。

**[!UICONTROL 映射到属性]**:此属性指定保存文件夹节点的CRX存储库中文件夹节点的相对路径。 It starts with &quot;**./**&quot;，表示路径位于文件夹的节点下。

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`:将该值作为属性存储在文件夹的元数据节点 `dc:title`。

* `./jcr:created`:在文件夹的节点上显示JCR属性。 如果您在CRXDE中配置这些属性，Adobe建议您将它们标记为“禁用编辑”，因为它们受保护。 否则，在保存资 `Asset(s) failed to modify`产的属性时，会出现错误“”。

要确保在元数据架构表单中正确显示组件，请勿在属性路径中包含空格。

**[!UICONTROL JSON路径]**:使用它指定JSON文件的路径，在该路径中为选项指定键值对。

**[!UICONTROL 占位符]**:使用此属性可指定与元数据属性相关的占位符文本。

**[!UICONTROL 选择]**:使用此属性可指定列表中的选项。

**[!UICONTROL 描述]**：使用此属性可添加对元数据组件的简短描述。

**[!UICONTROL 类]**:属性关联的对象类。

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

您可以从“文件夹元数据架构表单”页删除文件夹元数据架构表单。 要删除表单，请选择该表单，然后点按／单击工具栏中的删除图标。

![delete_form](assets/delete_form.png)

## 分配文件夹元数据架构 {#assign-a-folder-metadata-schema}

您可以从“文件夹元数据架构表单”页面或在创建文件夹时，将文件夹元数据架构分配给文件夹。

如果为文件夹配置元数据架构，则架构表单的路径将存储在下的文件 `folderMetadataSchema` 夹节点的属性中。*/jcr:content*。

### 从“文件夹元数据架构”页分配到架构 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 点按／单击AEM徽标，然后转到工具 **[!UICONTROL >资]** 产 **[!UICONTROL >文件夹]**&#x200B;元数据架构 ****。
1. 从“文件夹元数据架构表单”页中，选择要应用到文件夹的架构表单。
1. 在工具栏中，点按／单 **[!UICONTROL 击应用到文件夹]**。

1. 选择要应用架构的文件夹，然后单击／点按应 **[!UICONTROL 用]**。 如果已在文件夹上应用元数据架构，则会显示一条警告消息，通知您将覆盖现有的元数据架构。 点按／单击 **[!UICONTROL 覆盖]**。
1. 打开您应用了元数据架构的文件夹的元数据属性。

   ![folder_properties](assets/folder_properties.png)

   要查看文件夹元数据字段，请点按／单击文件夹元 **[!UICONTROL 数据选项卡]** 。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 创建文件夹时分配架构 {#assign-a-schema-when-creating-a-folder}

在创建文件夹时，可以分配文件夹元数据架构。 如果系统中至少存在一个文件夹元数据架构，则“创建文件夹”对话框中会显示 **[!UICONTROL 额外的列表]** 。 您可以选择所需的架构。 默认情况下，未选择架构。

1. 在AEM资产用户界面中，点按／单击工 **[!UICONTROL 具栏中]** 的创建。
1. 指定文件夹的标题和名称。
1. 从文件夹元数据架构列表中，选择所需的架构。 Then, tap/click **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. 打开您应用了元数据架构的文件夹的元数据属性。
1. 要查看文件夹元数据字段，请点按／单击文件夹元 **[!UICONTROL 数据选项卡]** 。

## 使用文件夹元数据架构 {#use-the-folder-metadata-schema}

打开使用文件夹元数据架构配置的文件夹的属性。 文件 **[!UICONTROL 夹属性页面中会显示]** “文件夹元数据”选项卡。 要查看文件夹元数据架构表单，请选择此选项卡。

在各个字段中输入元数据值，然后点按／单 **[!UICONTROL 击保存]** ，以存储这些值。 您指定的值存储在CRX存储库的文件夹节点中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

