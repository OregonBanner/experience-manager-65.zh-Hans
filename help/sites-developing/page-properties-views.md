---
title: 自定义页面属性的视图
seo-title: Customizing Views of Page Properties
description: 每个页面都有一组属性，您可以根据需要对其进行编辑
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 自定义页面属性的视图{#customizing-views-of-page-properties}

每个页面都有一组 [属性](/help/sites-authoring/editing-page-properties.md) 用户可以查看和编辑；创建页面（创建视图）时需要使用其中一些组件，以后可以查看和编辑（编辑视图）其他组件。 这些页面属性由对话框( `cq:dialog`)。

>[!CAUTION]
>
>经典UI中不提供自定义页面属性视图。

每个页面属性的默认状态为：

* (例如， **创建页面** 向导)

* 可在编辑视图中使用(例如， **查看属性**)

如果需要进行任何更改，则必须专门配置字段。 可以使用相应的节点属性完成此操作：

* 可在创建视图中使用的页面属性(例如， **创建页面** 向导):

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 可在编辑视图中使用的页面属性(例如， **查看**/**编辑**) **属性** 选项):

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

例如，请参阅 **更多标题和描述** 在 **基本** 选项卡。 这些参数在 **创建页面** 向导 `cq:showOnCreate` 已设置为 `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>请参阅 [扩展页面属性教程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 以了解自定义页面属性的指南。

## 配置页面属性 {#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用的字段。

例如，默认情况下， [**创建页面** 向导](/help/sites-authoring/managing-pages.md#creating-a-new-page) 显示分组在 **更多标题和描述**. 要隐藏这些内容，请配置：

1. 在下创建页面组件 `/apps`.
1. 创建覆盖(使用 *对话框差异* 由提供 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md)) `basic` 部分；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >请参阅：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您 ***必须*** 不会更改 `/libs` 路径。
   这是因为 `/libs` 在下次升级实例时被覆盖（当您应用修补程序或功能包时，可能会被覆盖）。
   配置和其他更改的推荐方法是：
   1. 重新创建所需项目(即， `/libs`)下 `/apps`
   1. 在 `/apps`


1. 设置 `path` 属性 `basic` 以指向对基本选项卡的覆盖（另请参阅下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 创建对 `basic` - `moretitles` 路径的段；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用相应的节点属性：

   * **名称**: `cq:showOnCreate`
   * **类型**: `Boolean`
   * **值**: `false`

   的 **更多标题和描述** 部分将不再显示在 **创建页面** 向导。

>[!NOTE]
在配置要与Live Copy一起使用的页面属性时，请参阅 [在页面属性上配置MSM锁定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 以了解更多详细信息。

## 页面属性的配置示例 {#sample-configuration-of-page-properties}

此示例演示了 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md);包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). 它还说明了这两种方法的使用 `cq:showOnCreate` 和 `cq:hideOnEdit`.

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-page-dialog项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
