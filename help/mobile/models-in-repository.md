---
title: 存储库中的模型
seo-title: 存储库中的模型
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# 存储库中的模型{#models-in-repository}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

模型包含一组数据类型，这些数据类型定义了内容服务最终将呈现的属性。 模型还定义了其他模型之间的关系，以强化数据完整性。

作为开发人员，您应该熟悉存储库中的模型结构。 您可以根据应用程序要求创建自己的模型和实体。

## 创建模型类型{#creating-model-types}

在&#x200B;*/libs/settings/mobileapps/model-types*&#x200B;下，有两种系统提供的型号类型。 如果要覆盖系统模型类型，则需要在希望覆盖发生的配置节点下创建&#x200B;*mobileapps/model-types*&#x200B;节点。

例如，如果您已在&#x200B;*/conf/myconf1*&#x200B;和&#x200B;*/conf/myconf2*&#x200B;中创建配置，并且希望仅覆盖&#x200B;*conf1*&#x200B;上的系统模型类型，则应在&#x200B;*conf1*&#x200B;设置下创建&#x200B;*mobileapps/model-types*&#x200B;节点。

如果要允许将数据类型添加到模型，则模型类型必须具有名为“scaffolding”的子节点，即类型为“cq:Page”的子节点，以及资源类型为&#x200B;*wcm/scaffolding/components/scaffolding*。

基架页面还必须在PageContent节点上包含&#x200B;*dataTypesConfig*&#x200B;属性，该属性指示将允许使用此类型创建的数据类型模型。

>[!NOTE]
>
>**Scaffolding**&#x200B;是一个页面，用于定义实体可基于模型编辑的数据类型。 还可以对每种数据类型进行配置，以定义字段在UI中的显示方式以及保留数据值的方式。

### 数据类型配置{#data-types-config}

数据类型配置节点包含数据类型项的列表。 每个数据类型项目指定数据类型在模型编辑器中的显示方式，以及需要如何持久保留该数据类型以最终由实体进行渲染。

| **属性名称** | **描述** |
|---|---|
| fieldIcon | 表示数据类型的CoralUI图标类 |
| fieldPropResourceType | 用于呈现用于配置数据类型的所有属性的组件 |
| fieldProperties | fieldPropResourceType为&#x200B;*mobileapps/caas/gui/components/models/editor/datatypes/field*&#x200B;时使用的属性组件的多值列表 |
| fieldResourceType | resource数据类型的持久节点的类型（即将在实体编辑器中呈现属性的组件） |
| fieldViewResourceType | 用于在模型编辑器视图中呈现数据类型的组件（如果忽略此属性，则将使用fieldResourceType） |
| fieldTitle | 将在模型编辑器中显示的数据类型的名称 |
| multiFieldResourceType | 选择多值时要在持久节点上使用的资源类型 |
| renderType | 用于客户端渲染的渲染提示 |

### 数据类型配置叠加{#data-types-config-overlay}

“dataTypesConfig”属性支持Sling资源合并。 这意味着，系统模型类型（甚至自定义模型类型）使用的数据类型可以通过使用覆盖节点进行自定义。

需要创建&#x200B;*/libs/settings/mobileapps/models/formbuilderconfig/datatypes*&#x200B;的叠加，然后根据需要进行自定义。

例如，可以添加字符串数据类型的叠加，以将fieldResourceType更改为自定义组件。

有关Sling资源合并的更多信息，请参阅[在AEM](/help/sites-developing/sling-resource-merger.md)中使用Sling资源合并器。

![chlimage_1-7](assets/chlimage_1-7.png)

### 数据类型 {#data-types}

模型数据类型是表单组件，能够包含在发布表单时要包含的数据。 数据类型组件可能会根据需要而复杂。 自定义数据类型的示例可以是特定国家/地区的地址块，以避免始终使用原始数据类型重新创建该数据块。

有关自定义数据类型的示例，请参阅“/libs/mobileapps/caas/components/form/contentreference”。

