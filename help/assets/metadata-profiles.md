---
title: 元数据用户档案，用于自定义资产的元数据要求
description: 了解资产的元数据用户档案。 了解如何创建元数据用户档案并将其应用到文件夹资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 元数据配置文件 {#metadata-profiles}

元数据用户档案允许您将默认元数据应用于文件夹内的资产。创建元数据用户档案并将其应用到文件夹。您随后上传到文件夹的任何资产都会继承您在元数据用户档案中配置的默认元数据。

## 添加元数据用户档案 {#adding-a-metadata-profile}

1. 导航到工 **[!UICONTROL 具>资产>元数据用户档案]** ，然后点 **[!UICONTROL 按创建]**。
1. 为元数据用户档案（例如，示例元数据）输入标题，然后点按创 **[!UICONTROL 建]**。 The [!UICONTROL Edit Form] for the metadata profile is displayed.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Click a component and configure its properties in the **[!UICONTROL Settings]** tab. For example, click the **[!UICONTROL Description]** component and edit its properties.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Edit the following properties for the **[!UICONTROL Description]** component:

   * **[!UICONTROL 字段标签]**:元数据属性的显示名称。 仅供用户参考。

   * **[!UICONTROL 映射到属性]**:此属性的值提供资产节点在存储库中保存的相对路径／名称。该值应始终与开始, `./` 因为它指示该路径位于资产的节点下。
   ![chlimage_1-199](assets/chlimage_1-482.png)

   您为&#x200B;**[!UICONTROL 映射到属性]**&#x200B;指定的值会作为属性存储在资产的元数据节点下。例如，如果您指定`/jcr:content/metadata/dc:desc` 作为映射到属 **[!UICONTROL 性的名称]**,AEM资产会将该值存储在资 `dc:desc` 产的元数据节点。

   * **[!UICONTROL 默认值]**：使用此属性可为元数据组件添加默认值。For example, if you specify &quot;My description&quot; then this value is assigned to the property `dc:desc` at the asset&#39;s metadata node.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >将默认值添加到新的元数据属性(该属性在中尚不存在。( `/jcr:content/metadata` 节点)默认情况下不在资产的“属性”页面上显示属性及其值。 要视图资产“属性”页面上的新属 [!UICONTROL 性] ，请修改相应的模式表单。

1. （可选）从“构建表单”选项卡中向“编辑表单”添 **[!UICONTROL 加更多组件]** ，然后在“设置”选项卡中配置 **[!UICONTROL 其属性]** 。 “构建表单”选项卡中提供 **[!UICONTROL 以下属性]** :

| 组件 | 属性 |
|---|---|
| [!UICONTROL 章节标题] | 字段标签，说 <br> 明 |
| [!UICONTROL 单行文本] | 字段标签， <br> 映射到属性，默 <br> 认值 |
| [!UICONTROL 多值文本] | 字段标签， <br> 映射到属性，默 <br> 认值 |
| [!UICONTROL 数字] | 字段标签， <br> 映射到属性，默 <br> 认值 |
| [!UICONTROL 日期] | 字段标签， <br> 映射到属性，默 <br> 认值 |
| [!UICONTROL 标准标记] | 字段标签， <br> 映射到属性，默 <br> 认值，说 <br> 明 |

![chlimage_1-201](assets/chlimage_1-484.png)

1. 点按／单击 **[!UICONTROL 完成]**。 The Metadata Profile is added to the list of profiles in the **[!UICONTROL Metadata Profiles]** page.<br>


   ![元数据用户档案已添加到元数据用户档案页](assets/MetadataProfiles-page.png)

## 复制元数据用户档案 {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a metadata profile to make a copy of it.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. 点按 **[!UICONTROL 工具栏]** 中的复制。
1. 在&#x200B;**[!UICONTROL 复制元数据配置文件]**&#x200B;对话框中，为元数据配置文件的新副本输入标题。
1. 点按&#x200B;**[!UICONTROL 复制]**。元数据配置文件的副本将显示在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面的配置文件列表中。

   ![在元数据用户档案页面中添加的元数据用户档案副本](assets/copy-metadata-profile.png)

## 删除元数据用户档案 {#deleting-a-metadata-profile}

1. 在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择要删除的配置文件。

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. 选项卡[]**[!UICONTROL 删除工具栏中的元数据用户档案]** 。
1. In the dialog, click **[!UICONTROL Delete]** to confirm the delete operation. The metadata profile is deleted from the list.

## Apply a metadata profile to folders {#applying-a-metadata-profile-to-folders}

当您将元数据配置文件分配给文件夹之后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。这就意味着您只能为每个文件夹分配一个元数据配置文件。因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果您为文件夹分配了一个不同的元数据配置文件，新配置文件就会取代之前的配置文件。此前存在的文件夹资产将保持不变。新用户档案将应用于稍后添加到该文件夹的资产。

在用户界面中，为其分配了用户档案的文件夹会以卡名称中显示的用户档案名称来指示。

![chlimage_1-205](assets/chlimage_1-489.png)

您可以将元数据用户档案应用到特定文件夹或全局应用于所有资产。

您可以重新处理文件夹中的资产，该文件夹中已经有一个现有的元数据用户档案，您稍后会更改该元数据。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

### 将元数据用户档案应用到特定文件夹 {#applying-metadata-profiles-to-specific-folders}

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将元数据配置文件应用到文件夹，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中应用。本节将介绍如何通过这两种方式将元数据配置文件应用到文件夹。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理已具有现有视频用户档案的文件夹中的资产，您稍后会更改该文件夹。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

#### Apply metadata profiles to folders from Profiles user interface {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

请按照以下步骤应用元数据用户档案:

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 选择您要应用到一个或多个文件夹的元数据配置文件。

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 从“属性”将元数据用户档案应用到文件夹 {#applying-metadata-profiles-to-folders-from-properties}

1. In the left rail, tap **[!UICONTROL Assets]** then navigate to the folder that you want to apply a metadata profile to.
1. 在文件夹中，点按或单击复选标记以将其选中，然后点按或单击属 **[!UICONTROL 性]**。

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and tap **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

### 全局应用元数据用户档案 {#applying-a-metadata-profile-globally}

除了将用户档案应用到文件夹之外，您还可以全局应用用户档案，以便上传到AEM资产的任何内容都会应用选定的。

您可以重新处理文件夹中的资产，该文件夹中已经有一个现有的元数据用户档案，您稍后会更改该元数据。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

**要全局应用元数据用户档案，请执行下列操作之一**

* 导航到并 `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 应用相应的用户档案，然后点按 **[!UICONTROL 保存]**。

   ![chlimage_1-209](assets/chlimage_1-492.png)

* 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`. 添加属性， `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` 然后点按 **全部保存**。

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Remove a metadata profile from folders {#removing-a-metadata-profile-from-folders}

当您将元数据配置文件从文件夹删除之后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。但是，此前对文件夹中的文件所做的处理均予以保留。

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中的文件夹删除元数据配置文件，或者如果您在文件夹中，也可以直接从&#x200B;**[!UICONTROL 属性]**&#x200B;中删除。本节将介绍如何通过这两种方式将元数据配置文件从文件夹中删除。

### Remove metadata profiles from folders via Profiles user interface {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 点按或单击AEM徽标，然后导航到工 **[!UICONTROL 具>资产>元数据用户档案]**。
1. 选择您要从一个或多个文件夹删除的元数据配置文件。
1. 点按&#x200B;**[!UICONTROL 从文件夹删除元数据配置文件]**，然后选择一个或多个要从中删除配置文件的文件夹，然后点按&#x200B;**[!UICONTROL 完成]**。

   您可以确认元数据用户档案不再应用于文件夹，因为该名称不再显示在文件夹名称的下方。

### 通过“属性”将元数据用户档案从文件夹删除 {#removing-metadata-profiles-from-folders-via-properties}

1. 点按AEM徽标并导 **[!UICONTROL 航资产]** ，然后导航到要从中删除元数据用户档案的文件夹。
1. 在文件夹中，点按复选标记以将其选中，然后点按属 **[!UICONTROL 性]**。
1. 选择&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;选项卡，并从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

>[!MORELIKETHIS]
>
>* [用户档案处理元数据、图像和视频](processing-profiles.md)
>* [组织数字资产以使用处理用户档案的最佳实践](/help/assets/organize-assets.md)

