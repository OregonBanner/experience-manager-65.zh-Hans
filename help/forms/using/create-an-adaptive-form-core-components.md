---
title: 如何创建自适应表单？
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: 了解如何使用创建自适应表单 [!DNL Experience Manager Forms]. 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 1b97dc536550da8904bc7da09e983e0722c42a3d
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 4%

---


# 创建基于核心组件的自适应Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe建议使用核心组件来 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 或 [创建独立的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html) |

**适用于：** ✅自适应表单核心组件❎ [自适应表单基础组件](/help/forms/using/create-adaptive-form.md).


自适应表单可让您创建引人入胜、响应式、动态和自适应的表单。AEM Forms为商业用户提供易于使用的UI以快速创建自适应Forms。 UI提供快速选项卡导航，以轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，请了解可供您使用的Forms组件类型：

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化数据捕获组件。 这些组件为您的数字注册体验提供自定义功能、缩短开发时间并降低维护成本。 开发人员可以轻松自定义这些组件并为它们设置样式。 Adobe建议利用这些现代化的、可扩展的组件来开发自适应Forms。

* [自适应Forms Foundation组件](creating-adaptive-form.md)：它们是经典（旧）数据捕获组件。 您可以继续使用这些组件来编辑现有的基于基础组件的自适应表单。 如果您正在创建表单，Adobe建议使用  [自适应Forms核心组件](/help/forms/using/create-adaptive-form.md) 创建自适应Forms。

## 先决条件

创建自适应表单需要满足以下条件：

* **为您的环境启用自适应Forms核心组件**：需要AEM Archetype项目版本41或更高版本， [为您的环境启用核心组件](/help/forms/using/enable-adaptive-forms-core-components.md). 在为您的环境启用核心组件时， **自适应Forms（核心组件）** 模板和画布主题将添加到您的环境中。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（布局和样式）。 它具有包含特定属性和内容结构的预格式化的组件。 它还提供定义主题和提交操作的选项。 主题定义外观，提交操作定义在提交自适应表单时要执行的操作。

  >[!NOTE]
  >
  > 如果你没有， **自适应Forms（核心组件）** 环境模板， [为您的环境启用自适应Forms核心组件](/help/forms/using/enable-adaptive-forms-core-components.md). 在为您的环境启用核心组件时， **自适应Forms（核心组件）** 模板即添加到您的环境中。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。 样式包括诸如背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式反映在相应的组件上。  此 `Canvas` 在为环境启用核心组件时，默认添加主题。 您还可以 [下载和自定义标准主题](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **权限**：将您的用户添加到 [!DNL forms-users] 组。 董事会成员 [!DNL forms-users] 组有权创建自适应表单。 有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).

## 创建自适应表单 {#create-an-adaptive-form}

1. 登录到您的本地 [AEM创作实例](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. 在“Experience Manager登录”页上输入您的凭据。 登录后，在左上角，点按 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]**  > **[!UICONTROL 创建自适应Forms]**.

1. 选择自适应Forms核心组件模板并单击 **[!UICONTROL 下一个]**.

1. 此 **[!UICONTROL 添加属性]** 显示。 指定以下属性字段的值。 “标题”和“名称”字段是必填字段：

   * **[!UICONTROL 标题：]** 指定表单的显示名称。 标题可帮助您识别 [!DNL Experience Manager Forms] 用户界面。
   * **[!UICONTROL 名称：]** 指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成“名称”字段的值。 您可以更改建议值。 名称字段只能包含字母数字字符、连字符和下划线。
   * **[!UICONTROL 描述：]** 指定有关表单的详细信息。
   * **[!UICONTROL 主题客户端库]：** 指定自适应表单的主题。 默认情况下， `adaptiveform.theme.canvas3` 已选择主题。 您还可以从中选择不同的主题 **[!UICONTROL 主题客户端库]** 下拉菜单。
   * **[!UICONTROL 配置容器：]**  定义存储自适应Forms配置文件的位置。 这些配置文件包含与自适应Forms的行为和外观相关的设置和属性。
   * **[!UICONTROL 标记：]** 指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在 **[!UICONTROL 标记]** 盒子。
1. 点按 **[!UICONTROL 创建]**. 创建自适应表单，并显示用于打开表单进行编辑的对话框。


1. 点按 **[!UICONTROL 编辑]** 以在新选项卡中打开新创建的表单。 将打开表单进行编辑，并显示模板中的可用内容。 它还会显示用于自定义新创建的表单的侧栏。


## 使用自适应Forms核心组件创建表单

