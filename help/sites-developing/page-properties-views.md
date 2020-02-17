---
title: 自定义页面属性的视图
seo-title: 自定义页面属性的视图
description: 每个页面都有一组属性，您可以根据需要编辑这些属性
seo-description: 每个页面都有一组属性，您可以根据需要编辑这些属性
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d

---


# 自定义页面属性的视图{#customizing-views-of-page-properties}

每页都有一套可供 [用户查](/help/sites-authoring/editing-page-properties.md) 看和编辑的属性；有些是创建页面（创建视图）时必需的，有些则可在以后的阶段查看和编辑（编辑视图）。 这些页面属性由相应页面组件的对话框()定 `cq:dialog`义并使其可用。

>[!CAUTION]
>
>自定义页面属性视图在经典UI中不可用。

每个页面属性的默认状态为：

* 隐藏在创建视图中(例如创建 **页面向导** )

* 在编辑视图中可用(例如，查看 **属性**)

如果需要任何更改，则必须明确配置字段。 这是使用相应的节点属性完成的：

* 在创建视图中可用的页面属性(例如，创 **建页面向导** ):

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 要在编辑视图(例如，查看／编辑 ****)属性选项&#x200B;**中可用的页**&#x200B;面属性 **** ):

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

例如，请参阅基础页面组件的“基本”选项卡 **上的更多标题和说明** ，以 **** 下分组字段的设置。 在创建页面向 **导中** ，这 `cq:showOnCreate` 些图标在设置为 `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>有关自定义 [页面属性的指南](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) ，请参阅扩展页面属性教程。

## 配置页面属性 {#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用的字段。

例如，默认情况下，“创 [**建页面&#x200B;**”向导显示在“更多标题和说](/help/sites-authoring/managing-pages.md#creating-a-new-page)明”下分组的字段****。 要隐藏这些内容，请配置：

1. 在下面创建页面组件 `/apps`。
1. 为页面组件的部分 *创建覆盖* (使用 [Sling Resource Mergare](/help/sites-developing/sling-resource-merger.md)提供的对话区 `basic` 别);例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >请参阅：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您 ***不得*** 更改路径中的任 `/libs` 何内容。
   这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
   建议的配置和其他更改方法是：
   1. 在下面重新创建所需的项目(即，它存在于 `/libs`中) `/apps`
   1. 在 `/apps`


1. 将属 `path` 性设置为 `basic` 指向基本选项卡的覆盖（另请参阅下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相应的路径 `basic` 上 `moretitles` 创建——部分的覆盖；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用相应的节点属性：

   * **名称**: `cq:showOnCreate`
   * **类型**: `Boolean`
   * **值**: `false`
   创建 **页面向导中将不再显示** “更多标题和说 **明”部分** 。

>[!NOTE]
当配置页面属性以与Live Copy一起使用时，请参 [阅在页面属性上配置MSM锁](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) ，以获取更多详细信息。

## 页面属性的示例配置 {#sample-configuration-of-page-properties}

此范例演示了 [Sling Resource Merager的对话差异技术](/help/sites-developing/sling-resource-merger.md);包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它还说明了和的使 `cq:showOnCreate` 用方 `cq:hideOnEdit`法。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-page-dialog项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
