---
title: 如何创建自适应表单
description: 了解如何使用创建自适应表单 [!DNL Experience Manager Forms]. 自适应表单是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型、XFA表单模板以及XML或JSON架构创建自适应表单。
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: 654dcb7c9bbb73420df7494b21fddb8cb4fdd39a
workflow-type: tm+mt
source-wordcount: '1936'
ht-degree: 8%

---

# 创建自适应表单 {#creating-an-adaptive-form}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html) |
| AEM 6.5 | 本文 |

## 创建自适应表单 {#strong-create-an-adaptive-form-strong}

按照以下步骤创建自适应表单。

1. 访问 [!DNL Experience Manager Forms] 创作实例位于 `https://'[server]:[port]'/<custom-context-if-any>.`

1. 在 Experience Manager 登录页面上输入您的凭据。

   登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。

   >[!NOTE]
   >
   >对于默认安装，登录为 `admin` 密码是 `admin`.

1. 点按 **[!UICONTROL 创建]** 并选择 **[!UICONTROL 自适应表单]**.
1. 此时会显示一个用于选择模板的选项。 有关模板的详细信息，请参阅 [自适应表单模板](creating-adaptive-form.md#p-adaptive-form-templates-p). 点按模板以将其选定，然后点按下一步。
1. 将显示“添加属性”选项。 指定以下属性字段的值。 标题和名称字段是必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。 标题可帮助您在 [!DNL Experience Manager Forms] 用户界面中标识表单。
   * **[!UICONTROL 名称：]**&#x200B;指定表单的名称。在存储库中创建具有指定名称的节点。在开始键入标题时，名称字段的值将自动生成。您可以更改建议的值。名称字段只能包含字母数字字符、连字符和下划线。所有无效的输入都将替换为连字符。
   * **[!UICONTROL 描述：]** 指定有关表单的详细信息。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在 **[!UICONTROL 标记]** 盒子。

1. 您可以基于以下表单模型之一创建自适应表单：

   * [表单数据模型](#fdm)
   * [XFA表单模板](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML或JSON架构](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 无或不带任何表单模型

   您可以从以下位置配置这些权限： **[!UICONTROL 表单模型]** 选项卡 **[!UICONTROL 添加属性]** 页面。 默认情况下，选定的表单模型为 **[!UICONTROL 无]**.

1. 点按&#x200B;**[!UICONTROL 创建]**。创建自适应表单，并显示用于打开表单进行编辑的对话框。

   指定完所有属性后，单击 **[!UICONTROL 创建]**. 创建自适应表单，并显示用于打开表单进行编辑的对话框。

   指定完所有属性后，单击 **[!UICONTROL 创建]**. 创建自适应表单，并显示用于打开表单进行编辑的对话框。

1. 点按 **[!UICONTROL 打开]** 以在新选项卡中打开新创建的表单。 将打开表单进行编辑，并显示模板中的可用内容。 它还显示边栏，可用于根据需要自定义新创建的表单。

   根据自适应表单的类型，关联的XFA表单模板、XML架构或JSON架构中存在的表单元素将显示在 **[!UICONTROL 数据模型对象]** 选项卡 **[!UICONTROL 内容浏览器]** 在侧栏中。 您还可以拖放这些元素以构建自适应表单。

   有关自适应表单创作界面和可用组件的信息，请参阅 [自适应表单创作简介](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >允许浏览器中的弹出窗口在新选项卡中打开新创建的表单。

## 基于表单数据模型创建自适应表单 {#fdm}

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 可让您集成多个数据源，并将其实体和服务整合在一起，以创建表单数据模型。 它是JSON架构的扩展。 您可以使用表单数据模型创建自适应表单。 在表单数据模型中配置的实体或数据模型对象可用作表单创作的数据模型对象。 它们绑定到各自的数据源，并用于预填充表单并将提交的数据写回各自的数据源。 您还可以使用自适应表单规则调用在表单数据模型中配置的服务。

要使用表单数据模型创建自适应表单，请执行以下操作：

1. 在添加属性屏幕上的表单模型选项卡中，选择 **[!UICONTROL 表单数据模型]** 在 **[!UICONTROL 选择自]** 下拉列表。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点击以展开 **[!UICONTROL 选择表单数据模型]**. 列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您还可以更改自适应表单的表单数据模型。 有关详细步骤，请参阅 [编辑自适应表单的表单模型属性](#edit-form-model).

## 基于XFA表单模板创建自适应表单 {#create-an-adaptive-form-based-on-an-xfa-form-template}

您可以重新利用XFA表单模板来创建自适应表单。 要重新调整用途，请上传XFA表单模板并将其与自适应表单关联。 表单模板（XFA表单）的元素可在自适应表单创作时在内容查找器中使用。 从内容查找器中，您可以将表单模板元素拖放到表单上。

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

## 创建基于XML或JSON架构的自适应表单 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON架构表示组织中的后端系统生成或使用数据的结构。 您可以将架构关联到自适应表单，并使用其元素将动态内容添加到自适应表单。 架构的元素在内容浏览器的数据模型对象选项卡中可用，用于创作自适应表单。 您可以拖放架构元素来构建表单。

请参阅以下文档，了解如何为创作自适应表单设计XML或JSON架构。

* [使用XML架构创建自适应表单](adaptive-form-xml-schema-form-model.md)
* [使用JSON架构创建自适应表单](adaptive-form-json-schema-form-model.md)

执行以下操作以使用XML或JSON架构作为自适应表单的表单模型：

1. 在 **[!UICONTROL 添加属性]** 自适应表单创建页面的步骤，点击 **[!UICONTROL 表单模型]** 选项卡。
1. 在表单模型选项卡中，选择 **[!UICONTROL 架构]** 从 **[!UICONTROL 选择自]** 下拉字段。

1. 点按 **[!UICONTROL 选择架构]** 并执行以下操作之一：

   * **[!UICONTROL 从磁盘上传]**  — 选择此选项并点按上传架构定义，以浏览并从您的文件系统上传XML架构或JSON架构。 上传的架构文件驻留在表单中，其他自适应表单无法访问。
   * **[!UICONTROL 在存储库中搜索]**  — 选择此选项可从存储库中可用的架构定义文件列表中进行选择。 选择XML或JSON架构文件作为表单模型。 所选架构通过引用与表单相关联，并且可在其他自适应表单中使用。

   >[!CAUTION]
   >
   >请确保JSON架构文件名以结尾 **.schema.json**. 例如：mySchema.schema.json

   ![选择XML或JSON架构](assets/upload-schema.png)
   **图：** *选择XML或JSON架构*

1. （仅适用于XML架构）选择或上传XML架构后，请指定要与自适应表单映射的选定XSD文件的根元素。

   ![选择XSD根元素](assets/xsd-root-element.png)
   **图：** *选择XSD根元素*

>[!NOTE]
>
>您还可以更改自适应表单的架构。 有关详细步骤，请参阅 [编辑自适应表单的表单模型属性](#edit-form-model).

## 自适应表单模板 {#adaptive-form-templates}

模板提供基本结构并定义自适应表单的外观（布局和样式）。 它的预格式化的组件包含某些属性和内容结构。<!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

此外，您可以使用模板编辑器创建自己的模板。 有关使用模板的详细信息，请参阅 [自适应表单模板](template-editor.md).

>[!NOTE]
>
>打开使用高级模板创建的自适应表单进行编辑时，会显示一条错误消息。 高级模板具有签名步骤组件，并且默认情况下为其启用Adobe Sign。 创建和选择 [Adobe Sign云配置](adobe-sign-integration-adaptive-forms.md) 和 [配置签名者](working-with-adobe-sign.md#addsignerstoanadaptiveform) 以解决错误。

## 编辑自适应表单的表单模型属性 {#edit-form-model}

创建自适应表单时，不使用表单模型（对表单模型使用“无”选项），或使用表单模型（如表单模板、XML架构或JSON架构或表单数据模型）。 您可以将自适应表单的表单模型从“无”更改为其他表单模型。 对于基于表单模型的自适应表单，您可以为同一表单模型选择其他表单模板、XML架构、JSON架构或表单数据模型。 但是，不能从一个表单模型更改到另一个表单模型。

1. 选择自适应表单并点按 **属性** 图标。
1. 打开&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡并执行下列操作之一。

   * 如果自适应表单没有表单模型，您可以选择其他表单模型，并相应地选择表单模板、XML或JSON架构或表单数据模型。
   * 如果自适应表单基于表单模型，则可以为同一表单模型选择其他表单模板、XML或JSON架构或表单数据模型。

1. 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存属性。

## 自动保存自适应表单 {#auto-save-an-adaptive-form}

默认情况下，自适应表单的内容会在用户操作时保存，例如按保存按钮时。 您还可以配置自适应表单，以根据事件或时间间隔自动开始保存内容。 自动保存选项在以下方面很有用：

* 自动为匿名和登录用户保存内容
* 保存表单内容而不需要用户干预或用户干预最少
* 开始基于用户事件保存表单内容
* 在指定的时间间隔后重复保存表单的内容

### 为自适应表单启用自动保存 {#enable-auto-save-for-an-adaptive-form}

默认情况下，不启用自动保存选项。 您可以从自适应表单的“自动保存”选项卡中启用自动保存选项。 “自动保存”选项卡还提供了几个其他配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后点按 ![字段级](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后点击 ![cmppr](assets/cmppr.png).
1. 在 **[!UICONTROL 自动保存]** 部分， **[!UICONTROL 启用]** 自动保存选项。
1. 在 **[!UICONTROL 自适应表单事件]** 框中，指定1或TRUE将在浏览器中加载表单时自动开始保存表单。 您还可以为事件指定条件表达式，该表达式在触发并返回true时开始保存表单的内容。
1. 指定触发器。 根据您的配置触发自动保存。 您的选项包括：

   * **[!UICONTROL 基于时间：]** 选择选项，以根据特定时间间隔开始保存内容。
   * **[!UICONTROL 基于事件：]** 选择选项以在触发事件时开始保存内容。

   选择触发器后，将启用“策略配置”框。 通过“策略配置”框，您可以：

   * 如果您选择，请指定时间间隔 **[!UICONTROL 基于时间]** 触发器。
   * 如果您选择，请指定事件名称 **[!UICONTROL 基于事件]** 触发器。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （仅限基于时间的自动保存）执行以下步骤来配置基于时间的自动保存选项。

   1. 在 **[!UICONTROL 在此间隔自动保存]** 框中，以秒为单位指定时间间隔。 在间隔框中指定的秒数过后，将重复保存该表单。

1. （仅限基于事件的自动保存）执行以下步骤来配置用于基于事件的自动保存的选项。

   1. 在 **[!UICONTROL 在此事件后自动保存]** 框，指定 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每当表达式的计算结果为TRUE时，将保存表单。

1. （可选）要自动为匿名用户保存内容，请选择 **[!UICONTROL 为匿名用户启用自动保存]** 选项，然后单击 **[!UICONTROL 确定]**.

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保将Forms通用配置服务配置为允许所有用户预览、验证和签署表单。
   >
   >要配置服务，请转到Adobe Experience Manager Web控制台配置，网址为 `https://'[server]:[port]'system/console/configMgr` 并编辑 **[!UICONTROL Forms通用配置服务]** 以选择 **[!UICONTROL 所有用户]** 中的选项 **[!UICONTROL 允许]** 字段，并保存配置。
