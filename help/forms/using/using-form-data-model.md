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
feature: 表单数据模型
exl-id: 9a73a643-7ad4-49aa-a971-08d52679158d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---

# 使用表单数据模型{#use-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms数据集成允许您使用不同的后端数据源来创建表单数据模型，该模型可用作各种自适应表单和交互式通信工作流中的模式。 它需要配置数据源，并根据数据源中可用的数据模型对象和服务创建表单数据模型。 有关更多信息，请参阅下列主题：

* [AEM Forms数据集成](../../forms/using/data-integration.md)
* [配置数据源](../../forms/using/configure-data-sources.md)
* [创建表单数据模型](../../forms/using/create-form-data-models.md)
* [使用表单数据模型](../../forms/using/work-with-form-data-model.md)

表单数据模型是JSON模式的扩展，您可以使用它：

* [创建自适应表单和片段](#create-af)
* [创建交互式通信和构建基块，如文本、列表和条件片段](#create-ic)
* [使用示例数据预览交互式通信](#preview-ic)
* [预填自适应表单和交互式通信](#prefill)
* [将提交的自适应表单数据写回数据源](#write-af)
* [使用自适应表单规则调用服务](#invoke-services)

## 创建自适应表单和片段{#create-af}

您可以根据表单数据模型创建[自适应表单](../../forms/using/creating-adaptive-form.md)和[自适应表单片段](../../forms/using/adaptive-form-fragments.md)。 在创建自适应表单或自适应表单片段时，请执行以下操作以使用表单数据模型：

1. 在“添加属性”屏幕的“表单模型”选项卡中，选择&#x200B;**[!UICONTROL 从]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 表单数据模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 点按以展开&#x200B;**[!UICONTROL 选择表单数据模型]**。 将列出所有可用的表单数据模型。

   从数据模型中选择。

   ![create-af-2-1](assets/create-af-2-1.png)

1. （**仅自适应表单片段**）您可以基于表单数据模型中的一个数据模型对象来创建自适应表单片段。 展开&#x200B;**[!UICONTROL 表单数据模型定义]**&#x200B;下拉列表。 它列出了指定表单数据模型中的所有数据模型对象。 从列表中选择数据模型对象。

   ![create-af-3](assets/create-af-3.png)

创建基于表单数据模型的自适应表单或自适应表单片段后，表单数据模型对象会显示在内容浏览器的&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中的自适应表单编辑器中。

>[!NOTE]
>
>对于自适应表单片段，只有在创作时选择的数据模型对象及其关联的数据模型对象才会显示在“数据模型对象”(Data Model Objects)选项卡中。

![data-model-objects-tab](assets/data-model-objects-tab.png)

您可以将数据模型对象拖放到自适应表单或片段上以添加表单字段。 添加的表单字段将保留元数据属性并与数据模型对象属性绑定。 绑定可确保在表单提交时在相应数据源中更新字段值，并在表单呈现时预填。

## 创建交互式通信{#create-ic}

您可以基于表单数据模型创建交互式通信，您可以使用该表单数据模型预填充来自已配置数据源的数据的交互式通信。 此外，交互式通信的构建基块（如文本、列表和条件文档片段）可以基于表单数据模型。

创建交互式通信或文档片段时，可以选择表单数据模型。 下图显示了“创建交互式通信”对话框的“常规”选项卡。

![create-ic](assets/create-ic.png)

创建交互式通信对话框的“常规”选项卡

有关更多信息，请参阅：

[创建交互式通信](../../forms/using/create-interactive-communication.md)

[交互式通信中的文本](/help/forms/using/texts-interactive-communications.md)

[交互式通信中的条件](/help/forms/using/conditions-interactive-communications.md)

[列表片段](/help/forms/using/lists.md)

## 使用示例数据{#preview-ic}预览

表单数据模型编辑器允许您为表单数据模型中的数据模型对象生成和编辑示例数据。 您可以使用此数据预览和测试交互式通信和自适应表单。 在预览之前，必须生成示例数据，如[使用表单数据模型](../../forms/using/work-with-form-data-model.md#sample)中所述。

要预览与示例表单数据模型数据的交互式通信，请执行以下操作：

1. 在AEM创作实例上，导航到&#x200B;**[!UICONTROL Forms > Forms和文档]**。
1. 选择交互式通信，然后点按工具栏中的&#x200B;**[!UICONTROL 预览]**&#x200B;以选择&#x200B;**[!UICONTROL Web渠道]**、**[!UICONTROL 打印渠道]**&#x200B;或&#x200B;**[!UICONTROL 两个渠道]**&#x200B;以预览交互式通信。
1. 在预览&#x200B;[*渠道*]&#x200B;对话框中，确保选中&#x200B;**[!UICONTROL 测试表单数据模型]**&#x200B;的数据，然后点按&#x200B;**[!UICONTROL 预览]**。

打开交互式通信，其中包含预填充的示例数据。

![web预览](assets/web-preview.png)

同样，要预览带有示例数据的自适应表单，请在创作模式下打开自适应表单，然后点按&#x200B;**[!UICONTROL 预览]**。

## 使用表单数据模型服务预填充 {#prefill}

AEM Forms提供开箱即用的表单数据模型预填充服务，您可以启用该服务以便根据表单数据模型进行自适应表单和交互式通信。 预填充服务在自适应表单和交互式通信中查询数据模型对象的数据源，并相应地在呈现表单或通信时预填充数据。

要为自适应表单启用表单数据模型预填充服务，请打开自适应表单容器属性，然后从基本折叠面板的&#x200B;**[!UICONTROL 预填充服务]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 表单数据模型预填充服务]**。 然后，保存属性。

![预填充服务](assets/prefill-service.png)

要在交互式通信中配置表单数据模型预填充服务，您可以在创建表单数据模型预填充服务时或稍后通过修改属性，从“预填充服务”下拉列表中选择“表单数据模型预填充服务”。

![edit-ic-props](assets/edit-ic-props.png)

用于交互式通信的编辑属性对话框

## 将提交的自适应表单数据写入数据源{#write-af}

当用户根据表单数据模型提交表单时，您可以配置表单以将数据模型对象提交的数据写入其数据源。 为了实现此用例，AEM Forms提供了[表单数据模型提交操作](../../forms/using/configuring-submit-actions.md)，该操作现成仅适用于基于表单数据模型的自适应表单。 它会在其数据源中写入数据模型对象的提交数据。

要配置表单数据模型提交操作，请打开自适应表单容器属性，然后从提交折叠面板下的提交操作下拉列表中选择&#x200B;**[!UICONTROL 使用表单数据模型]**&#x200B;提交。 然后，从要提交的数据模型对象的&#x200B;**[!UICONTROL 名称下拉列表中浏览并选择一个数据模型对象。]**&#x200B;保存属性。

在表单提交时，将配置数据模型对象的数据写入相应的数据源。

![数据提交](assets/data-submission.png)

您还可以使用二进制数据模型对象属性将表单附件提交到数据源。 执行以下操作以将附件提交到JDBC数据源：

1. 将包含二进制属性的数据模型对象添加到表单数据模型。
1. 在自适应表单中，将组件浏览器中的&#x200B;**[!UICONTROL 文件附件]**&#x200B;组件拖放到自适应表单上。
1. 点按以选择添加的组件，然后点按![settings_icon](assets/settings_icon.png) ，以打开该组件的“属性”浏览器。
1. 在“绑定引用”字段中，点按![foldersearch_18](assets/foldersearch_18.png) ，然后导航以选择您在表单数据模型中添加的二进制属性。 根据需要配置其他属性。

   点按![check-button](assets/check-button.png)以保存属性。 附件字段现在绑定到表单数据模型的二进制属性。

1. 在自适应表单容器属性的“提交”部分中，启用&#x200B;**[!UICONTROL 提交表单附件]**。 表单提交时，它会将二进制属性字段中的附件提交到数据源。

## 使用规则{#invoke-services}在自适应表单中调用服务

在基于表单数据模型的自适应表单中，您可以[创建规则](../../forms/using/rule-editor.md)以调用在表单数据模型中配置的服务。 规则中的&#x200B;**[!UICONTROL 调用服务]**&#x200B;操作列出了表单数据模型中的所有可用服务，并允许您选择服务的输入和输出字段。 您还可以使用&#x200B;**设置值**&#x200B;规则类型来调用表单数据模型服务，并将字段的值设置为服务返回的输出。

例如，以下规则会调用以员工ID为输入的get服务，并且返回的值会填充在表单中相应的从属ID、姓氏、名字和性别字段中。

![调用服务](assets/invoke-service.png)

此外，您还可以使用`guidelib.dataIntegrationUtils.executeOperation` API在规则编辑器的代码编辑器中编写JavaScript。 有关API详细信息，请参阅[API以调用表单数据模型服务](/help/forms/using/invoke-form-data-model-services.md)。
