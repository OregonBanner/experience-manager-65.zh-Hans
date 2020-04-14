---
title: 创建自适应表单
seo-title: 创建自适应表单
description: 如何使用AEM Forms创建自适应表单。 自适应表单是响应式HTML5表单，可简化信息收集和处理。
seo-description: 如何使用AEM Forms创建自适应表单。 自适应表单是响应式HTML5表单，可简化信息收集和处理。
uuid: 444f461a-9e88-4385-b5ee-e985067ab7bc
content-type: reference
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f06b8cb2-6f98-465f-beec-1e91e3f45707
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# 创建自适应表单 {#creating-an-adaptive-form}

## <strong>创建自适应表单</strong>{#strong-create-an-adaptive-form-strong}

按照以下步骤创建自适应表单。

1. 访问AEM Forms作者实例，网址为 `https://'[server]:[port]'/<custom-context-if-any>.`

1. 在AEM登录页面上输入凭据。

   登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager >表单>表单和文档]**。

   >[!NOTE]
   >
   >对于默认安装，登录名 `admin` 为，口令为 `admin`。

1. 点按 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 自适应表单]**。
1. 此时会显示一个用于选择模板的选项。 有关模板的详细信息，请参阅自 [适应表单模板](/help/forms/using/creating-adaptive-form.md#p-adaptive-form-templates-p)。 点按模板以将其选中，然后点按下一步。
1. 出现“添加属性”选项。 指定以下属性字段的值。 “标题”和“名称”字段是必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。 标题可帮助您在AEM Forms用户界面中识别表单。
   * **[!UICONTROL 名称：]** 指定表单的名称。 将在存储库中创建具有指定名称的节点。 在开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都替换为连字符。
   * **[!UICONTROL 说明：]** 指定有关表单的详细信息。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在“标记”框中键入新的标 **记名** 。

1. 您可以基于以下任一表单模型创建自适应表单：

   * [表单数据模型](#fdm)
   * [XFA表单模板](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)
   * [XML或JSON模式](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-xml-or-json-schema-p)
   * 无或没有任何表单模型
   您可以从添加属性页面的 **[!UICONTROL 表单模型]** 选项卡中 **[!UICONTROL 配置这些模型]** 。 默认情况下，选定的表单模型为“ **[!UICONTROL 无”]**。

1. 点按&#x200B;**创建**。将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

   指定完所有属性后，单击“创 **[!UICONTROL 建”]**。 将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

   指定完所有属性后，单击“创 **[!UICONTROL 建”]**。 将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

1. 点按 **[!UICONTROL 打开]** ，在新选项卡中打开新创建的表单。 此时将打开表单进行编辑，并显示模板中的可用内容。 它还显示侧栏，以根据需要自定义新创建的表单。

   根据自适应表单的类型，关联的XFA表单模板、XML模式或JSON模式中存在的表单元素将显示在提要栏中内容浏览器的 **[!UICONTROL Data Model]** Objects **** （数据模型对象）选项卡中。 您还可以拖放这些元素以构建自适应表单。

   有关自适应表单创作界面和可用组件的信息，请参 [阅创作自适应表单简介](/help/forms/using/introduction-forms-authoring.md)。

   >[!NOTE] {grayBox=&quot;true&quot;}
   >
   >允许浏览器中的弹出窗口在新选项卡中打开新创建的表单。

## 基于表单数据模型创建自适应表单 {#fdm}

[AEM Forms数据集成](/help/forms/using/data-integration.md) ，允许您集成多个数据源并将其实体和服务整合在一起，以创建表单数据模型。 它是JSON模式的扩展。 您可以使用表单数据模型创建自适应表单。 在表单数据模型中配置的实体或数据模型对象可用作表单创作的数据模型对象。 它们绑定到各个数据源，用于预填表单并将提交的数据写回各个数据源。 您还可以使用自适应表单规则调用在表单数据模型中配置的服务。

要使用表单数据模型创建自适应表单，请执行以下操作：

1. 在“添加属性”屏幕的“表单模型”选项卡中， **[!UICONTROL 在“从中选择”下拉]** 列表中选择“表 **[!UICONTROL 单数据模型]** ”。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点按以展开“选 **[!UICONTROL 择表单数据模型”]**。 列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您还可以更改自适应表单的表单数据模型。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 基于XFA表单模板创建自适应表单 {#create-an-adaptive-form-based-on-an-xfa-form-template}

您可以重用XFA表单模板来创建自适应表单。 要重用XFA表单模板，请上传并将其与自适应表单关联。 自适应表单创作时，表单模板（XFA表单）的元素可用于内容查找器中。 从内容查找器中，可以将表单模板元素拖放到表单上。

>[!NOTE]
>
>[在开始创建基于表单模板的自适应表单之前](/help/forms/using/get-xdp-pdf-documents-aem.md) ，请先将XFA表单模板上传到AEM表单。

执行以下操作以将XFA表单模板用作自适应表单的表单模型：

1. 在“添 **[!UICONTROL 加属性]** ”页面上，打开“表 **[!UICONTROL 单模型]** ”选项卡。
1. 在表单模型选项卡的下拉列表中，选择表单模 **[!UICONTROL 板]**。 将列出通过AEM Forms UI上传到存储库的所有表单模板以供选择。 从列表中选择模板。

   ![将XFA表单模板与自适应表单关联](assets/form_model_xfa_associate.png)
   **图：** 选 *择表单模板*

   >[!NOTE]
   >
   >您还可以更改自适应表单的表单模板。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 基于XML或JSON模式创建自适应表单 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON模式表示组织中后端系统生成或使用数据的结构。 您可以将模式与自适应表单关联，并使用其元素将动态内容添加到自适应表单。 模式的元素位于内容浏览器的“数据模型对象”选项卡中，用于创作自适应表单。 您可以拖放模式元素以构建表单。

请参阅以下文档，了解如何为创作自适应表单设计XML或JSON模式。

* [使用XML模式创建自适应表单](/help/forms/using/adaptive-form-xml-schema-form-model.md)
* [使用JSON模式创建自适应表单](/help/forms/using/adaptive-form-json-schema-form-model.md)

执行以下操作以将XML或JSON模式用作自适应表单的表单模型：

1. 在自适应 **[!UICONTROL 表单创建页面的]** “添加属性”步骤中，点按表单模 **[!UICONTROL 型选项卡]** 。
1. 在“表单模型”选项卡中， **[!UICONTROL 从“从]** ”下 **[!UICONTROL 拉字段中选]** 择“模式”。

1. 点按 **[!UICONTROL 选择模式]** ，然后执行下列操作之一：

   * **[!UICONTROL 从磁盘上传]** -选择此选项，然后点按上传模式定义，以从文件系统浏览和上传XML模式或JSON模式。 上传的模式文件驻留在表单中，其他自适应表单无法访问。
   * **[!UICONTROL 在存储库中搜索]** -选择此选项可从存储库中可用的模式定义文件列表中进行选择。 选择XML或JSON模式文件作为表单模型。 所选模式将按引用与表单关联，并可供在其他自适应表单中使用。
   >[!CAUTION] {grayBox=&quot;true&quot;}
   >
   >确保JSON模式文件名以 **.模式.json结尾**。 例如：mySchema.模式.json

   ![选择XML或JSON模式](assets/upload-schema.png)
   **图：** 选 *择XML或JSON模式*

1. (仅限XML模式)在选择或上传XML模式后，指定选定XSD文件的根元素以与自适应表单一起映射。

   ![选择XSD根元素](assets/xsd-root-element.png)
   **图：** 选 *择XSD根元素*

>[!NOTE]
>
>您还可以更改自适应表单的模式。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 自适应表单模板 {#adaptive-form-templates}

模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有预格式化的组件，这些组件包含某些属性和内容结构。 AEM Forms现成提供了一些自适应表单模板。 要获取包含高级模板的完整模板包，您需要安装AEM Forms加载项包。 有关详细信息，请 [参阅安装AEM Forms加载项包](/help/forms/using/installing-configuring-aem-forms-osgi.md)。

此外，您还可以使用模板编辑器创建自己的模板。 有关使用模板的更多信息，请参阅自适 [应表单模板](/help/forms/using/template-editor.md)。

>[!NOTE]
>
>当您打开使用高级模板创建的自适应表单进行编辑时，将显示一条错误消息。 高级模板具有签名步骤组件，默认情况下为其启用Adobe Sign。 创建并选择 [Adobe Sign云配置](/help/forms/using/adobe-sign-integration-adaptive-forms.md) , [并配置签署方](working-with-adobe-sign.md#addsignerstoanadaptiveform) ，以解决错误。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

自适应表单是在没有表单模型（使用表单模型的“无”选项）或使用表单模型(如表单模板、XML模式或JSON模式或表单数据模型)的情况下创建的。 可以将自适应表单的表单模型从“无”更改为其他表单模型。 对于基于表单模型的自适应表单，可以为同一表单模型选择其他表单模板、XML模式、JSON模式或表单数据模型。 但是，不能将一个表单模型更改为另一个表单模型。

1. 选择自适应表单并点按属 **性图** 标。
1. 打开“表 **[!UICONTROL 单模型]** ”选项卡，然后执行以下操作之一。

   * 如果自适应表单没有表单模型，您可以选择其他表单模型，并相应地选择表单模板、XML或JSON模式或表单数据模型。
   * 如果自适应表单基于表单模型，则可以为同一表单模型选择其他表单模板、XML或JSON模式或表单数据模型。

1. 点按 **[!UICONTROL 保存]** ，以保存属性。

## 自动保存自适应表单 {#auto-save-an-adaptive-form}

默认情况下，自适应表单的内容会保存在用户操作上，如按保存按钮时。 您还可以配置自适应表单以根据开始或时间间隔自动保存内容。 “自动保存”选项在以下位置很有帮助：

* 自动保存匿名用户和登录用户的内容
* 无需或最少的用户干预即可保存表单的内容
* 开始保存基于用户事件的表单内容
* 在指定的时间间隔后重复保存表单的内容

### 为自适应表单启用自动保存 {#enable-auto-save-for-an-adaptive-form}

默认情况下，自动保存选项未启用。 您可以从自适应表单的“自动保存”选项卡中启用自动保存选项。 “自动保存”选项卡还提供了若干其他配置选项。 执行以下步骤以为自适应表单启用和配置自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后点按字 ![段级别](assets/field-level.png) >自适应表 **[!UICONTROL 单容器]**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在“自 **[!UICONTROL 动保存]** ”部分， **[!UICONTROL 启用]** “自动保存”选项。
1. 在“自 **[!UICONTROL 适应表单事件]** ”框中，指定1或TRUE可在表单加载到浏览器时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，开始将保存表单的内容。
1. 指定触发器。 自动保存会根据您的配置触发。 您的选择包括：

   * **[!UICONTROL 基于时间：]** 选择选项以开始根据特定时间间隔保存内容。
   * **[!UICONTROL 事件:]** 选择开始选项，以在触发事件时保存内容。
   当您选择触发器时，“策略配置”框处于启用状态。 “战略配置”框允许您：

   * 如果选择基于时间的触发器，请指 **[!UICONTROL 定时间间隔]** 。
   * 如果选择基于事件的触发器，请指 **[!UICONTROL 定事件名]** 。
   您还可以创建自定义策略并将其添加到列表。 有关详细信息，请参 [阅实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在“在 **[!UICONTROL 此间隔上自动保存]** ”框中，以秒为单位指定时间间隔。 在经过间隔框中指定的秒数后，将重复保存表单。

1. (仅基于事件的自动保存)执行以下步骤以配置基于事件的自动保存选项。

   1. 在“在此 **事件后自动保存** ”框中，指定 [GuideBridge事件](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 。 每次表达式的计算结果为TRUE时，将保存表单。

1. （可选）要自动保存匿名用户的内容，请选择“为匿名用户启 **用自动保存”选项** ，然后单击“确 **[!UICONTROL 定”]**。

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保您配置Forms Common Configuration Service，以允许所有用户预览、验证和签署表单。
   >
   >要配置服务，请转到上的AEM Web Console配置，并编辑 `https://'[server]:[port]'system/console/configMgr`**[!UICONTROL Forms Common Configuration Service]** ，以在“允许”字段中选择“ **[!UICONTROL 所有用户]** ”选项 **** ，然后保存该配置。