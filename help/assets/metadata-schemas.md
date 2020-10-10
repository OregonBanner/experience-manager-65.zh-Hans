---
title: '元数据模式，用于定义中元数据属性页面的布局 [!DNL Adobe Experience Manager Assets]。 '
description: 元数据模式定义属性页面的布局以及为资产显示的元数据属性。 了解如何创建自定义元数据模式、编辑元数据模式，以及如何将元数据模式应用于资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '3601'
ht-degree: 11%

---


# 元数据架构 {#metadata-schemas}

组织会提出一个元数据模型，它增强了资产发现、使用、互操作性等。 正确的元数据应用程序对于维护元数据驱动的工作流和流程至关重要。 要遵守整个组织的元数据战略和标准，您可以使用元数据模式来帮助DAM用户进行调整。 [!DNL Adobe Experience Manager] 允许轻松、灵活地创建、维护和应用元数据模式。

在 [!DNL Adobe Experience Manager Assets]中，模式包含要填写的特定信息的特定字段。 它还包含布局信息，以用户友好的方式显示元数据字段。 元数据属性包括标题、描述、MIME类型、标记等。 您可以使用元数 [!UICONTROL 据模式Forms] ，修改现有模式或添加自定义元数据模式。

要视图和编辑资产的属性页面，请执行以下步骤：

1. 在卡片 **[!UICONTROL 视图中]** ，单击资产拼贴上快速操作中的“视图属性”选项。 或者，选择资产，然后单击工 **[!UICONTROL 具栏]**![中的](assets/do-not-localize/info-circle-icon.png) 视图属性。

1. 您可以编辑可用选项卡下的各种可编辑元数据属性。 但是，您无法在属性页 [!UICONTROL 面的] “基本 [!UICONTROL ”选项] 卡中修改资产类型。

   ![资产属性的“基本”选项卡，其中无法更改资产类型](assets/asset-properties-basic-tab.png)

*图：资产属性上的“基[!UICONTROL 本”选项卡]。*

要修改资产的MIME类型，请使用自定义元数据模式表单或修改现有表单。 请参 [阅编辑元数据模式](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) Forms，以了解更多信息。 如果您修改MIME类型的元数据模式，则会修改资产和所有子类型的属性页面布局。 例如，修改jpeg模式时，只 `default/image` 会修改MIME类型资产的元数据布局（资产属性） `image/jpeg`。 但是，如果您编辑默认模式，则所做的更改将修改所有类型资产的元数据布局。

## Metadata Schema forms {#default-metadata-schema-forms}

要视图表单或模板的列表，请在界面 [!DNL Experience Manager] 中导航到 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >元数 **[!UICONTROL 据模式]**。

[!DNL Experience Manager] 提供以下元数据模式表单模板。

| 模板 |  | 描述 |
|---|---|---|
| [!UICONTROL 默认] |  | 资产的基本元数据模式表单。 |
|  | The following child forms inherit the properties of the [!UICONTROL default] form: |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media视频的模式表单。 |
|  | <ul><li>[!UICONTROL 图像]</li></ul> | 模式表单，用于MIME类型(如 `image/jpeg` 和 `image/png`)。 <br> 图 [!UICONTROL 像表单] 具有以下子表单模板： <ul><li> [!UICONTROL jpeg]:模式子类型为jpeg的资产 [!UICONTROL 表单]。</li> <li>[!UICONTROL tiff]:子类型为TIFF的资产的模式表单。</li></ul> |
|  | <ul><li>[!UICONTROL 应用]</li></ul> | 模式表单，用于MIME类型如 `application/pdf` 和 `application/zip`。 <br>[!UICONTROL pdf]:模式子类型为PDF的资产的表单。 |
|  | <ul><li>[!UICONTROL 视频]</li></ul> | 模式表单，用于MIME类型(如 `video/avi` 和 `video/mp4`)。 |
| [!UICONTROL 收藏集] |  | 集合的模式表单。 |
| [!UICONTROL contentfragment] |  | [模式内容片段表单](/help/sites-developing/customizing-content-fragments.md)。 |
| [!UICONTROL 表单] |  | This schema form relates to [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] |  | 模式表单，用于用户生成的内容片段和资产从社交媒体集成到Experience Manager中。 |

