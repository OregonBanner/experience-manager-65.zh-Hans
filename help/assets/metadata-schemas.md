---
title: '元数据架构定义元数据属性页的布局 '
description: 元数据架构定义属性页面的布局以及为资产显示的元数据属性。 了解如何创建自定义元数据架构、编辑元数据架构，以及如何将元数据架构应用到资产。
contentOwner: AG
role: Business Practitioner,Administrator
feature: 元数据
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
source-git-commit: eefd19768cc52350ba5858a439b793c125fd23cc
workflow-type: tm+mt
source-wordcount: '3547'
ht-degree: 15%

---

# 元数据架构 {#metadata-schemas}

组织会提出一种元数据模型，该模型可增强资产发现、使用情况、互操作性等。 正确的元数据应用程序对于维护元数据驱动的工作流和流程来说是神圣不可侵犯的。 为了遵循组织范围的元数据策略和标准，您可以使用元数据架构来帮助DAM用户进行协调。 [!DNL Adobe Experience Manager] 允许使用简单灵活的方法创建、维护和应用元数据架构。

在[!DNL Adobe Experience Manager Assets]中，架构包含要填写的特定信息的特定字段。 它还包含布局信息，以用户友好的方式显示元数据字段。 元数据属性包括标题、描述、MIME类型、标记等。 您可以使用[!UICONTROL 元数据架构Forms]编辑器来修改现有架构或添加自定义元数据架构。

要查看和编辑资产的属性页面，请执行以下步骤：

1. 单击卡片视图中资产拼贴快速操作中的&#x200B;**[!UICONTROL 查看属性]**&#x200B;选项。 或者，选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]** ![查看属性](assets/do-not-localize/info-circle-icon.png)。

1. 您可以在可用选项卡下编辑各种可编辑的元数据属性。 但是，您无法在属性页面的[!UICONTROL 基本]选项卡中修改资产[!UICONTROL 类型]。

   ![资产属性的“基本”选项卡，其中资产类型无法更改](assets/asset-properties-basic-tab.png)

   *图：“资产属性”中的“基 [!UICONTROL 本”选项卡]。*

   要修改资产的MIME类型，请使用自定义元数据架构表单或修改现有表单。 有关更多信息，请参阅[编辑元数据架构Forms](#edit-metadata-schema-forms)。 如果修改MIME类型的元数据架构，则会修改资产的属性页面布局和所有子类型。 例如，修改`default/image`下的jpeg架构仅会修改MIME类型为`image/jpeg`的资产的元数据布局（资产属性）。 但是，如果您编辑默认架构，则所做的更改将修改所有类型资产的元数据布局。

## 元数据架构表单 {#default-metadata-schema-forms}

要查看表单或模板列表，请在[!DNL Experience Manager]界面中导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**。

[!DNL Experience Manager] 提供了以下元数据架构表单模板。

| 模板 |  | 描述 |
|---|---|---|
| [!UICONTROL 默认] |  | 资产的基本元数据架构表单。 |
|  | 以下子表单继承[!UICONTROL default]表单的属性： |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media视频的架构表单。 |
|  | <ul><li>[!UICONTROL 图像]</li></ul> | MIME类型为`image/jpeg`和`image/png`的图像的架构表单。 <br> 图像  表单具有以下子表单模板： <ul><li> [!UICONTROL jpeg]:子类型为jpeg [!UICONTROL 的资产的架构]表单。</li> <li>[!UICONTROL tiff]:子类型为TIFF的资产的架构表单。</li></ul> |
|  | <ul><li>[!UICONTROL 应用程序]</li></ul> | MIME类型为`application/pdf`和`application/zip`的资产的架构表单。 <br>[!UICONTROL pdf]:子类型为PDF的资产的架构表单。 |
|  | <ul><li>[!UICONTROL 视频]</li></ul> | MIME类型为`video/avi`和`video/mp4`的视频资产的架构表单。 |
| [!UICONTROL 收藏集] |  | 集合的架构表单。 |
| [!UICONTROL contentfragment] |  | [内容片段的架构表单](/help/sites-developing/customizing-content-fragments.md)。 |
| [!UICONTROL 表单] |  | 此架构表单与[Adobe Experience Manager Forms](/help/forms/home.md)相关。 |
| [!UICONTROL ugc_contentfragment] |  | 用于用户生成的内容片段和资产从社交媒体集成到Experience Manager中的架构表单。 |

>[!NOTE]
>
>要查看架构表单的子表单，请单击架构表单名称。

## 添加元数据架构表单 {#add-a-metadata-schema-form}

要添加元数据架构表单，请执行以下步骤：

1. 要将自定义模板添加到列表，请单击工具栏中的&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >锁定符号随未编辑的模板一起显示。 如果自定义模板，则不会将其锁定在![锁定关闭的](assets/do-not-localize/lock_closed_icon.svg)。

1. 在对话框中，提供架构表单的标题，然后单击&#x200B;**[!UICONTROL 创建]**&#x200B;以完成表单创建过程。

## 编辑元数据架构表单 {#edit-metadata-schema-forms}

您可以编辑新添加的或现有的元数据架构表单。 元数据架构表单包括选项卡和选项卡中的表单项目。 您可以将这些表单项目映射/配置到CRX存储库元数据节点中的字段。 您可以向元数据架构表单中添加选项卡或表单项目。 从父级派生的选项卡和表单项目处于锁定状态。 无法从子级别更改它们。

1. 在[!UICONTROL 元数据架构Forms]页面上，选择一个表单，然后单击工具栏中的&#x200B;**[!UICONTROL 编辑]** 。

1. 在&#x200B;**[!UICONTROL 元数据架构表单编辑器]**&#x200B;页面上，自定义元数据表单。 将所需的组件从&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡拖到其中一个选项卡。

1. 要配置组件，请选择该组件并在&#x200B;**[!UICONTROL Settings]**&#x200B;选项卡中修改其属性。

### [!UICONTROL 构建表单]选项卡中的组件 {#components-within-the-build-form-tab}

**[!UICONTROL 构建表单]**&#x200B;选项卡列出了您在架构表单中使用的表单项目。 **[!UICONTROL 设置]**&#x200B;选项卡提供您在&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡中选择的每个项目的属性。 下表列出了&#x200B;**[!UICONTROL 构建表单]**&#x200B;选项卡中可用的表单项目：

| 组件名称 | 描述 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 章节标题] | 添加一系列常用组件的章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。它将作为字符串存储。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。它将作为字符串数组存储。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记。 |
| [!UICONTROL 智能标记] | 通过自动添加元数据标记来添加以增强搜索功能。 |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。在保存资产时，该字段将作为 POST 参数发送。 |
| [!UICONTROL 资产引用对象] | 添加此组件可查看该资产所引用的其他资产的列表。 |
| [!UICONTROL 资产引用] | 添加此组件可显示引用该资产的其他资产的列表。 |
| [!UICONTROL 产品引用] | 添加此组件可显示与该资产关联的产品的列表。 |
| [!UICONTROL 资产评级] | 添加以显示资产评级选项。 |
| [!UICONTROL 上下文元数据] | 添加可控制资产属性页面中其他元数据选项卡的显示。 |

