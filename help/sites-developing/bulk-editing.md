---
title: 配置页面以批量编辑页面属性
seo-title: 配置页面以批量编辑页面属性
description: 通过批量编辑页面属性，您可以一次编辑多个页面的属性
seo-description: 通过批量编辑页面属性，您可以一次编辑多个页面的属性
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 7%

---

# 配置页面以批量编辑页面属性{#configuring-your-page-for-bulk-editing-of-page-properties}

[批量编辑页](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 面属性允许您一次编辑多个页面的属性。

由于值可能不同，因此默认情况下不会启用页面属性以进行批量编辑。 必须明确允许（启用）这些规则。 在定义可批量编辑的页面属性时，您需要考虑某些影响，例如：

* 某些字段通常是唯一的；例如页面标题。 当将应用一个值时，您必须确定启用此类字段以进行批量编辑是否有意义。
* 某些字段可能具有多个值 — 这在渲染时需要有意义的表示形式。

   例如，一个复选框，指示“准备发布”。 在批量编辑之前，这可能会有多个值（例如，准备就绪、正在审阅、正在进行）。

>[!CAUTION]
>
>批量编辑页面属性的方法如下：
>
>* 在经典UI中不可用。
>* 不适用于Live Copy中的页面。
>* 仅适用于具有相同资源类型的页面。

>



>[!NOTE]
>
>批量编辑功能也可用于资产。 其操作大体相同，只有少数几点差别。有关完整的信息，请参阅[编辑多个资产的属性](/help/assets/metadata.md)。您可以使用[架构编辑器](/help/assets/metadata-schemas.md)自定义资产的批量元数据编辑器中的字段。

## 启用字段{#enabling-a-field}

>[!NOTE]
>
>某些字段可能具有多个值 — 这在渲染时需要有意义的表示形式。 因此，您应仅启用以下字段类型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



在页面组件上启用字段（模板上的&#x200B;*not*）：

1. 使用CRXDE Lite（或等效的方法）打开页面组件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此示例假定已在实例上安装核心组件，如果实例正在与We.Retail示例内容一起运行，则是如此。 有关更多信息，请参阅[核心组件文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

1. 导航到`cq:dialog`定义中的必填字段。
1. 在字段节点上定义以下属性：

   * **名称**: `allowBulkEdit`
   * **类型**: `Boolean`
   * **值**:  `true`

   例如，对于标准页面[foundation组件](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   该资产将在以下位置定义：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >***必须***&#x200B;不更改`/libs`路径中的任何内容。
   >
   >这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
   >
   >配置和其他更改的推荐方法是：
   >
   >    1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
   >    1. 在`/apps`中进行任何更改


1. 选择&#x200B;**全部保存**&#x200B;以保留更新。