>[!NOTE]
>
>要查看架构表单的子表单，请单击架构表单名称。

## Add a metadata schema form {#add-a-metadata-schema-form}

要添加元数据模式表单，请执行以下步骤：

1. 要向列表添加自定义模板，请单击工 **[!UICONTROL 具栏]** 中的创建。

   >[!NOTE]
   >
   >随未编辑的模板一起显示锁符号。 如果自定义模板，则不会锁定锁 ![定关闭](assets/do-not-localize/lock_closed_icon.svg)。

1. 在对话框中，提供模式表单的标题，然后单 **[!UICONTROL 击创建]** ，以完成表单创建过程。

## 编辑元数据模式表单 {#edit-metadata-schema-forms}

您可以编辑新添加的或现有的元数据模式表单。 元数据模式表单包括选项卡和选项卡中的表单项。 您可以将这些表单项映射到／配置到CRX存储库中元数据节点内的字段。 可向元数据模式表单添加选项卡或表单项。 从父级派生的选项卡和表单项目处于锁定状态。 无法从子级别更改它们。

1. 在元数 [!UICONTROL 据模式] “Forms”页面上 **[!UICONTROL ，选择一个表单，然后单击工]** 具栏中的“编辑”。

1. 在元数据 **[!UICONTROL 模式表单编辑器页]** ，自定义元数据表单。 将所需的组件从“构 **[!UICONTROL 建表单]** ”选项卡拖到其中一个选项卡。

   ![用于自定义资产属性页面的元数据模式编辑器](assets/metadata-schema-editor.png)

   *图：元数[!UICONTROL 据模式表单编辑器]（包含可用选项卡）页面。*

1. To configure a component, select it and modify its properties in the **[!UICONTROL Settings]** tab.

### Components within the [!UICONTROL Build Form] tab {#components-within-the-build-form-tab}

The **[!UICONTROL Build Form]** tab lists form items that you use in your schema form. The **[!UICONTROL Settings]** tab provides the attributes of each item that you select in the **[!UICONTROL Build Form]** tab. The following table lists the form items available in the **[!UICONTROL Build Form]** tab:

| 组件名称 | 描述 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 章节标题] | 添加一列表常用组件的章节标题。 |
| [!UICONTROL 单行文本] | 添加单行文本属性。它存储为字符串。 |
| [!UICONTROL 多值文本] | 添加多值文本属性。它存储为字符串数组。 |
| [!UICONTROL 数字] | 添加数字组件。 |
| [!UICONTROL 日期] | 添加日期组件。 |
| [!UICONTROL 下拉列表] | 添加下拉列表。 |
| [!UICONTROL 标准标记] | 添加标记. |
| [!UICONTROL 智能标记] | 通过自动添加元数据标记来增强搜索功能。 |
| [!UICONTROL 隐藏字段] | 添加隐藏字段。在保存资产时，它将作为POST参数发送。 |
| [!UICONTROL 资产引用对象] | 将此组件添加到资产引用的资产的视图列表。 |
| [!UICONTROL 资产引用] | 添加以显示引用资产的资产列表。 |
| [!UICONTROL 产品引用] | 添加以显示与资产链接的产品的列表。 |
| [!UICONTROL 资产评级] | 添加以显示资产评级选项。 |
| [!UICONTROL 上下文元数据] | 添加以控制资产属性页面中其他元数据选项卡的显示。 |

#### 编辑元数据组件 {#edit-the-metadata-component}

要编辑表单上元数据组件的属性，请单击该组件以编辑设置选项卡中的以下全部或一部分 **[!UICONTROL 属性]** 。

**字段标签**:资产的属性页面上显示的元数据属性的名称。

**映射到属性**:此属性指定资产节点在CRX存储库中保存的相对路径或名称。 它会开始 `./` 指示该路径位于资产的节点下。

以下是此属性的有效值：

