---
title: 自定义页面属性的视图
seo-title: 自定义页面属性的视图
description: 每个页面都有一组属性，您可以根据需要对其进行编辑
seo-description: 每个页面都有一组属性，您可以根据需要对其进行编辑
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 自定义页面属性的视图{#customizing-views-of-page-properties}

每个页面都有一组[属性](/help/sites-authoring/editing-page-properties.md)，供用户查看和编辑；创建页面（创建视图）时需要使用其中一些组件，以后可以查看和编辑（编辑视图）其他组件。 这些页面属性由相应页面组件的对话框(`cq:dialog`)定义并提供。

>[!CAUTION]
>
>经典UI中不提供自定义页面属性视图。

每个页面属性的默认状态为：

* (例如，**创建页面**&#x200B;向导)

* 可在编辑视图中使用(例如，**查看属性**)

如果需要进行任何更改，则必须专门配置字段。 可以使用相应的节点属性完成此操作：

* 可在创建视图中使用的页面属性(例如，**创建页面**&#x200B;向导):

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 可在编辑视图中使用的页面属性(例如，**查看**/**编辑**)**属性**&#x200B;选项):

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

例如，请参阅基础页面组件&#x200B;**基本**&#x200B;选项卡的&#x200B;**更多标题和描述**&#x200B;下分组的字段设置。 在&#x200B;**创建页面**&#x200B;向导中，会显示这些内容，因为`cq:showOnCreate`已设置为`true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>有关自定义页面属性的指南，请参阅[扩展页面属性教程](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 。

## 配置页面属性{#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用的字段。

例如，默认情况下，[**创建页面**&#x200B;向导](/help/sites-authoring/managing-pages.md#creating-a-new-page)显示在&#x200B;**更多标题和描述**&#x200B;下分组的字段。 要隐藏这些内容，请配置：

1. 在`/apps`下创建页面组件。
1. 为页面组件的`basic`部分创建覆盖（使用&#x200B;*对话框diff*&#x200B;由[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)提供）；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >请参阅：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
   这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
   配置和其他更改的推荐方法是：
   1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
   1. 在`/apps`中进行任何更改


1. 将`basic`上的`path`属性设置为指向基本选项卡的覆盖（另请参阅下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相应路径上创建对`basic` - `moretitles`部分的覆盖；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用相应的节点属性：

   * **名称**: `cq:showOnCreate`
   * **类型**: `Boolean`
   * **值**:  `false`

   **更多标题和描述**&#x200B;部分将不再显示在&#x200B;**创建页面**&#x200B;向导中。

>[!NOTE]
有关更多详细信息，请参阅[在页面属性上配置MSM锁定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 。

## 页面属性{#sample-configuration-of-page-properties}的示例配置

此示例演示了[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)的对话框差异技术；包括使用[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它还说明了`cq:showOnCreate`和`cq:hideOnEdit`的用法。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-page-dialog项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
