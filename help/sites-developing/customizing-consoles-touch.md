---
title: 自定义控制台
description: AEM提供了多种机制，使您能够自定义创作实例的控制台
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 22%

---

# 自定义控制台 {#customizing-the-consoles}

>[!CAUTION]
>
>本文档介绍如何在启用触屏的现代UI中自定义控制台，并且不适用于经典UI。

AEM提供了各种机制让您能够自定义控制台(以及 [页面创作功能](/help/sites-developing/customizing-page-authoring-touch.md))。

* Clientlibs Clientlibs允许您扩展默认实施以实现新功能，同时重用标准函数、对象和方法。 进行自定义时，您可以在下面创建自己的clientlib `/apps.` 例如，它可以保存自定义组件所需的代码。

* 叠加基于节点定义，允许您叠加标准功能(在 `/libs`)中提供的自定义函数(在 `/apps`)。 创建叠加时，不需要原始内容的1:1副本，因为sling资源合并器允许继承。

可以通过多种方式使用这些变量来扩展AEM控制台。 下面包含少量选件（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用和创建 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和创建 [叠加](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>您 ***必须*** 不会更改中的任何内容 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>建议用于配置和其他更改的方法是：
>
>1. 重新创建所需项目(即，它存在于 `/libs`)，在 `/apps`
>
>1. 在中进行任何更改 `/apps`
>

例如，以下位置位于 `/libs` 结构可以重叠：

* 控制台（任何基于Granite UI页面的控制台）；例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>请参阅知识库文章， [AEM TouchUI问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以获取更多提示和工具。

## 自定义控制台的默认视图 {#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、信息卡、列表）：

1. 可通过从下覆盖所需条目来重新排序视图：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一个条目将是默认条目。

   可用的节点与可用的视图选项相关：

   * `column`
   * `card`
   * `list`

1. 例如，在列表的覆盖中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定义下列属性：

   * **名称**：`sling:orderBefore`
   * **类型**：`String`
   * **值**：`column`

### 将新操作添加到工具栏 {#add-new-action-to-the-toolbar}

1. 您可以构建自己的组件，并为自定义操作包含相应的客户端库。 例如， **提升至Twitter** 操作位置：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然后可以将其连接到控制台上的工具栏项：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在选择模式下：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 将工具栏操作限制为特定组 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自定义呈现条件来叠加标准操作，并施加在呈现它之前必须满足的特定条件。

   例如，创建一个组件以根据组控制渲染条件：

   `/apps/myapp/components/renderconditions/group`

1. 要将这些方法应用于站点控制台上的创建站点操作，请执行以下操作：

   `/libs/wcm/core/content/sites`

   创建叠加：

   `/apps/wcm/core/content/sites`

1. 然后，为操作添加rendercondition：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此节点上的属性，您可以定义`groups`允许执行特定操作；例如，`administrators`

### 在列表视图中自定义列 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能针对文本字段列进行了优化；对于其他数据类型，可以叠加 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 在 `/apps`.

要自定义列表视图中的列：

1. 叠加可用列的列表。

   * 在节点上：

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * 添加新列 — 或删除现有列。

   请参阅 [使用叠加（和Sling资源合并器）](/help/sites-developing/overlays.md) 以了解更多信息。

1. 可选：

   * 如果要插入其他数据，则需要编写 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 带有
     `pageInfoProviderType` 属性。

   例如，请参阅下面的附加类/捆绑包（来自GitHub）。

1. 现在，您可以在列表视图的列配置器中选择该列。

### 筛选资源 {#filtering-resources}

使用控制台时，常见的用例是用户必须从资源（例如，页面、组件、资源等）中进行选择的情况。 这可以采用列表形式，例如，作者必须从中选择一个项目。

为了使列表保持合理的大小并且与用例相关，可以通过自定义谓词的形式实施筛选条件。请参阅 [本文](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 以了解详细信息。