* `./jcr:content/metadata/dc:title`：将该值作为属性 `dc:title` 存储在资产的元数据节点中。

* `./jcr:created`:存储资产的创建日期和时间。 它是受保护的属性。 如果配置这些属性，Adobe建议您将其标记为禁用编辑。

要确保在元数据模式表单中正确显示组件，属性路径不应包含任何空格。

* **占位符**:使用此属性可指定与元数据属性相关的占位符文本。
* **必需**:使用此属性可在属性页面上将元数据属性标记为必需。
* **禁用编辑**:使用此属性可禁止对属性页面上的属性进行任何编辑。
* **在只读模式下显示空字段**:标记此属性可在属性页面上显示元数据属性，即使其没有值也是如此。默认情况下，当元数据属性没有值时，不会在属性页面中列出该属性。
* **显示订购列表**:使用此属性可显示选项的有序列表。
* **选择**:使用此属性指定列表中的选项。
* **描述**：使用此属性可添加对元数据组件的简短描述。
* **类**:属性关联的对象类。
* **删除**:单击 [!UICONTROL 删除] ，以从模式表单中删除组件。

>[!NOTE]
>
>隐 [!UICONTROL 藏字段] 组件不包含这些属性。 而是包括属性，如名称、值、字段标签和说明。 无论何时保存资产，都会将“隐藏字段”组件的值作为 POST 参数进行发送。该组件的值不会作为资产的元数据进行保存。

如果选择&#x200B;**[!UICONTROL 必需]**&#x200B;选项，则可以搜索缺少必需元数据的资产。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，展开&#x200B;**[!UICONTROL 元数据验证]**&#x200B;谓词，然后选择&#x200B;**[!UICONTROL 无效]**&#x200B;选项。搜索结果中显示的资产缺少您通过架构表单配置的必需元数据。

![在“过滤器”面板的“元数据验证”谓词中选择的选项](assets/invalid-metadata-predicate.png)

如果您将上下文元数据组件添加到任何模式表单的任何选项卡，该组件将作为列表显示在应用特定模式的资产的属性页面中。 该列表包括除您应用了上下文元数据组件的选项卡外的所有其他选项卡。 目前，此功能提供基本功能，用于根据上下文控制元数据的显示。

![资产属性的上下文元数据组件列表选项卡](assets/metadata-contextual-component-list.png)

要在属性页面中显示除应用上下文元数据组件的选项卡之外的任何选项卡，请从列表中选择该选项卡。 该选项卡会添加到属性页面。

![上下文元数据列表上选择的选项卡会显示在资产属性页面上](assets/contextual-metadata-asset-properties.png)

*图：资产属性页面中的上下文元数据。*

### 在JSON文件中指定属性 {#specify-properties-in-json-file}

您还可以通过指定相应的键值对在 JSON 文件中定义选项，而不是为&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中的选项指定属性。在 **[!UICONTROL JSON 路径]**&#x200B;字段中指定 JSON 文件的路径。

#### 在模式表单中添加或删除选项卡 {#adding-deleting-a-tab-in-the-schema-form}

通过架构编辑器，可以添加或删除选项卡。The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![元数据模式表单中的默认选项卡](assets/metadata-schema-form-tabs.png)

Click `+` to add a tab on a schema form. By default, the new tab has the name `Unnamed-1`. You can modify the name from the **[!UICONTROL Settings]** tab. Click `X` to delete a tab.

![使用元数据模式编辑器添加或删除选项卡](assets/metadata-schema-form-new-tab.png)

## 串联元数据 {#cascading-metadata}

在捕获资产的元数据信息时，用户会在各种可用字段中提供信息。 您可以显示特定元数据字段或字段值，这些字段或字段值取决于在其他字段中选择的选项。 此类元数据的条件显示称为级联元数据。 换言之，您可以在特定元数据字段／值与一个或多个字段和／或其值之间创建依赖关系。

使用元数据模式定义用于显示级联元数据的规则。 例如，如果您的元数据模式包含资产类型字段，则您可以根据用户选择的资产类型定义要显示的相关字段集。