#### 编辑元数据组件 {#edit-the-metadata-component}

要编辑表单上元数据组件的属性，请在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中单击该组件以编辑以下所有属性或属性的子集。

**字段标签**:资产的属性页面上显示的元数据属性的名称。

**映射到属性**:此属性指定保存在CRX存储库中的资产节点的相对路径或名称。以`./`开头，表示路径位于资产的节点下。

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* `./jcr:created`:存储资产的创建日期和时间。它是受保护的属性。 如果配置这些属性，Adobe建议您将其标记为“禁用编辑”。 否则，在保存资产的属性时，会出现“资产修改失败”错误。

要确保组件在元数据架构表单中正确显示，属性路径不应包含任何空格。

* **占位符**:使用此属性可指定与元数据属性相关的占位符文本。
* **必需**:使用此属性可在属性页面上将元数据属性标记为必需属性。
* **禁用编辑**:使用此属性可禁止对属性页面上的属性进行任何编辑。
* **在“只读”中显示空字段**:标记此属性可在属性页面上显示元数据属性，即使此属性没有值也是如此。默认情况下，当元数据属性没有值时，该属性不会列在属性页面上。
* **按顺序显示列表**:使用此属性可显示有序的选项列表。
* **选项**:使用此属性可在列表中指定选项。
* **描述**：使用此属性可添加对元数据组件的简短描述。
* **类**:属性与关联的对象类。
* **删除**:单击  删除可从架构表单中删除组件。

>[!NOTE]
>
>[!UICONTROL 隐藏字段]组件不包含这些属性。 相反，它包含属性，如属性名称、值、字段标签和描述。 无论何时保存资产，都会将“隐藏字段”组件的值作为 POST 参数进行发送。该组件的值不会作为资产的元数据进行保存。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

