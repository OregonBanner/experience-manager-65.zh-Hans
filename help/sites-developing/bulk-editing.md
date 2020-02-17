---
title: 配置页面以批量编辑页面属性
seo-title: 配置页面以批量编辑页面属性
description: 批量编辑页面属性允许您同时编辑多个页面的属性
seo-description: 批量编辑页面属性允许您同时编辑多个页面的属性
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuring your Page for Bulk Editing of Page Properties {#configuring-your-page-for-bulk-editing-of-page-properties}

[通过批量编辑页面属性](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) ，您可以同时编辑多个页面的属性。

由于可能有不同的值，因此默认情况下不启用页面属性进行批量编辑。 它们必须明确列入白名单（已启用）。 在定义页面属性以便进行批量编辑时，您需要考虑某些含义，例如：

* 某些字段通常是唯一的；例如页面标题。 您必须决定在何时应用一个值时启用此类字段进行批量编辑是否有意义。
* 某些字段可能有多个值——这在渲染时需要有意义的表示。

   例如，一个复选框，指示“准备发布”。 在批量编辑之前，这可能具有多个值（例如，就绪、正在审阅、正在进行中）。

>[!CAUTION]
>
>页面属性的批量编辑是：
>
>* 在经典UI中不可用。
>* Live copy中的页面不可用。
>* 仅适用于具有相同资源类型的页面。
>



>[!NOTE]
>
>资产也可进行批量编辑。 其操作大体相同，只有少数几点差别。有关完整的信息，请参阅[编辑多个资产的属性](/help/assets/managing-multiple-assets.md)。You can customize the fields in the Bulk Metadata editor for Assets using the [Schema editor](/help/assets/metadata-schemas.md).

## 启用字段 {#enabling-a-field}

>[!NOTE]
>
>某些字段可能有多个值——这在渲染时需要有意义的表示。 因此，您只应启用以下字段类型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>



在页面组件（不在模板中）上&#x200B;*启用* “字段”:

1. 使用CRXDE Lite（或等效的方法）打开页面组件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此示例假定实例上已安装核心组件，即当实例与We.Retail示例内容一起运行时。 See the [Core Components documentation](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) for more information.

1. 导航到定义中的必需字 `cq:dialog` 段。
1. 在字段节点上定义以下属性：

   * **名称**: `allowBulkEdit`
   * **类型**: `Boolean`
   * **值**: `true`
   例如，对于标准页面基础 [组件](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   该属性的定义如下：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您 ***不得*** 更改路径中的任 `/libs` 何内容。
   >
   >这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
   >
   >建议的配置和其他更改方法是：
   >
   >    1. 在下面重新创建所需的项目(即，它存在于 `/libs`中) `/apps`
   >    1. 在 `/apps`


1. 选择 **全部保存** ，以保留您的更新。