>[!CAUTION]
>
>内容片段不支持层叠元数据。

以下是一些可定义级联元数据的使用案例：

* 如果需要用户位置，则根据用户对国家／地区和州的选择显示相关城市名称。
* 根据用户对产品列表的选择，在类别中加载相关品牌名称。
* 根据在另一个字段中指定的值切换特定字段的可见性。 例如，如果用户希望将发运交付到其他地址，则显示单独的发运地址字段。
* 根据在另一个字段中指定的值将字段指定为必填字段。
* 根据在另一个字段中指定的值更改特定字段显示的选项。
* 根据在其他字段中指定的值，在特定字段中设置默认元数据值。

### 在 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

请考虑您希望根据所选资产类型显示级联元数据的方案。 一些示例

* 对于视频，显示适用的字段，如格式、编解码器、持续时间等。
* 对于Word或PDF文档，显示页面计数、作者等字段。

无论选择何种资产类型，均将版权信息显示为必填字段。

1. 在界 [!DNL Experience Manager] 面中，转至 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >元数 **[!UICONTROL 据模式]**。
1. In the **[!UICONTROL Schema Forms]** page, select a schema form and then click **[!UICONTROL Edit]** from the toolbar to edit the schema.

   ![select_form](assets/select_form.png)

1. （可选）在元数据模式编辑器中，创建新字段以进行条件化。 在“设置”选项卡中指定名称和属 **[!UICONTROL 性路径]** 。

   要创建新选项卡，请单 `+` 击以添加选项卡，然后添加元数据字段。

   ![add_tab](assets/add_tab.png)

1. 为资产类型添加下拉列表字段。 在“设置”选项卡中指定名称和属 **[!UICONTROL 性路径]** 。 添加可选描述。

   ![asset_type_field](assets/asset_type_field.png)

1. 键值对是提供给表单用户的选项。 您可以手动或从JSON文件提供键值对。

   * 要手动指定值，请选择“手 **[!UICONTROL 动添加]**”，然后单 **[!UICONTROL 击“添加选项]** ”，然后指定选项文本和值。 例如，指定视频、PDF、Word和图像资产类型。

   * 要动态从JSON文件中提取值，请选 **[!UICONTROL 择“通过JSON路径添加]** ”并提供JSON文件的路径。 [!DNL Experience Manager] 向用户显示表单时，实时获取键值对。

   这两种选择是互斥的。 无法从JSON文件导入选项并手动编辑。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >添加JSON文件时，键值对不会显示在元数据模式编辑器中，但在已发布的表单中可用。

   >[!NOTE]
   >
   >添加选项时，如果单击“下拉框”字段，则界面会扭曲，选项的删除选项将停止工作。 保存更改前，不要单击下拉菜单。 如果您遇到此问题，请保存模式并再次打开它以继续编辑。

1. （可选）添加其他必填字段。 例如，资产类型视频的格式、编解码器和持续时间。

   同样，为其他资产类型添加从属字段。 例如，为文档资产（如PDF和Word文件）添加字段页数和作者。

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. 要在资产类型字段和其他字段之间创建依赖关系，请选择相关字段并打开“规 **[!UICONTROL 则]** ”选项卡。

   ![select_dependentfield](assets/select_dependentfield.png)

1. Under **[!UICONTROL Requirement]**, choose the **[!UICONTROL Required, based on new rule]** option.
1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 Click **[!UICONTROL Done]** to save the changes.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >具有手动预定义值的下拉列表可与规则一起使用。 已配置JSON路径的下拉菜单不能与使用预定义值应用条件的规则一起使用。 如果这些值在运行时从JSON加载，则无法应用预定义的规则。

1. 在“可 **[!UICONTROL 见性]**”下，根据新 **[!UICONTROL 规则选项选择“可见]** ”。

1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. 还可以选择创建依赖关系时所依据的字段值。 在这种情况下，请选择“ **[!UICONTROL 视频]**”。 Click **[!UICONTROL Done]** to save the changes.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >单击空格（或除值之外的任何位置）将重置这些值。 如果发生这种情况，请重新选择值。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