![在“过滤器”面板的“元数据验证谓词”中选择的选项](assets/invalid-metadata-predicate.png)

如果将上下文元数据组件添加到任何架构表单的任何选项卡，则该组件会在应用了特定架构的资产的属性页面中显示为列表。 该列表包含所有其他选项卡，但您应用上下文元数据组件的选项卡除外。 目前，此功能提供了基本功能，用于根据上下文控制元数据的显示。

![列出资产属性选项卡的上下文元数据组件](assets/metadata-contextual-component-list.png)

要在属性页面中显示除应用上下文元数据组件的选项卡之外的任何选项卡，请从列表中选择选项卡。 选项卡会添加到属性页面。

![在上下文元数据列表中选择的选项卡将显示在资产属性页面上](assets/contextual-metadata-asset-properties.png)

*图：资产属性页面中的上下文元数据。*

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 在架构表单中添加或删除选项卡 {#adding-deleting-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。默认架构表单包括&#x200B;**[!UICONTROL Basic]**、**[!UICONTROL Advanced]**、**[!UICONTROL IPTC]**&#x200B;和&#x200B;**[!UICONTROL IPTC扩展]**&#x200B;选项卡。

单击`+`在架构表单上添加选项卡。 默认情况下，新选项卡的名称为`Unnamed-1`。 您可以从&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中修改该名称。单击`X`以删除选项卡。

![使用元数据架构编辑器添加或删除选项卡](assets/metadata-schema-form-new-tab.png)

## 串联元数据 {#cascading-metadata}

在捕获资产的元数据信息时，用户会在各种可用字段中提供信息。 您可以显示特定的元数据字段或字段值，这些字段值取决于在其他字段中选择的选项。 此类元数据的条件显示称为级联元数据。 换言之，您可以在特定元数据字段/值与一个或多个字段和/或其值之间创建依赖项。

使用元数据架构定义用于显示级联元数据的规则。 例如，如果您的元数据架构包含资产类型字段，则可以根据用户选择的资产类型定义要显示的相关字段集。

>[!CAUTION]
>
>内容片段不支持级联元数据。

以下是可为其定义级联元数据的一些用例：

* 如果需要用户位置，则根据用户对国家/地区和州的选择显示相关的城市名称。
* 根据用户对产品类别的选择，在列表中加载相关的品牌名称。
* 根据其他字段中指定的值切换特定字段的可见性。 例如，如果用户希望以不同的地址交付发运，则显示单独的发运地址字段。
* 根据其他字段中指定的值，将字段指定为必填字段。
* 根据其他字段中指定的值更改特定字段显示的选项。
* 根据其他字段中指定的值，在特定字段中设置默认元数据值。

### 在[!DNL Experience Manager]中配置级联元数据 {#configure-cascading-metadata-in-aem}

假设您想要根据所选资产类型显示级联元数据。 一些示例

* 对于视频，显示适用的字段，如格式、编解码器、持续时间等。
* 对于Word或PDF文档，显示字段，如页面计数、作者等。

无论选择何种资产类型，都会将版权信息显示为必填字段。

1. 在[!DNL Experience Manager]界面中，转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
1. 在&#x200B;**[!UICONTROL 架构Forms]**&#x200B;页面中，选择架构表单，然后单击工具栏中的&#x200B;**[!UICONTROL 编辑]**&#x200B;以编辑架构。

   ![select_form](assets/select_form.png)

1. （可选）在元数据架构编辑器中，创建要条件化的新字段。 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中指定名称和属性路径。

   要创建新选项卡，请单击`+`以添加选项卡，然后添加元数据字段。

   ![add_tab](assets/add_tab.png)

1. 为资产类型添加下拉字段。 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中指定名称和属性路径。 添加可选描述。

   ![asset_type_field](assets/asset_type_field.png)

1. 键值对是提供给表单用户的选项。 您可以手动或从JSON文件提供键值对。

   * 要手动指定值，请选择&#x200B;**[!UICONTROL 手动添加]**，然后单击&#x200B;**[!UICONTROL 添加选择]**&#x200B;并指定选项文本和值。 例如，指定视频、PDF、Word和图像资产类型。

   * 要动态获取JSON文件中的值，请选择&#x200B;**[!UICONTROL 通过JSON路径添加]**&#x200B;并提供JSON文件的路径。 [!DNL Experience Manager] 向用户显示表单时，会实时获取键值对。

   两个选项是互斥的。 您无法从JSON文件导入选项并手动编辑。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >添加JSON文件时，键值对不会显示在元数据架构编辑器中，但可在已发布的表单中使用。

   >[!NOTE]
   >
   >添加选项时，如果单击下拉字段，则界面会扭曲，选项的删除选项会停止工作。 在保存更改之前，请勿单击下拉菜单。 如果遇到此问题，请保存架构并再次将其打开以继续编辑。

1. （可选）添加其他必填字段。 例如，资产类型视频的格式、编解码器和持续时间。

   同样，为其他资产类型添加从属字段。 例如，为文档资产（如PDF和Word文件）添加字段页面计数和作者。

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 要在资产类型字段和其他字段之间创建依赖关系，请选择相关字段，然后打开&#x200B;**[!UICONTROL Rules]**&#x200B;选项卡。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 在&#x200B;**[!UICONTROL Requirement]**&#x200B;下，根据新规则&#x200B;]**选项选择**[!UICONTROL  Required。
1. 单击&#x200B;**[!UICONTROL 添加规则]**，然后选择&#x200B;**[!UICONTROL 资产类型]**&#x200B;字段以创建依赖项。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >包含手动预定义值的下拉列表可与规则一起使用。 配置了JSON路径的下拉菜单不能与使用预定义值来应用条件的规则一起使用。 如果在运行时从JSON加载值，则无法应用预定义规则。

1. 在“可 **[!UICONTROL 见性]**”下，根据新 **[!UICONTROL 规则选项选择“可见]** ”。

1. 单击&#x200B;**[!UICONTROL 添加规则]**，然后选择&#x200B;**[!UICONTROL 资产类型]**&#x200B;字段以创建依赖项。 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >单击空格（或值以外的任何位置）会重置这些值。 如果发生这种情况，请重新选择值。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

1. 同样，在资产类型字段中的值视频与其他字段（如编解码器和持续时间）之间创建依赖关系。
1. 重复以下步骤，在[!UICONTROL 资产类型]字段和[!UICONTROL 页面计数]和[!UICONTROL 作者]等字段中，在文档资产（PDF和Word）之间创建依赖项。
1. 单击&#x200B;**[!UICONTROL 保存]**。将元数据架构应用到文件夹。

1. 导航到应用元数据架构的文件夹，然后打开资产的属性页面。 根据您在资产类型字段中的选择，将显示相关的级联元数据字段。

   ![视频资产的级联元数据](assets/video_asset.png)

   *图：级联视频的元数据。*

   ![文档资产的级联元数据](assets/doc_type_fields.png)

   *图：为文档级联元数据。*

## 删除元数据架构表单 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 允许您仅删除自定义架构表单。您无法删除默认的架构表单/模板。但是，您可以删除对这些表单所做的任何自定义更改。

要删除表单，请选择一个表单，然后单击删除。

>[!NOTE]
>
>* 删除对默认表单的自定义更改后，锁定![closed](assets/do-not-localize/lock_closed_icon.svg)将在表单前重新显示。 它表示表单已还原为其默认状态。
>* 无法删除[!DNL Assets]中的默认元数据架构表单。


## MIME类型的架构表单 {#schema-forms-for-mime-types}

[!DNL Experience Manager] 为各种开箱即用的MIME类型提供默认表单。但是，您可以为各种MIME类型的资产添加自定义表单。

### 为MIME类型添加新表单 {#add-new-forms-for-mime-types}

在相应的表单类型下创建表单。 例如，要为`image/png`子类型添加模板，请在“image”表单下创建表单。 架构表单的标题是子类型名称。在这种情况下，标题为`png`。

#### 对各种MIME类型使用现有架构模板 {#use-an-existing-schema-template-for-various-mime-types}

您可以为不同的 MIME 类型使用现有模板。例如，对于MIME类型为`image/png`的资产，请使用`image/jpeg`表单。

在这种情况下，请在CRX存储库的`/etc/dam/metadataeditor/mimetypemappings`处创建一个节点。 指定节点的名称并定义以下属性：

| 名称 | 描述 | 类型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的现有表单的名称 | `String` | `image/jpeg` |
| `mimetypes` | 使用`exposedmimetype`属性中定义的表单的MIME类型列表 | `String` | `image/png` |

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
| video/avi | video/avi、video/msvideo、video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 授予对元数据架构的访问权限 {#grant-access-to-metadata-schemas}

元数据架构功能仅适用于管理员。但是，管理员可以通过修改某些权限来向非管理员用户提供访问权限。 为非管理员用户提供对`/conf`文件夹的创建、修改和删除权限。

## 应用特定于文件夹的元数据 {#apply-folder-specific-metadata}

[!DNL Assets] 允许您定义元数据架构的变体，并将其应用到特定文件夹。

例如，您可以定义默认元数据架构的变体并将其应用到文件夹。 应用修改后的架构时，它会覆盖原始的默认元数据架构，该架构已应用于文件夹中的资产。

只有上传到应用此架构的文件夹的资产，才符合变体元数据架构中定义的修改后元数据。 [!DNL Assets] 在应用了原始架构的其他文件夹中，将继续符合在原始架构中定义的元数据。

资产的元数据继承基于应用于层次结构中顶级文件夹的架构。 子文件夹会应用相同的架构或继承该架构。 如果在子文件夹级别应用了其他架构，则继承将停止。

1. 在[!DNL Experience Manager]界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框（例如默认的元数据表单），然后单击&#x200B;**[!UICONTROL Copy]**&#x200B;并将其另存为自定义表单。 为表单指定自定义名称，例如`my_default`。 或者，您也可以创建自定义表单。

1. 在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页面中，选择`my_default`表单，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 在&#x200B;**[!UICONTROL 元数据架构编辑器]**&#x200B;页面中，向架构表单中添加文本字段。 例如，添加标签为&#x200B;**[!UICONTROL Category]**&#x200B;的字段。

   ![向元数据架构表单编辑器中添加了文本字段](assets/text-field-metadata-schema-editor.png)

   *图：向元数据架构表单编辑器中添加了文本字段。*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页面中。
1. 单击工具栏中的&#x200B;**[!UICONTROL 应用到文件夹]** ，将自定义元数据应用到文件夹。

1. 选择要应用已修改架构的文件夹，然后单击&#x200B;**[!UICONTROL Apply]**。

   ![选择要应用元数据架构的文件夹](assets/metadata-schema-select-folder.png)

1. 如果文件夹应用了其他元数据架构，则会显示一条消息，警告您将要覆盖现有的元数据架构。 单击&#x200B;**覆盖**。
1. 单击&#x200B;**确定**&#x200B;以关闭成功消息。
1. 导航到应用已修改元数据架构的文件夹。

## 定义必需元数据 {#define-mandatory-metadata}

您可以在文件夹级别定义必填字段，该字段对上传到该文件夹的资产强制执行。 如果您为之前定义的必填字段上传缺少元数据的资产，则卡片视图中的资产上会显示缺少元数据的可视指示。

>[!NOTE]
>
>根据其他字段的值，可以将元数据字段定义为必填字段。 在卡片视图中，[!DNL Experience Manager]不显示有关此类必需元数据字段缺少元数据的警告消息。

1. 在[!DNL Experience Manager]界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为`my_default`。

1. 编辑自定义表单。 添加必填字段。 例如，添加&#x200B;**[!UICONTROL Category]**&#x200B;字段，并将该字段设为必填字段。

   ![通过在元数据架构表单编辑器的规则选项卡中选择必需，将必填字段添加到元数据表单](assets/mandatory-field-metadata-schema-editor.png)

   *图：元数据架构表单编辑器中的必填字段。*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在&#x200B;**[!UICONTROL 元数据架构Forms]**&#x200B;页面中。 选择表单，然后单击工具栏中的&#x200B;**[!UICONTROL 应用到文件夹]** ，将自定义元数据应用到文件夹。

1. 导航到文件夹，并上传某些资产，其中缺少您添加到自定义表单的必填字段的元数据。 资产的卡片视图中会显示有关必填字段缺失元数据的消息。

   ![在文件夹中上传资产时，资产卡片视图中缺少必需元数据的消息](assets/metadata-missing-info-card-view.png)

1. （可选）访问`https://[aem_server]:[port]/system/console/components/`。 配置并启用默认禁用的`com.day.cq.dam.core.impl.MissingMetadataNotificationJob`组件。 设置一个频度，在该频率下[!DNL Experience Manager]会检查资产上元数据的有效性。 此配置会向资产的`jcr:content`中添加属性`hasValidMetadata`。 [!DNL Experience Manager] 使用此属性过滤搜索结果中的无效资产。如果您在选中后添加资产，则在进行下一次计划检查之前，不会为资产添加`hasValidMetadata`标记。 因此，直到下次计划检查后，资产才会显示在无效元数据的搜索筛选器中。

   >[!CAUTION]
   >
   >元数据验证检查占用大量资源，并且可能会影响系统性能。 相应地计划检查。 如果服务器无法处理负载，请尝试禁用此作业。

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
