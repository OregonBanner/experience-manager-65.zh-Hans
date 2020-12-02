---
title: 自定义视图页面属性
seo-title: 自定义视图页面属性
description: 每个页面都有一组属性，您可以根据需要进行编辑
seo-description: 每个页面都有一组属性，您可以根据需要进行编辑
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# 自定义页面属性的视图符{#customizing-views-of-page-properties}

每页都有一组[属性](/help/sites-authoring/editing-page-properties.md)，用户可以查看和编辑；创建页面时需要某些视图(创建视图)，其他页面则可在以后的阶段进行查看和编辑（编辑）。 这些页面属性由相应页面组件的对话框(`cq:dialog`)定义并提供。

>[!CAUTION]
>
>自定义页面属性视图在经典UI中不可用。

每个页面属性的默认状态为：

* (例如，**创建页面**&#x200B;向导)

* (例如，**视图属性**)

如果需要任何更改，则必须明确配置字段。 使用相应的节点属性完成此操作：

* 要在创建视图中可用的页面属性(例如，**创建页面**&#x200B;向导):

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 可在编辑视图中使用的页面属性(例如，**视图**/**编辑**)**属性**&#x200B;选项):

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

例如，请参阅基础页面组件&#x200B;**基本**&#x200B;选项卡上&#x200B;**更多标题和说明**&#x200B;下分组的字段设置。 在&#x200B;**创建页面**&#x200B;向导中可以看到这些内容，因为`cq:showOnCreate`已设置为`true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>有关自定义页面属性的指南，请参阅[扩展页面属性教程](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html)。

## 配置页面属性{#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用字段。

例如，默认情况下，[**创建页面**&#x200B;向导](/help/sites-authoring/managing-pages.md#creating-a-new-page)显示在&#x200B;**更多标题和说明**&#x200B;下分组的字段。 要隐藏这些内容，请配置：

1. 在`/apps`下创建页面组件。
1. 为页面组件的`basic`部分创建覆盖（使用[Sling Resource Mergare](/help/sites-developing/sling-resource-merger.md)提供的&#x200B;*对话框diff*）;例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >请参阅：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，***必须***&#x200B;不更改`/libs`路径中的任何内容。
   这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
   建议的配置和其他更改方法是：
   1. 在`/apps`下重新创建所需项（即，它存在于`/libs`中）
   1. 在`/apps`中进行任何更改


1. 在`basic`上设置`path`属性，以指向基本选项卡的覆盖（另请参见下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相应路径上创建`basic` - `moretitles`节的覆盖；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用相应的节点属性：

   * **名称**: `cq:showOnCreate`
   * **类型**: `Boolean`
   * **值**:  `false`

   **更多标题和说明**&#x200B;部分将不再显示在&#x200B;**创建页面**&#x200B;向导中。

>[!NOTE]
当配置要与Live Copy一起使用的页面属性时，请参阅[在页面属性上配置MSM锁](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui)以了解更多详细信息。

## 页面属性配置示例{#sample-configuration-of-page-properties}

此示例演示了[Sling Resource Merabure](/help/sites-developing/sling-resource-merger.md)的对话框差异技术；包括使用[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它还说明了`cq:showOnCreate`和`cq:hideOnEdit`的用法。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-page-dialog项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