1. 同样，在“资产类型”字段中的值“视频”与其他字段（如编解码器和持续时间）之间创建依赖关系。
1. 重复这些步骤，在“资产类型”字段中的文档资产(PDF和Word [!UICONTROL )与“页面计数] ”和“作者”等字段之 [!UICONTROL 间创建] 依 [!UICONTROL 赖关系]。
1. 单击&#x200B;**[!UICONTROL 保存]**。将元数据模式应用到文件夹。

1. 导航到您应用元数据模式的文件夹，然后打开资产的属性页面。 根据您在资产类型字段中的选择，系统会显示相关的层叠元数据字段。

   ![视频资产的层叠元数据](assets/video_asset.png)

   *图：为视频级联元数据。*

   ![文档资产的级联元数据](assets/doc_type_fields.png)

   *图：为文档级联元数据。*

## 删除元数据模式表单 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 允许您仅删除自定义模式表单。 您无法删除默认的架构表单/模板。但是，您可以删除对这些表单所做的任何自定义更改。

要删除表单，请选择一个表单，然后单击“删除”。

>[!NOTE]
>
>* 删除对默认表单的自定义更改后，关闭的锁 ![定功能](assets/do-not-localize/lock_closed_icon.svg) 将重新出现在表单前面。 它表示表单已恢复为默认状态。
>* 无法删除中的默认元数据模式表 [!DNL Assets]单。


## Schema forms for MIME types {#schema-forms-for-mime-types}

[!DNL Experience Manager] 为各种开箱即用的MIME类型提供默认表单。 但是，您可以为各种MIME类型的资产添加自定义表单。

### Add new forms for MIME types {#add-new-forms-for-mime-types}

在相应的表单类型下创建表单。 For example, to add a template for the `image/png` subtype, create the form under the &quot;image&quot; forms. 架构表单的标题是子类型名称。In this case, the title is `png`.

#### Use an existing schema template for various MIME types {#use-an-existing-schema-template-for-various-mime-types}

您可以为不同的 MIME 类型使用现有模板。For example, use the `image/jpeg` form for assets of MIME type `image/png`.

In this case, create a node at `/etc/dam/metadataeditor/mimetypemappings` in the CRX repository. 指定节点的名称并定义以下属性：

| 名称 | 描述 | 类型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的现有表单的名称 | `String` | `image/jpeg` |
| `mimetypes` | List of MIME types that use the form defined in the `exposedmimetype` attribute | `String` | `image/png` |

[!DNL Assets] 映射以下MIME类型和模式表单：

| 架构表单 | MIME类型 |
| --------------------------- | --------------------------------------------------- |
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

## Grant access to metadata schemas {#grant-access-to-metadata-schemas}

元数据架构功能仅适用于管理员。但是，管理员可以通过修改某些权限向非管理员用户提供访问权限。 为非管理员用户提供对文件夹的创建、修改和删除 `/conf` 权限。

## 应用特定于文件夹的元数据 {#apply-folder-specific-metadata}

[!DNL Assets] 允许您定义元数据模式的变体，并将其应用到特定文件夹。

例如，您可以定义默认元数据模式的变体并将其应用到文件夹。 应用修改后的模式时，该模式将覆盖应用于文件夹内资产的原始默认元数据区域。

只有上传到应用此模式的文件夹的资产才符合变体元数据模式中定义的修改后的元数据。 [!DNL Assets] 在其他应用原始模式的文件夹中，继续与原始模式中定义的元数据保持一致。

资产的元数据继承基于应用于层次结构中第一级文件夹的模式。 换言之，如果文件夹不包含子文件夹，则文件夹内的资产会继承应用于该文件夹的模式的元数据。

您可以在子文件夹中应用其他模式。 子文件夹中的资产将继承直接子文件夹的元数据模式。 如果子文件夹级别未应用模式或同一模式，则其资产会从父文件夹继承模式。

