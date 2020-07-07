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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 0%

---


# 创建自适应表单 {#creating-an-adaptive-form}

## <strong>创建自适应表单</strong> {#strong-create-an-adaptive-form-strong}

按照以下步骤创建自适应表单。

1. 访问AEM Forms作者实例： `https://'[server]:[port]'/<custom-context-if-any>.`

1. 在AEM登录页面上输入凭据。

   登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager>表单>表单和文档]**。

   >[!NOTE]
   >
   >对于默认安装，登录名 `admin` 为，口令为 `admin`。

1. 点按 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 自适应表单]**。
1. 此时会显示一个用于选择模板的选项。 有关模板的更多信息，请参 [阅自适应表单模板](/help/forms/using/creating-adaptive-form.md#p-adaptive-form-templates-p)。 点按模板以选择它，然后点按下一步。
1. 出现“添加属性”选项。 指定以下属性字段的值。 “标题”和“名称”字段为必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。 标题可帮助您在AEM Forms用户界面中识别表单。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 当您开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都替换为连字符。
   * **[!UICONTROL 描述：]** 指定有关表单的详细信息。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在“标记”框中键入新 **标记** 名称。

1. 您可以基于以下表单模型之一创建自适应表单：

   * [表单数据模型](#fdm)
   * [XFA表单模板](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)
   * [XML或JSON模式](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-xml-or-json-schema-p)
   * 无或没有任何表单模型

   您可以从添加属性页 **[!UICONTROL 面的表单模]** 型选项卡 **[!UICONTROL 中配置这些模]** 型。 默认情况下，所选的表单模型为“ **[!UICONTROL 无”]**。

1. 点按&#x200B;**创建**。将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

   指定完所有属性后，单击“创 **[!UICONTROL 建”]**。 将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

   指定完所有属性后，单击“创 **[!UICONTROL 建”]**。 将创建自适应表单，并显示一个用于打开表单进行编辑的对话框。

1. 点按 **[!UICONTROL 打开]** ，在新选项卡中打开新创建的表单。 此时将打开表单进行编辑，并显示模板中的可用内容。 它还显示侧栏，以根据需要自定义新创建的表单。

   根据自适应表单的类型，关联的XFA表单模板、XML模式或JSON模式中存在的表单元素将显示在提要 **[!UICONTROL 栏中内容浏览器的]** “数据 **[!UICONTROL 模型对象]** ”选项卡中。 您还可以拖放这些元素以构建自适应表单。

   有关自适应表单创作界面和可用组件的信息，请参 [阅自适应表单创作简介](/help/forms/using/introduction-forms-authoring.md)。

   >[!NOTE]
   >
   >允许浏览器中的弹出窗口在新选项卡中打开新创建的表单。

## 根据表单数据模型创建自适应表单 {#fdm}

[AEM Forms数据集](/help/forms/using/data-integration.md) 成允许您集成多个数据源，并将其实体和服务整合在一起，以创建表单数据模型。 它是JSON模式的扩展。 您可以使用表单数据模型创建自适应表单。 在表单数据模型中配置的实体或数据模型对象可用作表单创作的数据模型对象。 它们绑定到各个数据源，用于预填表单并将提交的数据写回各个数据源。 您还可以使用自适应表单规则调用在表单数据模型中配置的服务。

要使用表单数据模型创建自适应表单，请执行以下操作：

1. 在“添加属性”屏幕的“表单模型”选项卡 **[!UICONTROL 中，在“从选]** 择中 **[!UICONTROL ”下]** 拉列表中选择“表单数据模型”。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点按以展开 **[!UICONTROL 选择表单数据模型]**。 列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您还可以更改自适应表单的表单数据模型。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 根据XFA表单模板创建自适应表单 {#create-an-adaptive-form-based-on-an-xfa-form-template}

您可以重用XFA表单模板来创建自适应表单。 要重新设定用途，请上传XFA表单模板并将其与自适应表单关联。 自适应表单创作时，表单模板（XFA表单）的元素可在内容查找器中使用。 在内容查找器中，可以将表单模板元素拖放到表单上。

>[!NOTE]
>
>[在开始创建基于表单模板的自适应表单](/help/forms/using/get-xdp-pdf-documents-aem.md) 之前，请先将XFA表单模板上传到AEM Forms。

执行以下操作以将XFA表单模板用作自适应表单的表单模型：

1. 在“添 **[!UICONTROL 加属性]** ”页面上，打开 **[!UICONTROL “表单模型]** ”选项卡。
1. 在表单模型选项卡的下拉列表中，选择表单 **[!UICONTROL 模板]**。 将列出通过AEM FormsUI上传到存储库的所有表单模板供选择。 从列表中选择模板。

   ![将XFA表单模板与自适应表单关联](assets/form_model_xfa_associate.png)
   **图：** *选择表单模板*

   >[!NOTE]
   >
   >您还可以更改自适应表单的表单模板。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 根据XML或JSON模式创建自适应表单 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON模式表示组织中的后端系统生成或使用数据的结构。 您可以将模式与自适应表单关联，并使用其元素将动态内容添加到自适应表单。 模式的元素位于内容浏览器的“数据模型对象”选项卡中，用于创作自适应表单。 您可以拖放模式元素以构建表单。

请参阅以下文档，了解如何为创作自适应表单设计XML或JSON模式。

* [使用XML模式创建自适应表单](/help/forms/using/adaptive-form-xml-schema-form-model.md)
* [使用JSON模式创建自适应表单](/help/forms/using/adaptive-form-json-schema-form-model.md)

执行以下操作以将XML或JSON模式用作自适应表单的表单模型：

1. 在自适 **[!UICONTROL 应表单创建页]** 的添加属性步骤中，点按表单 **[!UICONTROL 模型选项卡]** 。
1. 在“表单模型”选项卡中， **[!UICONTROL 从]** “从 **[!UICONTROL 中选择]** ”下拉字段中选择模式。

1. 点按 **[!UICONTROL 选择模式]** ，然后执行下列操作之一：

   * **[!UICONTROL 从磁盘上传]** -选择此选项，然后点按上传模式定义，以从文件系统浏览和上传XML模式或JSON模式。 上传的模式文件驻留在表单中，其他自适应表单无法访问。
   * **[!UICONTROL 在存储库中搜索]** -选择此选项可从存储库中可用的模式定义文件列表中进行选择。 选择XML或JSON模式文件作为表单模型。 所选模式将按引用与表单关联，并可供其他自适应表单使用。

   >[!CAUTION]
   >
   >确保JSON模式文件名以。 **模式.json结尾**。 例如： mySchema.模式.json

   ![选择XML或JSON模式](assets/upload-schema.png)
   **图：** *选择XML或JSON模式*

1. (仅限XML模式)选择或上传XML模式后，请指定选定XSD文件的根元素，以与自适应表单进行映射。

   ![选择XSD根元素](assets/xsd-root-element.png)
   **图：** *选择XSD根元素*

>[!NOTE]
>
>您还可以更改自适应表单的模式。 有关详细步骤，请参 [阅编辑自适应表单的表单模型属性](#edit-form-model)。

## 自适应表单模板 {#adaptive-form-templates}

模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有预格式化的组件，这些组件包含某些属性和内容结构。 开箱即用，AEM Forms提供一些自适应表单模板。 要获得包含高级模板的完整模板包，您需要安装AEM Forms加载项包。 有关详细信息，请 [参阅安装AEM Forms加载项包](/help/forms/using/installing-configuring-aem-forms-osgi.md)。

此外，您可以使用模板编辑器创建您自己的模板。 有关使用模板的更多信息，请参阅自 [适应表单模板](/help/forms/using/template-editor.md)。

>[!NOTE]
>
>打开使用高级模板创建的自适应表单进行编辑时，将显示一条错误消息。 高级模板具有签名步骤组件，默认情况下为其启用Adobe Sign。 创建并选择 [Adobe Sign云配置](/help/forms/using/adobe-sign-integration-adaptive-forms.md) , [并配置签署方](working-with-adobe-sign.md#addsignerstoanadaptiveform) 以解决错误。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

自适应表单是在没有表单模型（使用表单模型的“无”选项）或使用表单模型(如表单模板、XML模式或JSON模式或表单数据模型)的情况下创建的。 可以将自适应表单的表单模型从“无”更改为其他表单模型。 对于基于表单模型的自适应表单，可以为同一表单模型选择其他表单模板、XML模式、JSON模式或表单数据模型。 但是，不能将一个表单模型更改为另一个表单模型。

1. 选择自适应表单并点按 **属性** 图标。
1. 打开“ **[!UICONTROL 表单模型]** ”选项卡并执行下列操作之一。

   * 如果自适应表单没有表单模型，您可以选择其他表单模型，并相应地选择表单模板、XML或JSON模式或表单数据模型。
   * 如果自适应表单基于表单模型，则可以为同一表单模型选择其他表单模板、XML或JSON模式或表单数据模型。

1. 点按 **[!UICONTROL 保存]** ，以保存属性。

## 自动保存自适应表单 {#auto-save-an-adaptive-form}

默认情况下，自适应表单的内容会保存在用户操作上，如按保存按钮时。 您还可以配置自适应表单以根据开始或时间间隔自动保存内容。 “自动保存”选项在以下位置很有用：

* 自动保存匿名和登录用户的内容
* 在无需或最少用户干预的情况下保存表单的内容
* 开始根据用户事件保存表单的内容
* 在指定的时间间隔后重复保存表单的内容

### 为自适应表单启用自动保存 {#enable-auto-save-for-an-adaptive-form}

默认情况下，自动保存选项未启用。 您可以从自适应表单的“自动保存”选项卡中启用自动保存选项。 “自动保存”选项卡还提供了其他几个配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后点 ![按字段级](assets/field-level.png) >自 **[!UICONTROL 适应表单容器]**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在“自 **[!UICONTROL 动保存]** ”部分 **[!UICONTROL ，启]** 用“自动保存”选项。
1. 在“自 **[!UICONTROL 适应表单事件]** ”框中，指定1或TRUE可在表单加载到浏览器时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，开始将保存表单的内容。
1. 指定触发器。 自动保存会根据您的配置触发。 您的选择包括：

   * **[!UICONTROL 基于时间：]** 选择选项以开始根据特定时间间隔保存内容。
   * **[!UICONTROL 事件:]** 选择开始选项，以在触发事件时保存内容。

   选择触发器时，“策略配置”框处于启用状态。 “策略配置”框允许您：

   * 如果选择基于时间的触发器，请 **[!UICONTROL 指定时间间隔]** 。
   * 如果选择基于事件的触发器，请 **[!UICONTROL 指定事件]** 名称。

   您还可以创建自定义策略并将其添加到列表。 有关详细信息，请 [参阅实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在“自动 **[!UICONTROL 保存此时间间隔]** ”框中，以秒为单位指定时间间隔。 在经过间隔框中指定的秒数后，将重复保存表单。

1. (仅基于事件的自动保存)执行以下步骤以配置基于事件的自动保存选项。

   1. 在“此 **事件后自动保存** ”框中，指 [定GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每次表达式计算结果为TRUE时，将保存表单。

1. （可选）要自动保存匿名用户的内容，请选择“为匿名 **用户启用自动保存** ”选项，然后单 **[!UICONTROL 击“确定”]**。

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保配置Forms Common Configuration Service以允许所有用户对表单进行预览、验证和签名。
   >
   >要配置服务，请转到AEM Web Console配置，并 `https://'[server]:[port]'system/console/configMgr` 编辑Forms **[!UICONTROL Common Configuration Service]** ，在“允 **[!UICONTROL 许”字段中选]** 择“所有用户 **[!UICONTROL ”选项]** ，然后保存配置。