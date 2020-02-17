---
title: 自定义控制台
seo-title: 自定义控制台
description: AEM提供了各种机制，使您能够自定义创作实例的控制台
seo-description: AEM提供了各种机制，使您能够自定义创作实例的控制台
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 自定义控制台 {#customizing-the-consoles}

>[!CAUTION]
>
>本文档介绍如何在现代化的触屏优化UI中自定义控制台，不适用于经典UI。

AEM提供了各种机制，允许您自定义创作实例的控 [制台(和页面创作功](/help/sites-developing/customizing-page-authoring-touch.md))。

* ClientlibsClientlibs允许您扩展默认实现以实现新功能，同时重用标准函数、对象和方法。 自定义时，您可以在“例如，它可以保存自定义组件 `/apps.` 所需的代码”下创建自己的clientlib。

* OverlaysOverlays基于节点定义，允许您将标准功能(in)与您自己的自定义功能(in `/libs`)相 `/apps`叠加。 创建叠加时，不需要原始文件的1:1副本，因为sling资源合并允许继承。

这些控制台可以通过多种方式用于扩展AEM控制台。 下面将介绍一个小选项（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用和创建 [clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和创建 [叠加](/help/sites-developing/overlays.md)。
>* [花岗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>
AEM Gems会话- AEM 6.0的用 [户界面自定义中](https://docs.adobe.com/content/ddc/en/gems.html) 也介绍了本主题 [](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
>
>建议的配置和其他更改方法是：
>
>1. 在下面重新创建所需的项目(即，它存在于 `/libs`中) `/apps`
   >
   >
1. 在 `/apps`
>



例如，结构中的以下位 `/libs` 置可以覆盖：

* 控制台（任何基于Granite UI页面的控制台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>有关更多提示和工具，请参 [阅知识库文章AEM TouchUI问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)。

## 自定义控制台的默认视图 {#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、卡、列表）:

1. 您可以通过在下面覆盖所需条目来重新排序视图：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一个条目将是默认值。

   可用的节点与可用的视图选项相关联：

   * `column`
   * `card`
   * `list`

1. 例如，在列表的叠加中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定义以下属性：

   * **名称**: `sling:orderBefore`
   * **类型**: `String`
   * **值**: `column`

### 将新操作添加到工具栏 {#add-new-action-to-the-toolbar}

1. 您可以构建自己的组件并包含相应的客户端库以执行自定义操作。 例如，提 **升到Twitter** 操作：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然后，可以将其连接到控制台上的工具栏项目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在选择模式下：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 将工具栏操作限制为特定组 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自定义渲染条件来叠加标准操作，并施加在渲染之前必须满足的特定条件。

   例如，创建一个组件以根据组控制呈现条件：

   `/apps/myapp/components/renderconditions/group`

1. 要将这些应用于站点控制台上的创建站点操作，请执行以下操作：

   `/libs/wcm/core/content/sites`

   创建叠加：

   `/apps/wcm/core/content/sites`

1. 然后，为操作添加渲染条件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此节点上的属性，您可以定义 `groups` 允许执行特定操作的权限；例如， `administrators`

### 自定义列表视图中的列 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能针对文本字段的列进行了优化；对于其他数据类型，可以在中进行 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 叠加 `/apps`

要自定义列表视图中的列，请执行以下操作：

1. 覆盖可用列的列表。

   * 在节点上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 添加新列——或删除现有列。
   有关 [更多信息，请参阅使用叠加（和Sling资源合并）](/help/sites-developing/overlays.md) 。

1. 可选：

   * 如果要插入其他数据，您需要使用 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 属性.
   例如，请参阅下面附加的类／捆绑包（从GitHub）。

1. 您现在可以在列表视图的列配置器中选择列。

### 筛选资源 {#filtering-resources}

使用控制台时，一个常见用例是用户必须从资源（例如页面、组件、资产等）中进行选择。 这可以采用列表的形式，例如，作者必须从中选择一个项目。

为了使列表保持合理的大小并且与用例相关，可以以自定义谓词的形式实现过滤器。 有关 [详细信息](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) ，请参阅此文章。