1. 在界 [!DNL Experience Manager] 面中，导航到 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >元数据 **[!UICONTROL 模式]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 选中表单前面的复选框（例如默认元数据表单），然后单击“复 **[!UICONTROL 制]** ”并将其另存为自定义表单。 指定表单的自定义名称，例如 `my_default`。 或者，您也可以创建自定义表单。

1. 在元数 **[!UICONTROL 据模式]** “Forms”页 `my_default` 面中，选择表单，然后单 **[!UICONTROL 击编辑]**。

1. 在元数 **[!UICONTROL 据模式编辑]** 器页面中，向模式表单添加一个文本字段。 例如，添加一个带有标签类别 **[!UICONTROL 的字段]**。

   ![文本字段已添加到元数据模式表单编辑器](assets/text-field-metadata-schema-editor.png)

   *图：文本字段已添加到元数据模式表单编辑器。*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在元数据 **[!UICONTROL 模式Forms]** 页面。
1. 单 **[!UICONTROL 击工具栏中的应用到文件夹]** ，以将自定义元数据应用到文件夹。

1. 选择要应用已修改模式的文件夹，然后单击“应 **[!UICONTROL 用”]**。

   ![选择要应用元数据模式的文件夹](assets/metadata-schema-select-folder.png)

1. 如果该文件夹应用了其他元数据模式，则会显示一条消息，警告您将覆盖现有元数据模式。 单击“ **覆盖**”。
1. Click **OK** to close the success message.
1. 导览至应用已修改元数据模式的文件夹。

## 定义必填元数据 {#define-mandatory-metadata}

您可以在文件夹级别定义必填字段，这将强制执行于上传到该文件夹的资产。 如果您上传的资产上传之前定义的必填字段缺少元数据，则卡视图的资产上会显示缺少元数据的可视指示。

>[!NOTE]
>
>可以根据其他字段的值将元数据字段定义为强制字段。 在卡视图中，不 [!DNL Experience Manager] 显示此类强制元数据字段缺少元数据的警告消息。

1. 在界 [!DNL Experience Manager] 面中，导航到 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** >元数据 **[!UICONTROL 模式]**。 此时会显示&#x200B;**[!UICONTROL 元数据架构表单]**&#x200B;页面。
1. 将默认元数据表单另存为自定义表单。 例如，将其另存为 `my_default`。

1. 编辑自定义表单。 添加必填字段。 例如，添加一个 **[!UICONTROL 类别]** 字段，并将该字段设为必填。

   ![在元数据模式表单编辑器的规则选项卡中选择必需，将必填字段添加到元数据表单](assets/mandatory-field-metadata-schema-editor.png)

   *图：元数据模式表单编辑器中的必填字段。*

1. 单击&#x200B;**[!UICONTROL 保存]**。修改后的表单列在元数据 **[!UICONTROL 模式Forms]** 页面。 选择表单，然后单 **[!UICONTROL 击工具栏中的应用到文]** 件夹，以将自定义元数据应用到文件夹。

1. 导航到文件夹，然后上传某些资产，其中缺少您添加到自定义表单的必填字段的元数据。 资产的卡视图上会显示必填字段中缺少的元数据的消息。

   ![在文件夹中上传资产时，资产卡视图中缺少必需元数据的消息](assets/metadata-missing-info-card-view.png)

1. （可选）访 `https://[aem_server]:[port]/system/console/components/`问。 配置并启 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 用默认禁用的组件。 设置检查资产上 [!DNL Experience Manager] 元数据的有效性的频率。 此配置向资产 `hasValidMetadata` 添加 `jcr:content` 属性。 [!DNL Experience Manager] 使用此属性筛选搜索结果中的无效资产。 如果您在选中后添加资产，则直到下一个计划的选 `hasValidMetadata` 中后，资产才会被标记。 因此，资产不会显示在搜索过滤器中，搜索无效元数据，直到下次计划检查后才显示。

   >[!CAUTION]
   >
   >元数据验证检查会占用大量资源，并且可能会影响系统性能。 计划相应的检查。 如果服务器无法处理负载，请尝试禁用此作业。

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
