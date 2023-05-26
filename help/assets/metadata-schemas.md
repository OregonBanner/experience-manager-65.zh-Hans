---
title: 元数据架构定义元数据属性页面的布局
description: 元数据架构定义属性页面的布局以及为资源显示的元数据属性。 了解如何创建自定义元数据架构、编辑元数据架构以及如何将元数据架构应用于资源。
contentOwner: AG
mini-toc-levels: 1
role: User,Admin
feature: Metadata
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 8%

---

# 元数据架构 {#metadata-schemas}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=en) |
| AEM 6.5 | 本文 |

组织可以构建一个元数据模型，用于增强资产发现、使用、互操作性等。 正确的元数据应用程序对于维护元数据驱动的工作流程和流程至关重要。 要遵循组织范围的元数据策略和标准，您可以使用帮助DAM用户对齐的元数据架构。 [!DNL Adobe Experience Manager] 允许使用简单灵活的方法创建、维护和应用元数据架构。

In [!DNL Adobe Experience Manager Assets]，架构包含要填写的特定信息的特定字段。 它还包含布局信息，以便以用户友好的方式显示元数据字段。 元数据属性包括标题、描述、MIME类型、标记等。 您可以使用 [!UICONTROL 元数据架构Forms] 编辑器以修改现有架构或添加自定义元数据架构。

要查看和编辑资产的属性页面，请执行以下步骤：

1. 单击 **[!UICONTROL 查看属性]** 卡片视图中资源拼贴上的快速操作选项。 或者，选择一个资产，然后单击 **[!UICONTROL 属性]** ![查看属性](assets/do-not-localize/info-circle-icon.png) 工具栏中。

1. 您可以在可用选项卡下编辑各种可编辑的元数据属性。 但是，您无法修改资源 [!UICONTROL 类型] 在 [!UICONTROL 基本] 属性页的选项卡。

   ![资源属性的“基本”选项卡，无法更改资源类型](assets/asset-properties-basic-tab.png)

   *图：资产的“基本”选项卡 [!UICONTROL 属性].*

   在创建或编辑元数据架构时，请确保只有一个属性映射到字段。

   要修改资源的MIME类型，请使用自定义元数据架构表单或修改现有表单。 参见 [编辑元数据架构Forms](#edit-metadata-schema-forms) 了解更多信息。 如果修改MIME类型的元数据架构，则会修改资源和所有子类型的属性页面布局。 例如，修改 `default/image` 仅修改具有MIME类型的资产的元数据布局（资产属性） `image/jpeg`. 但是，如果您编辑默认架构，则所做的更改会修改所有资源类型的元数据布局。

## 元数据架构表单 {#default-metadata-schema-forms}

要查看表单或模板列表，请 [!DNL Experience Manager] 界面导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.

[!DNL Experience Manager] 提供了以下元数据架构表单模板。

| 模板 |  | 描述 |
|---|---|---|
| [!UICONTROL 默认] |  | 资源的基本元数据架构表单。 |
|  | 以下子表单继承以下子表单的属性： [!UICONTROL 默认] 表单： |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media视频的架构表单。 |
|  | <ul><li>[!UICONTROL 图像]</li></ul> | 具有MIME类型的图像的架构表单，例如 `image/jpeg` 和 `image/png`. <br> 此 [!UICONTROL 图像] 表单包含以下子表单模板： <ul><li> [!UICONTROL jpeg]：具有子类型的资产的架构表单 [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]：具有子类型TIFF的资源的架构表单。</li></ul> |
|  | <ul><li>[!UICONTROL 应用程序]</li></ul> | 具有MIME类型的资产的架构表单，例如 `application/pdf` 和 `application/zip`. <br>[!UICONTROL pdf]：具有子类型PDF的资产架构表单。 |
|  | <ul><li>[!UICONTROL 视频]</li></ul> | 具有MIME类型的视频资产的架构表单，例如 `video/avi` 和 `video/mp4`. |
| [!UICONTROL 收藏集] |  | 收藏集的架构表单。 |
| [!UICONTROL contentfragment] |  | [内容片段的架构表单](/help/sites-developing/customizing-content-fragments.md). |
| [!UICONTROL 表单] |  | 此架构表单与 [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] |  | 用户生成的内容片段和资产从社交媒体集成到Experience Manager中的架构表单。 |

>[!NOTE]
>
>要查看架构表单的子表单，请单击架构表单名称。

## 添加元数据架构表单 {#add-a-metadata-schema-form}

要添加元数据架构表单，请执行以下步骤：

1. 要将自定义模板添加到列表，请单击 **[!UICONTROL 创建]** 工具栏中。

   >[!NOTE]
   >
   >锁定符号随未编辑的模板一起显示。 如果自定义模板，则该模板不会锁定 ![锁定已关闭](assets/do-not-localize/lock_closed_icon.svg).

1. 在对话框中，提供架构表单的标题并单击 **[!UICONTROL 创建]** 以完成表单创建过程。

## 编辑元数据架构表单 {#edit-metadata-schema-forms}

您可以编辑新添加或现有的元数据架构表单。 元数据架构表单包含选项卡和选项卡中的表单项。 您可以将这些表单项映射/配置到CRX存储库中元数据节点内的字段。 您可以将选项卡或表单项添加到元数据架构表单。 从父项派生的选项卡和表单项目处于锁定状态。 不能在子级别更改它们。

1. 在 [!UICONTROL 元数据架构Forms] 页面，选择表单并单击 **[!UICONTROL 编辑]** 工具栏中。

1. 在 **[!UICONTROL 元数据架构表单编辑器]** 页面，自定义元数据表单。 将所需的组件从 **[!UICONTROL 构建表单]** 选项卡移至其中一个选项卡。

1. 要配置组件，请选择该组件并在 **[!UICONTROL 设置]** 选项卡。

### 中的组件 [!UICONTROL 构建表单] 选项卡 {#components-within-the-build-form-tab}

此 **[!UICONTROL 构建表单]** 选项卡列出了您在架构表单中使用的表单项目。 此 **[!UICONTROL 设置]** 选项卡提供您在选项中选择的每个项目的属性。 **[!UICONTROL 构建表单]** 选项卡。 下表列出了中可用的表单项目 **[!UICONTROL 构建表单]** 选项卡：

| 组件名称 | 描述 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 章节标题] | 为常用组件列表添加章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。 它以字符串形式存储。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。 它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 智能标记] | 添加以通过自动添加元数据标记来增强搜索功能。 |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。 保存资源时，此参数将作为POST参数发送。 |
| [!UICONTROL 资产引用对象] | 添加此组件可查看资产引用的资产列表。 |
| [!UICONTROL 资产引用] | 添加以显示引用了资源的资源列表。 |
| [!UICONTROL 产品引用] | 添加以显示与资产链接的产品列表。 |
| [!UICONTROL 资产评级] | 添加以显示用于对资产进行分级的选项。 |
| [!UICONTROL 上下文元数据] | 添加以控制其他元数据选项卡在资源属性页面中的显示。 |

