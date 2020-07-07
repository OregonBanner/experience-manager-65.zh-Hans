---
title: 使用表单数据模型
seo-title: 使用表单数据模型
description: 了解如何使用表单数据模型创建和使用自适应表单和交互式通信。
seo-description: 了解如何使用表单数据模型创建和使用自适应表单和交互式通信。
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# 使用表单数据模型{#use-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms数据集成允许您使用不同的后端数据源来创建表单模式模型，您可以在各种自适应表单和交互式通信工作流中将其用作。 它需要配置数据源，并根据数据源中提供的数据模型对象和服务创建表单数据模型。 有关更多信息，请参阅下列主题：

* [AEM Forms数据集成](../../forms/using/data-integration.md)
* [配置数据源](../../forms/using/configure-data-sources.md)
* [创建表单数据模型](../../forms/using/create-form-data-models.md)
* [使用表单数据模型](../../forms/using/work-with-form-data-model.md)

表单模式模型是JSON的扩展，您可以使用它：

* [创建自适应表单和片段](#create-af)
* [创建交互式通信和构件块，如文本、列表和条件片段](#create-ic)
* [预览交互式通信与样本数据](#preview-ic)
* [预填自适应表单和交互式通信](#prefill)
* [将提交的自适应表单数据写入数据源](#write-af)
* [使用自适应表单规则调用服务](#invoke-services)

## 创建自适应表单和片段 {#create-af}

您可以根据 [表单](../../forms/using/creating-adaptive-form.md)[数据模型创建自](../../forms/using/adaptive-form-fragments.md) 适应表单和自适应表单片段。 在创建自适应表单或自适应表单片段时，请执行以下操作以使用表单数据模型：

1. 在“添加属性”屏幕的“表单模型”选项卡 **[!UICONTROL 中，在“从选]** 择中 **[!UICONTROL ”下]** 拉列表中选择“表单数据模型”。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点按以展开 **[!UICONTROL 选择表单数据模型]**。 列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

1. (仅&#x200B;**限自适应表单片段**)您可以基于表单数据模型中只有一个数据模型对象来创建自适应表单片段。 展开 **[!UICONTROL “表单数据模型定义]** ”下拉列表。 它列表指定表单数据模型中的所有数据模型对象。 从列表中选择一个数据模型对象。

   ![create-af-3](assets/create-af-3.png)

创建基于表单数据模型的自适应表单或自适应表单片段后，表单数据模型对象将以自适应表单编辑器的形式 **[!UICONTROL 显示在内容浏览器的]** “数据模型对象”选项卡中。

>[!NOTE]
>
>对于自适应表单片段，只有创作时选择的数据模型对象及其关联的数据模型对象才会显示在“数据模型对象”选项卡中。

![data-model-objects-tab](assets/data-model-objects-tab.png)

您可以将数据模型对象拖放到自适应表单或片段上以添加表单字段。 添加的表单字段将保留元数据属性并与数据模型对象属性绑定。 绑定确保在提交表单时在相应数据源中更新字段值，并在呈现表单时预填字段值。

## 创建交互式通信 {#create-ic}

您可以基于表单数据模型创建交互式通信，您可以使用配置数据源中的数据预填交互式通信。 此外，诸如文本、列表和条件文档片段的交互式通信的构件块可以基于表单数据模型。

在创建交互式通信或文档片段时，可以选择表单数据模型。 下图显示了“创建交互式通信”对话框的“常规”选项卡。

![create-ic](assets/create-ic.png)

“创建交互式通信”对话框的“常规”选项卡

有关详细信息，请参阅：

[创建交互式通信](../../forms/using/create-interactive-communication.md)

[交互通信中的文本](/help/forms/using/texts-interactive-communications.md)

[交互通信中的条件](/help/forms/using/conditions-interactive-communications.md)

[列表片段](/help/forms/using/lists.md)

## 预览样本数据 {#preview-ic}

表单数据模型编辑器允许您为表单数据模型中的数据模型对象生成和编辑示例数据。 您可以使用此数据来预览和测试交互式通信和自适应表单。 预览前必须生成示例数据，如使用表单数 [据模型中所述](../../forms/using/work-with-form-data-model.md#sample)。

预览与示例表单数据模型数据的交互通信：

1. 在AEM作者实例中，导航到 **[!UICONTROL 表单>表单和文档]**。
1. 选择交互式通信并点 **[!UICONTROL 击工]** 具栏中的预览 ****，以选择Web **[!UICONTROL 渠道、打]**&#x200B;印渠道 **[!UICONTROL ，或者两]** 个渠道都预览交互式通信。
1. 在“预览 [*渠道*] ”对话框中，确保选 **[!UICONTROL 择“表单模型的测试数据]** ”并点按 **[!UICONTROL 预览]**。

交互式通信打开时会显示预填样本数据。

![Web预览](assets/web-preview.png)

同样，要将自适应表单与样本数据预览，请在创作模式下打开自适应表单并点按 **[!UICONTROL 预览]**。

## 使用表单数据模型服务预填 {#prefill}

AEM Forms提供现成的表单数据模型预填服务，您可以启用该服务来实现基于表单数据模型的自适应表单和交互式通信。 预填充服务查询自适应表单和交互式通信中的数据模型对象的数据源，并相应地在呈现表单或通信时预填充数据。

要为自适应表单启用表单容器模型预填服务，请打开自适应表单属性，并从基 **[!UICONTROL 本折叠面板的预填服务]****** 下拉菜单中选择表单数据模型预填服务。 然后，保存属性。

![预填服务](assets/prefill-service.png)

要在交互通信中配置表单数据模型预填服务，您可以在创建表单数据模型预填服务时或稍后通过修改属性，从“预填服务”下拉列表中选择“表单数据模型预填服务”。

![edit-ic-props](assets/edit-ic-props.png)

交互式通信的“编辑属性”对话框

## 将提交的自适应表单数据写入数据源 {#write-af}

当用户基于表单数据模型提交表单时，您可以配置表单以将数据模型对象的提交数据写入其数据源。 为了实现此用例，AEM Forms提 [供表单数据模型提交操作](../../forms/using/configuring-submit-actions.md)，该操作现成仅可用于基于表单数据模型的自适应表单。 它将数据模型对象的提交数据写入其数据源中。

要配置表单容器模型提交操作，请打开自适应表单属性，然后从提交折叠 **[!UICONTROL 面板下的提交操作下拉菜单中选择]** “使用表单数据模型提交”。 然后，从要提交的数据模型对象的“名 **[!UICONTROL 称”(Name)下拉框中浏览并选择]** 一个数据模型对象。 保存属性。

在表单提交时，将配置的数据模型对象的数据写入到相应的数据源。

![数据提交](assets/data-submission.png)

您还可以使用二进制数据模型对象属性将表单附件提交到数据源。 执行以下操作，将附件提交到JDBC数据源：

1. 向表单数据模型添加包含二进制属性的数据模型对象。
1. 在自适应表单中，将文件附 **[!UICONTROL 件组件从]** “组件”浏览器拖放到自适应表单上。
1. 点按以选择添加的组件， ![然后点按settings_icon](assets/settings_icon.png) 以打开该组件的“属性”浏览器。
1. 在“绑定引用”字段中，点 ![按文件夹search_](assets/foldersearch_18.png) 18，然后导航以选择您在表单数据模型中添加的二进制属性。 根据需要配置其他属性。

   点 ![按复选按钮](assets/check-button.png) ，保存属性。 附件字段现在绑定到表单数据模型的二进制属性。

1. 在自适应表单容器属性的“提交”部分，启用“提 **[!UICONTROL 交表单附件]**”。 在提交表单时，它将二进制属性字段中的附件提交到数据源。

## 使用规则调用自适应表单中的服务 {#invoke-services}

在基于表单数据模型的自适应表单中，您可以创 [建规则](../../forms/using/rule-editor.md) ，以调用在表单数据模型中配置的服务。 规 **[!UICONTROL 则中的调用]** “服务”操作列表表单数据模型中的所有可用服务，并允许您为服务选择输入和输出字段。 您还可以使用“ **设置值** ”规则类型调用表单数据模型服务，并将字段的值设置为服务返回的输出。

例如，以下规则调用以员工ID为输入的get服务，并在表单中相应的从属ID、姓、名和性别字段中填充返回的值。

![调用服务](assets/invoke-service.png)

此外，还可以使用 `guidelib.dataIntegrationUtils.executeOperation` API在规则编辑器的代码编辑器中编写JavaScript。 有关API详细信息，请 [参阅用于调用表单数据模型服务的API](/help/forms/using/invoke-form-data-model-services.md)。
