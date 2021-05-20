---
title: 如何创建自适应表单
description: '了解如何使用 [!DNL Experience Manager Forms]创建自适应表单。 自适应表单是响应式HTML5表单，可简化信息收集和处理过程。 深入了解如何根据表单数据模型、XFA表单模板以及XML或JSON架构创建自适应表单。 '
feature: 自适应表单
role: Business Practitioner, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# 创建自适应表单{#creating-an-adaptive-form}

## <strong>创建自适应表单</strong> {#strong-create-an-adaptive-form-strong}

按照以下步骤创建自适应表单。

1. 访问位于`https://'[server]:[port]'/<custom-context-if-any>.`的[!DNL Experience Manager Forms]创作实例

1. 在Experience Manager登录页面上输入凭据。

   登录后，点按左上角的&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   >[!NOTE]
   >
   >对于默认安装，登录名为`admin`，密码为`admin`。

1. 点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 自适应表单]**。
1. 此时会显示用于选择模板的选项。 有关模板的更多信息，请参阅[自适应表单模板](creating-adaptive-form.md#p-adaptive-form-templates-p)。 点按模板以将其选中，然后点按下一步。
1. 此时会显示“添加属性”选项。 指定以下属性字段的值。 标题和名称字段是必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。标题可帮助您识别[!DNL Experience Manager Forms]用户界面中的表单。
   * **[!UICONTROL 名称：]** 指定表单的名称。在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。
   * **[!UICONTROL 描述：]** 指定有关表单的详细信息。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。标记有助于搜索表单。 要创建标记，请在&#x200B;**[!UICONTROL 标记]**&#x200B;框中键入新标记名称。

1. 您可以基于以下任一表单模型创建自适应表单：

   * [表单数据模型](#fdm)
   * [XFA表单模板](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML或JSON架构](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 无或没有任何表单模型

   您可以从&#x200B;**[!UICONTROL 添加属性]**&#x200B;页面的&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡中配置这些属性。 默认情况下，所选的表单模型为&#x200B;**[!UICONTROL 无]**。

1. 点按&#x200B;**[!UICONTROL 创建]**。随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。

   指定完所有属性后，单击&#x200B;**[!UICONTROL 创建]**。 随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。

   指定完所有属性后，单击&#x200B;**[!UICONTROL 创建]**。 随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。

1. 点按&#x200B;**[!UICONTROL 打开]** ，以在新选项卡中打开新创建的表单。 此时将打开表单进行编辑，并显示模板中可用的内容。 它还会显示侧栏，以根据需要自定义新创建的表单。

   根据自适应表单的类型，关联的XFA表单模板、XML模式或JSON模式中存在的表单元素显示在侧栏中&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中。 您还可以拖放这些元素以构建自适应表单。

   有关自适应表单创作界面和可用组件的信息，请参阅[自适应表单创作简介](introduction-forms-authoring.md)。

   >[!NOTE]
   >
   >允许浏览器中的弹出窗口在新选项卡中打开新创建的表单。

## 根据表单数据模型创建自适应表单 {#fdm}

[[!DNL Experience Manager Forms] 数据](data-integration.md) 集成允许您集成多个数据源，并将其实体和服务整合在一起，以创建表单数据模型。它是JSON模式的扩展。 您可以使用表单数据模型创建自适应表单。 在表单数据模型中配置的实体或数据模型对象可用作表单创作的数据模型对象。 它们绑定到相应的数据源，用于预填表单并将提交的数据写回相应的数据源。 您还可以使用自适应表单规则调用在表单数据模型中配置的服务。

要使用表单数据模型创建自适应表单，请执行以下操作：

1. 在“添加属性”屏幕的“表单模型”选项卡中，选择&#x200B;**[!UICONTROL 从]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 表单数据模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点按以展开&#x200B;**[!UICONTROL 选择表单数据模型]**。 将列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您还可以更改自适应表单的表单数据模型。 有关详细步骤，请参阅[编辑自适应表单的表单模型属性](#edit-form-model)。

## 根据XFA表单模板{#create-an-adaptive-form-based-on-an-xfa-form-template}创建自适应表单

您可以重新调整XFA表单模板的用途以创建自适应表单。 要重新调整用途，请上传XFA表单模板并将其与自适应表单相关联。 表单模板（XFA表单）的元素可在自适应表单创作时在内容查找器中使用。 从内容查找器中，可以将表单模板元素拖放到表单上。

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## 基于XML或JSON架构{#create-an-adaptive-form-based-on-xml-or-json-schema}创建自适应表单

XML和JSON架构表示组织内的后端系统生成或使用数据的结构。 您可以将架构与自适应表单相关联，并使用其元素向自适应表单添加动态内容。 架构的元素位于内容浏览器的“数据模型对象”选项卡中，用于创作自适应表单。 您可以拖放架构元素以构建表单。

请参阅以下文档，了解如何设计用于创作自适应表单的XML或JSON模式。

* [使用XML架构创建自适应表单](adaptive-form-xml-schema-form-model.md)
* [使用JSON模式创建自适应表单](adaptive-form-json-schema-form-model.md)

请执行以下操作以将XML或JSON模式用作自适应表单的表单模型：

1. 在自适应表单创建页面的&#x200B;**[!UICONTROL 添加属性]**&#x200B;步骤中，点按&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡。
1. 在表单模型选项卡的&#x200B;**[!UICONTROL 从]**&#x200B;下拉字段中选择&#x200B;**[!UICONTROL 架构]**。

1. 点按&#x200B;**[!UICONTROL 选择架构]**，然后执行下列操作之一：

   * **[!UICONTROL 从磁盘上传]**  — 选择此选项，然后点按上传架构定义，以从您的文件系统中浏览并上传XML架构或JSON架构。上传的架构文件驻留在表单中，其他自适应表单无法访问该文件。
   * **[!UICONTROL 在存储库中搜索]**  — 选择此选项可从存储库中可用的架构定义文件列表中进行选择。选择XML或JSON架构文件作为表单模型。 所选架构通过引用与表单关联，并可在其他自适应表单中使用。

   >[!CAUTION]
   >
   >请确保JSON架构文件名以&#x200B;**.schema.json**&#x200B;结尾。 例如：mySchema.schema.json

   ![选择XML或JSON架构](assets/upload-schema.png)
   **图：** *选择XML或JSON架构*

1. （仅限XML架构）选择或上载XML架构后，请指定要与自适应表单一起映射的选定XSD文件的根元素。

   ![选择XSD根元素](assets/xsd-root-element.png)
   **图：** *选择XSD根元素*

>[!NOTE]
>
>您还可以更改自适应表单的架构。 有关详细步骤，请参阅[编辑自适应表单的表单模型属性](#edit-form-model)。

## 自适应表单模板{#adaptive-form-templates}

模板提供了基本结构并定义了自适应表单的外观（布局和样式）。 它具有预格式化的组件，其中包含某些属性和内容结构。<!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

此外，您还可以使用模板编辑器创建自己的模板。 有关使用模板的更多信息，请参阅[自适应表单模板](template-editor.md)。

>[!NOTE]
>
>当您打开使用高级模板创建的用于编辑的自适应表单时，会显示一条错误消息。 高级模板具有签名步骤组件，默认情况下为其启用Adobe Sign。 创建并选择[Adobe Sign云配置](adobe-sign-integration-adaptive-forms.md)和[配置签名者](working-with-adobe-sign.md#addsignerstoanadaptiveform)以解决错误。

## 编辑自适应表单{#edit-form-model}的表单模型属性

创建自适应表单时没有使用表单模型（使用表单模型的无选项），也没有使用表单模型（如表单模板、XML架构或JSON架构或表单数据模型）。 可以将自适应表单的表单模型从“无”更改为其他表单模型。 对于基于表单模型的自适应表单，您可以为同一表单模型选择其他表单模板、XML架构、JSON架构或表单数据模型。 但是，不能将一个表单模型更改为另一个表单模型。

1. 选择自适应表单，然后点按&#x200B;**属性**&#x200B;图标。
1. 打开&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡，然后执行下列操作之一。

   * 如果自适应表单没有表单模型，则可以选择其他表单模型，并相应地选择表单模板、XML或JSON架构或表单数据模型。
   * 如果自适应表单基于表单模型，则可以为同一表单模型选择其他表单模板、XML或JSON架构，或表单数据模型。

1. 点按&#x200B;**[!UICONTROL Save]**&#x200B;以保存属性。

## 自动保存自适应表单{#auto-save-an-adaptive-form}

默认情况下，自适应表单的内容会在用户操作（如按保存按钮）中保存。 您还可以配置自适应表单，以根据事件或时间间隔自动开始保存内容。 自动保存选项在以下位置很有用：

* 自动保存匿名用户和登录用户的内容
* 在无需或最少用户干预的情况下保存表单的内容
* 开始根据用户事件保存表单的内容
* 在指定的时间间隔后重复保存表单的内容

### 为自适应表单{#enable-auto-save-for-an-adaptive-form}启用自动保存

默认情况下，“自动保存”选项未启用。 您可以从自适应表单的“自动保存”选项卡中启用自动保存选项。 “自动保存”选项卡还提供了其他几个配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，点按![字段级别](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后点按![cmpr](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 自动保存]**&#x200B;部分， **[!UICONTROL 启用]**&#x200B;自动保存选项。
1. 在&#x200B;**[!UICONTROL 自适应表单事件]**&#x200B;框中，指定1或TRUE，以在浏览器中加载表单时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，将开始保存表单的内容。
1. 指定触发器。 会根据您的配置触发自动保存。 您的选项包括：

   * **[!UICONTROL 基于时间：]** 选择选项以根据特定时间间隔开始保存内容。
   * **[!UICONTROL 基于事件：]** 选择选项，以在触发事件时开始基于内容进行保存。

   选择触发器时，将启用“策略配置”框。 “策略配置”框允许您：

   * 如果选择&#x200B;**[!UICONTROL 基于时间]**&#x200B;触发器，请指定时间间隔。
   * 如果选择&#x200B;**[!UICONTROL 基于事件]**&#x200B;的触发器，请指定事件名称。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在&#x200B;**[!UICONTROL 自动保存此间隔]**&#x200B;框中，以秒为单位指定时间间隔。 在间隔框中指定的秒数过后，表单会重复保存。

1. （仅限基于事件的自动保存）执行以下步骤以配置用于基于事件的自动保存的选项。

   1. 在&#x200B;**[!UICONTROL 此事件后自动保存]**&#x200B;框中，指定[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)事件。 每次表达式计算为TRUE时，都会保存表单。

1. （可选）要自动保存匿名用户的内容，请选择&#x200B;**[!UICONTROL 为匿名用户启用自动保存]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >要使自动保存选项对匿名用户有效，请确保您配置Forms通用配置服务，以允许所有用户预览、验证和签名表单。
   >
   >要配置服务，请转到位于`https://'[server]:[port]'system/console/configMgr`的Adobe Experience Manager Web控制台配置，并编辑&#x200B;**[!UICONTROL Forms Common Configuration Service]**&#x200B;以在&#x200B;**[!UICONTROL Allow]**&#x200B;字段中选择&#x200B;**[!UICONTROL All Users]**&#x200B;选项，然后保存配置。