所有原始数据类型都使用现有的Granite表单组件。 请参阅：[https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

然后，任何自定义数据类型都可以添加到数据类型配置中，以供模型编辑器使用。

## 创建模型{#creating-models}

开发所有所需的模型类型和数据类型后，即可开始创建模型。 作者最终将使用模型创建实体，内容服务可使用这些实体来从中呈现其数据。

创建模型包括根据当前配置选取允许的模型类型，然后提供标题和描述。

要了解如何从功能板创建和管理模型，请参阅“移动设备应用程序”创作部分下的[创建模型](/help/mobile/administer-mobile-apps.md) 。

### 模型{#properties-of-a-model}的属性

下表显示了为模型定义的属性：

| **属性名称** | **描述** |
|---|---|
| 模型标题 | 模型名称 |
| 描述 | 模型描述 |
| 缩略图 | 模型的缩略图图像 |
| 模型类型 | 模型类型（这可以是一个简单的字符串或实际组件的路径） |
| 允许的子项 | 允许作为此模板子项的模板路径 |
| 允许的父项 | 允许作为此模板父项的模板路径 |

>[!NOTE]
>
>*允许的子项*&#x200B;和&#x200B;*允许的父项*&#x200B;属性遵循与页面模板相同的规则。 有关更多信息，请参阅[页面模板](/help/sites-developing/page-templates-static.md)。
>
>在引用&#x200B;*模型类型*&#x200B;属性时，所有模型都必须具有超类型&#x200B;*mobileapps/caas/components/data/entity*，但可以具有允许自定义内容交付的子类型。 确保所有模型类型都是唯一的，也可以帮助内容服务的客户端区分数据中的对象。

### 编辑模型{#editing-a-model}

编辑模型涉及打开与模型关联的基架对话框表单以进行编辑。 通常，基架是模型的子节点，但如果需要，可通过使用“cq:scaffolding”属性指定其路径，将其位于模型外部。 如果您想要在需要具有不同属性的多个模型之间共享相同的基架，则此选项非常有用。

当找到模型的基架时，模型编辑器将渲染“jcr:content/cq:dialog/content”下的任何内容。 客户端表单生成器引擎当前仅支持多达3列的固定布局。 在呈现的表单对话框的右侧，将显示数据类型配置中指定的所有数据类型的列表。 通过单击数据类型，可以对其进行编辑。 然后，右边栏将切换到选定数据类型的属性选项卡。 可以通过将新数据类型拖动到预览画布上来添加新数据类型。 单击“保存”(Save)将更改传播到服务器。 单击“取消”(Cancel)可关闭模型编辑器。

>[!NOTE]
>
>所有模型都是模板，因此它们遵循所有AEM模板规则。 这允许使用&#x200B;*allowedParents*&#x200B;和&#x200B;*allowedChildren*&#x200B;属性等属性。 在基于模型创建新图元时，这些操作非常有效。 模板规则将确保实体只能基于某些模型（具体取决于其层次结构）。
>
>要了解如何从功能板编辑模型，请参阅“移动设备应用程序”创作部分下的[创建模型](/help/mobile/administer-mobile-apps.md) 。

### 系统型号{#system-models}

提供了两种类型的预定义系统模型，以便简单地重复使用内容。 无法编辑这些模型。

**页面** 模型页面模型提供了一种快速方法，可重复使用站点中的现有内容以便由内容服务交付。

基于页面模型的实体的resourceType为：mobileapps/caas/components/data/pages

路径：站点页面的路径。 此路径中的内容（及其子项）将由内容服务处理程序渲染。

**资产** 模型资产模型提供了一种快速方法，可重复使用资产中的现有内容以通过内容服务进行交付。

基于页面模型的实体的resourceType为：*mobileapps/caas/components/data/assets.*

资产列表：资产中的路径列表。 每个资产都将作为子实体节点添加，其resourceType为&#x200B;*wcm/foundation/components/image*。

>[!NOTE]
>
>要了解有关使用这些模板从功能板创建模型的更多信息，请参阅“移动设备应用程序”创作部分下的[创建模型](/help/mobile/administer-mobile-apps.md)。