#### 编辑元数据组件 {#edit-the-metadata-component}

要编辑表单上元数据组件的属性，请单击该组件以编辑表单中以下属性的全部或子集 **[!UICONTROL 设置]** 选项卡。 建议仅将一个字段映射到元数据架构中的给定属性。 否则，系统会选取映射到资产的最新添加字段。

**字段标签**：在资产的属性页面上显示的元数据属性的名称。

**映射到属性**：此属性指定将资源保存在CRX存储库中的资源节点的相对路径或名称。 它始于 `./` 指示路径位于资产的节点下。

以下是属性的有效值示例：

* `./jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* `./jcr:created`：存储资源的创建日期和时间。 它是受保护的资产。 如果配置这些属性，Adobe建议将它们标记为“禁用编辑”。 否则，在保存资产的属性时，会出现“资产修改失败”错误。

为确保组件在元数据架构表单中正确显示，属性路径不应包含任何空格。

* **占位符**：使用此属性指定与元数据属性相关的占位符文本。
* **必需**：使用此属性可将元数据属性在属性页面上标记为必需。
* **禁用编辑**：使用此属性可禁止对属性页面上的属性进行任何编辑。
* **以只读方式显示空字段**：标记此属性以在属性页面上显示元数据属性，即使它没有值也是如此。 默认情况下，当元数据属性没有值时，它不会列在属性页面上。
* **显示排序的列表**：此属性用于显示经过排序的选择列表。
* **选项**：使用此属性指定列表中的选项。
* **描述** ：使用此属性可添加对元数据组件的简短描述。
* **类**：与属性关联的对象类。
* **删除**：单击 [!UICONTROL 删除] 从架构表单中删除组件。

>[!NOTE]
>
>此 [!UICONTROL 隐藏字段] 组件不包括这些属性。 而是包含属性，如属性“名称”、“值”、“字段标签”和“描述”。 每当保存资源时，隐藏字段组件的值都会作为POST参数发送。 它不会另存为资源的元数据。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

![在“筛选器的元数据验证谓词”面板中选择的选项](assets/invalid-metadata-predicate.png)

如果将“上下文元数据”组件添加到任何架构表单的任意选项卡，则该组件将以列表形式显示在应用了特定架构的资产属性页中。 该列表包含所有其他选项卡，但将上下文元数据组件应用于的选项卡除外。 目前，此功能提供基本功能，以根据上下文控制元数据的显示。

![上下文元数据组件列出了资源属性的选项卡](assets/metadata-contextual-component-list.png)

除了显示应用上下文元数据组件的选项卡外，要在属性页面中显示任何选项卡，请从列表中选择选项卡。 选项卡即会添加到属性页面中。

![在上下文元数据列表上选择的选项卡将显示在资源属性页面上](assets/contextual-metadata-asset-properties.png)

*图：资源属性页面中的上下文元数据。*

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 在架构表单中添加或删除选项卡 {#adding-deleting-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。默认架构表单包括 **[!UICONTROL 基本]**， **[!UICONTROL 高级]** ， **[!UICONTROL IPTC]**、和 **[!UICONTROL IPTC扩展]** 选项卡。

单击 `+` 在架构表单中添加选项卡。 默认情况下，新选项卡的名称为 `Unnamed-1`. 您可以从以下位置修改名称： **[!UICONTROL 设置]** 选项卡。 单击 `X` 以删除选项卡。

![使用元数据架构编辑器添加或删除选项卡](assets/metadata-schema-form-new-tab.png)

## 层叠元数据 {#cascading-metadata}

在捕获资源的元数据信息时，用户在各种可用字段中提供信息。 您可以显示依赖于在其他字段中选择的选项的特定元数据字段或字段值。 此类有条件地显示元数据称为层叠元数据。 换言之，您可以在特定元数据字段/值与一个或多个字段和/或其值之间创建依赖关系。

使用元数据架构定义用于显示层叠元数据的规则。 例如，如果您的元数据架构包含资源类型字段，您可以根据用户选择的资源类型定义要显示的相关字段集。

>[!CAUTION]
>
>内容片段不支持层叠元数据。

以下是您可以定义层叠元数据的一些用例：

* 在需要用户位置的地方，根据用户选择的国家和州显示相关城市名称。
* 根据用户选择的产品类别，在列表中加载相关品牌名称。
* 根据在另一个字段中指定的值切换特定字段的可见性。 例如，如果用户希望装运在不同地址交付，则显示单独的装运地址字段。
* 根据在另一个字段中指定的值，将一个字段指定为必填字段。
* 根据在另一个字段中指定的值更改为特定字段显示的选项。
* 根据在另一个字段中指定的值在特定字段中设置默认元数据值。

### 在中配置层叠元数据 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

考虑您要根据所选资源类型显示层叠元数据的方案。 一些示例

* 对于视频，显示适用的字段，例如格式、编解码器、持续时间等。
* 对于Word或PDF文档，显示字段，如页数、作者等。

无论选择的资产类型如何，都会将版权信息显示为必填字段。

1. In [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 在 **[!UICONTROL 架构Forms]** 页面上，选择架构表单，然后单击 **[!UICONTROL 编辑]** 以编辑架构。

   ![select_form](assets/select_form.png)

1. （可选）在元数据架构编辑器中，创建一个新字段以进行条件化。 在中指定名称和属性路径 **[!UICONTROL 设置]** 选项卡。

   要创建新选项卡，请单击 `+` 以添加选项卡，然后添加元数据字段。

   ![add_tab](assets/add_tab.png)

1. 为资源类型添加下拉字段。 在中指定名称和属性路径 **[!UICONTROL 设置]** 选项卡。 添加可选描述。

   ![asset_type_field](assets/asset_type_field.png)

1. 键值对是提供给表单用户的选项。 您可以手动或从JSON文件提供键值对。

   * 要手动指定值，请选择 **[!UICONTROL 手动添加]**，然后单击 **[!UICONTROL 添加选项]** 和指定选项文本和值。 例如，指定视频、PDF、Word和图像资源类型。

   * 要动态获取JSON文件中的值，请选择 **[!UICONTROL 通过JSON路径添加]** 和提供JSON文件的路径。 [!DNL Experience Manager] 向用户显示表单时实时获取键值对。

   这两个选项是互斥的。 您无法从JSON文件导入选项并手动编辑。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >添加JSON文件时，键值对不会显示在元数据架构编辑器中，但可在发布的表单中使用。

   >[!NOTE]
   >
   >添加选项时，如果单击“下拉”字段，则界面将扭曲，且选项的删除选项将停止工作。 在保存更改之前，请勿单击下拉菜单。 如果您遇到此问题，请保存架构并再次打开它以继续编辑。

1. （可选）添加其他必填字段。 例如，资源类型视频的格式、编解码器和持续时间。

   同样，为其他资源类型添加依赖字段。 例如，为文档资源(如PDF和Word文件)添加字段“页数”和“创作”。

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 要在资产类型字段和其他字段之间创建依赖关系，请选择依赖字段并打开 **[!UICONTROL 规则]** 选项卡。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 下 **[!UICONTROL 要求]**，选择 **[!UICONTROL 必需，基于新规则]** 选项。
1. 单击 **[!UICONTROL 添加规则]** 并选择 **[!UICONTROL 资源类型]** 用于创建依赖项的字段。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >带有手动预定义值的下拉列表可与规则一起使用。 包含配置的JSON路径的下拉菜单不能与使用预定义值来应用条件的规则一起使用。 如果在运行时从JSON加载值，则无法应用预定义规则。

1. 在“可 **[!UICONTROL 见性]**”下，根据新 **[!UICONTROL 规则选项选择“可见]** ”。

1. 单击 **[!UICONTROL 添加规则]** 并选择 **[!UICONTROL 资源类型]** 用于创建依赖项的字段。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >单击空格（或值以外的任何位置）会重置值。 如果发生这种情况，请重新选择值。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

1. 同样，在资产类型字段中的值Video与其他字段（如编解码器和持续时间）之间创建依赖关系。
1. 重复这些步骤以在中的文档资源(PDF和Word)之间创建依赖关系 [!UICONTROL 资源类型] 字段和字段，例如 [!UICONTROL 页数] 和 [!UICONTROL 作者].
1. 单击“**[!UICONTROL 保存]**”。将元数据架构应用于文件夹。

1. 导航到将元数据架构应用于的文件夹，然后打开资源的属性页面。 根据您在“资产类型”字段中的选择，将显示相关的级联元数据字段。

   ![视频资源的级联元数据](assets/video_asset.png)

   *图：视频的层叠元数据。*

   ![文档资产的级联元数据](assets/doc_type_fields.png)

   *图：文档的层叠元数据。*

## 删除元数据架构表单 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 仅允许您删除自定义架构表单。 不允许删除默认架构表单/模板。 但是，您可以删除这些表单中的任何自定义更改。

要删除表单，请选择一个表单，然后单击删除。

>[!NOTE]
>
>* 删除对默认表单的自定义更改后，锁定 ![锁定已关闭](assets/do-not-localize/lock_closed_icon.svg) 会在表单前重新显示。 它指示表单将恢复到其默认状态。
>* 您无法删除中的默认元数据架构表单 [!DNL Assets].


## MIME类型的架构表单 {#schema-forms-for-mime-types}

[!DNL Experience Manager] 为各种现成的MIME类型提供默认表单。 但是，您可以为各种MIME类型的资产添加自定义表单。

### 为MIME类型添加新表单 {#add-new-forms-for-mime-types}

在相应的表单类型下创建表单。 例如，为添加模板 `image/png` 子类型，在“图像”表单下创建表单。 架构表单的标题是子类型名称。在本例中，标题为 `png`.

#### 为各种MIME类型使用现有架构模板 {#use-an-existing-schema-template-for-various-mime-types}

您可以为其他MIME类型使用现有模板。 例如，使用 `image/jpeg` MIME类型资产的表单 `image/png`.

在这种情况下，请在以下位置创建一个节点： `/etc/dam/metadataeditor/mimetypemappings` 在CRX存储库中。 指定节点名称并定义以下属性：

| 名称 | 描述 | 类型 | 价值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的现有表单的名称 | `String` | `image/jpeg` |
| `mimetypes` | 使用中定义的表单的MIME类型列表 `exposedmimetype` 属性 | `String` | `image/png` |

[!DNL Assets] 映射以下MIME类型和架构表单：

| 架构表单 | MIME类型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi， video/msvideo， video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 授予对元数据架构的访问权限 {#grant-access-to-metadata-schemas}

元数据架构功能仅对管理员可用。 但是，管理员可以通过修改某些权限为非管理员提供访问权限。 为非管理员用户提供创建、修改和删除权限 `/conf` 文件夹。

## 应用文件夹特定的元数据 {#apply-folder-specific-metadata}

[!DNL Assets] 允许您定义元数据架构的变体并将其应用于特定文件夹。

例如，您可以定义默认元数据架构的变体并将其应用到文件夹。 应用修改后的架构时，它会覆盖应用于文件夹中资源的原始默认元数据架构。

只有上传到应用此架构的文件夹的资产符合变体元数据架构中定义的修改后的元数据。 [!DNL Assets] 在应用了原始架构的其他文件夹中，将继续符合在原始架构中定义的元数据。

按资产列出的元数据继承基于应用于层次结构中顶级文件夹的架构。 子文件夹应用或继承的架构相同。 如果在子文件夹级别应用了其他架构，继承将停止。

1. In [!DNL Experience Manager] 界面，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**. 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框，例如默认元数据表单，然后单击 **[!UICONTROL 复制]** 并将其另存为自定义表单。 指定表单的自定义名称，例如 `my_default`. 或者，您也可以创建自定义表单。

1. 在 **[!UICONTROL 元数据架构Forms]** 页面上，选择 `my_default` 表单，然后单击 **[!UICONTROL 编辑]**.

1. 在 **[!UICONTROL 元数据架构编辑器]** 页面，向架构表单中添加文本字段。 例如，添加带有标签的字段 **[!UICONTROL 类别]**.

   ![添加到元数据架构表单编辑器的文本字段](assets/text-field-metadata-schema-editor.png)

   *图：添加到元数据架构表单编辑器的文本字段。*

1. 单击“**[!UICONTROL 保存]**”。修改后的表单将列在 **[!UICONTROL 元数据架构Forms]** 页面。
1. 单击 **[!UICONTROL 应用到文件夹]** 以将自定义元数据应用到文件夹。

1. 选择要应用修改后架构的文件夹，然后单击 **[!UICONTROL 应用]**.

   ![选择要应用元数据架构的文件夹](assets/metadata-schema-select-folder.png)

1. 如果文件夹应用了其他元数据架构，则会显示一条消息，警告您即将覆盖现有元数据架构。 单击 **覆盖**.
1. 单击 **确定** 以关闭成功消息。
1. 导航到将修改后的元数据架构应用于的文件夹。

## 定义必需的元数据 {#define-mandatory-metadata}

您可以在文件夹级别定义必填字段，这会在上传到文件夹的资产上强制实施。 如果您上传的资产，缺少之前定义的必填字段的元数据，卡片视图中的资产上将显示缺少元数据的视觉指示。

>[!NOTE]
>
>可根据其他字段的值将元数据字段定义为必填字段。 在卡片视图中， [!DNL Experience Manager] 不显示有关此类必填元数据字段缺少元数据的警告消息。

1. In [!DNL Experience Manager] 界面，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**. 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为 `my_default`.

1. 编辑自定义表单。 添加必填字段。 例如，添加 **[!UICONTROL 类别]** 字段并将字段设为必填。

   ![通过在元数据架构表单编辑器的“规则”选项卡中选择“必需”，将必填字段添加到元数据表单](assets/mandatory-field-metadata-schema-editor.png)

   *图：元数据架构表单编辑器中的必填字段。*

1. 单击“**[!UICONTROL 保存]**”。修改后的表单将列在 **[!UICONTROL 元数据架构Forms]** 页面。 选择表单，然后单击 **[!UICONTROL 应用到文件夹]** 以将自定义元数据应用到文件夹。

1. 导航到文件夹并上传一些缺少元数据的资产，这些资产属于您添加到自定义表单中的必填字段。 在资源的卡片视图上，将显示一条消息，指出缺少必填字段的元数据。

   ![上传文件夹中的资产时，资产卡视图中缺少必需元数据的消息](assets/metadata-missing-info-card-view.png)

1. （可选）访问 `https://[aem_server]:[port]/system/console/components/`. 配置和启用 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 默认禁用的组件。 设置频率 [!DNL Experience Manager] 检查资源上的元数据的有效性。 此配置添加了一个属性 `hasValidMetadata` 到 `jcr:content` 个资源。 [!DNL Experience Manager] 使用此属性筛选搜索结果中的无效资源。 如果在检查后添加资产，则该资产不会使用 `hasValidMetadata` 直到下一次计划检查。 因此，直到下一次计划检查之后，资产才会出现在无效元数据的搜索过滤器中。

   >[!CAUTION]
   >
   >元数据验证检查占用大量资源，可能会影响系统性能。 相应地安排检查。 如果服务器无法应对负载，请尝试禁用此作业。

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