打开表单进行编辑后，您可以使用可用的自适应Forms核心组件将表单字段添加到表单。 您可以拖放或使用+ [插入组件] 选项将这些组件添加到表单。 请参阅AEM核心组件文档，了解可用组件 [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). 您也可以访问 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心组件运行情况。

## 为自适应表单配置提交操作 {#configure-submit-action-for-form}

提交操作允许您选择通过自适应表单捕获的数据的目标。 当用户单击自适应表单上的提交按钮时，会触发该事件。 自适应表单包括一些开箱即用的提交操作。 您还可以扩展默认提交操作以创建自己的自定义提交操作。 要为表单配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。

1. 单击  **[!UICONTROL 提交]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置提交操作](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 选择并配置 **[!UICONTROL 提交操作]**，具体取决于您的要求。 有关提交操作的详细信息，请参阅 [自适应表单提交操作](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 将用户重定向到页面或在提交表单时显示感谢消息

在提交表单时，您可以将用户重定向到其他网页或消息。 要重定向用户或配置感谢消息，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 提交]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置重定向页面或感谢消息](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * 要配置重定向URL，请为提交选项选择 **[!UICONTROL 重定向到URL]** 选项，然后浏览并选择AEM Sites页面，或提供外部页面的URL。

   * 要配置自定义或感谢消息，请在“提交”选项中选择 **[!UICONTROL 显示消息]** 选项，并在 **[!UICONTROL 消息内容]** 盒子。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。

## 为自适应表单配置架构或表单数据模型 {#configure-schema-or-data-model-for-form}

您可以使用表单数据模型将表单连接到数据源，以根据用户操作发送和接收数据。 您还可以将表单连接到JSON架构，以预定义格式接收提交的数据。 根据要求，将表单连接到JSON架构或表单数据模型：

* [创建JSON架构并上传到您的环境](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [创建表单数据模型](/help/forms/using/create-form-data-models.md)

### 为表单配置JSON架构或表单数据模型

要为表单配置JSON架构或表单数据模型，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 打开 **[!UICONTROL 数据模型]** 选项卡。

   ![单击扳手图标以打开自适应表单容器对话框以配置JSON架构或表单数据模型](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根据您的要求，选择并配置JSON架构或表单数据模型：

   * 当您选择 **[!UICONTROL 表单模型]** 选项，使用 **[!UICONTROL 选择表单数据模型]** 选项以选择预配置的表单数据模型。
   * 当您选择 **[!UICONTROL 架构]** 选项，使用 **[!UICONTROL 架构]** 选项来为您的表单选择JSON架构。

1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!NOTE]
>
> 您可以使用指南容器属性编辑自适应表单的JSON架构或表单数据模型。

## 配置预填充服务  {#configure-prefill-service-for-form}

您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 您可以：

* [创建自定义预填充服务](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [使用表单数据模型预填充服务](#fdm-prefill-service)

### 使用表单数据模型预填充服务预填充自适应表单的字段 {#fdm-prefill-service}

您可以使用表单数据模型预填充服务预填充使用表单数据模型或自定义预填充服务的自适应表单的字段。 表单数据模型预填充服务使用 [获取已配置表单数据模型的服务](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 以检索数据。 要对自适应表单使用表单数据模型预填充服务，请执行以下操作：

1. 打开内容浏览器，然后选择 **[!UICONTROL 参考线容器]** 自适应表单的组件。
1. 单击指南容器属性 ![指南属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开“自适应表单容器”对话框。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg) 图标。 随即会打开用于配置数据模型的自适应表单容器对话框。
   ![单击扳手图标以打开自适应表单容器对话框以配置重定向页面或感谢消息](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. 选择表单数据模型. 打开 **[!UICONTROL 基本]** 选项卡。 在预填充服务中，选择 **[!UICONTROL 表单数据模型预填充服务]**.
1. 单击&#x200B;**[!UICONTROL 完成]**。您的自适应表单现在配置为使用表单数据模型预填充。 您现在可以使用 [规则编辑器](rule-editor.md) 创建规则以预填充表单的字段。

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and tap ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Tap **[!UICONTROL Save]** to save the properties.
-->

## 后续内容

* [使用规则编辑器向表单添加动态行为](rule-editor.md)
* [创建或自定义基于核心组件的自适应Forms的主题](create-or-customize-themes-for-adaptive-forms-core-components.md)
* 为基于核心组件的自适应Forms创建模板

## 另请参阅

* [创建基于核心组件的自适应表单](create-an-adaptive-form-core-components.md)
* [创建自适应表单或将其添加到AEM Sites页面或体验片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)

