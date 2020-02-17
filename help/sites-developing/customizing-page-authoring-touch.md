---
title: 自定义页面创作
seo-title: 自定义页面创作
description: AEM提供了各种机制，使您能够自定义页面创作功能
seo-description: AEM提供了各种机制，使您能够自定义页面创作功能
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 自定义页面创作{#customizing-page-authoring}

>[!CAUTION]
>
>本文档介绍如何在现代化的触屏优化UI中自定义页面创作，但不适用于经典UI。

AEM提供了各种机制，使您能够自定义创作实例的页面创作功能( [和控制台](/help/sites-developing/customizing-consoles-touch.md))。

* Clientlibs

   Clientlibs允许您扩展默认实现以实现新功能，同时重用标准函数、对象和方法。 自定义时，您可以在新的clientlib必须下 `/apps.` 创建自己的clientlib:

   * 取决于创作clientlib `cq.authoring.editor.sites.page`
   * 属于相应类 `cq.authoring.editor.sites.page.hook` 别

* 叠加

   叠加基于节点定义，允许您将标准功能(in)与您自己的自定义功能( `/libs`in)相 `/apps`叠加。 创建叠加时，不需要原始文件的1:1副本，因为 [sling资源合并允许继承](/help/sites-developing/sling-resource-merger.md) 。

>[!NOTE]
>
>有关详细信息，请参 [阅JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。

这些功能可以通过多种方式在AEM实例中扩展页面创作功能。 下面将介绍一个选择（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用和创建 [clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和创建 [叠加](/help/sites-developing/overlays.md)。
>* [花岗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md) ，以了解用于页面创作的结构区域的详细信息。
>
>
AEM Gems会话- AEM 6.0的用 [户界面自定义中](https://docs.adobe.com/content/ddc/en/gems.html) 也介绍了本主题 [](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html)。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
>
>建议的配置和其他更改方法是：
>
>1. 在下面重新创建所需的项目(即，它存在于 `/libs`中) `/apps`
>1. 在 `/apps`


## 添加新图层（模式） {#add-new-layer-mode}

在编辑页面时，有多种可用 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 。 这些模式是使用图层实 [现的](/help/sites-developing/touch-ui-structure.md#layer)。 这些功能允许访问同一页面内容的不同类型的功能。 标准层有：编辑、预览、批注、开发人员和定位。

### 图层示例：Live copy状态 {#layer-example-live-copy-status}

标准AEM实例提供MSM层。 这访问与多站点管理 [相关的数据](/help/sites-administering/msm.md) ，并在层中突出显示它。

要查看其实际操作情况，您可以编辑任何 [We.Retail语言副本页面](/help/sites-developing/we-retail-globalized-site-structure.md) （或任何其他Live Copy页面）并选择 **Live copy状态模式** 。

可以在以下位置找到MSM层定义（供参考）:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例 {#code-sample}

这是一个示例包，它显示如何创建新层（模式），这是MSM视图的新层。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-new-layer-mode项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 向资产浏览器添加新选择类别 {#add-new-selection-category-to-asset-browser}

资产浏览器显示各种类型／类别（例如图像、文档等）的资产。 资产也可按这些资产类别进行筛选。

### 代码示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，其中显示如何将新组添加到资产查找器。 此示例连接到 [Flickr](https://www.flickr.com)的公共流并在侧面板中显示它们。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-assetfinder-flickr项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 筛选资源 {#filtering-resources}

创作页面时，用户通常必须从资源（例如页面、组件、资产等）中进行选择。 这可以采用列表的形式，例如，作者必须从中选择一个项目。

为了使列表保持合理的大小并且与用例相关，可以以自定义谓词的形式实现过滤器。 例如，如果使用 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite [](/help/sites-developing/touch-ui-concepts.md#granite-ui) 组件允许用户选择特定资源的路径，则可以按以下方式过滤显示的路径：

* 通过实现接口实现自定义谓 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 词。
* 指定谓词的名称，并在使用时引用该名称 `pathbrowser`。

有关创建自定义谓词的更多详细信息，请参 [阅此文章](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>通过实现接口实现自定义谓 `com.day.cq.commons.predicate.AbstractNodePredicate` 词在经典UI中同样有效。
>
>有关 [在经典UI中实现自定义谓词的示例，请参阅此知识库文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 。

## 将新操作添加到组件工具栏 {#add-new-action-to-a-component-toolbar}

每个组件（通常）都有一个工具栏，它提供对可对该组件执行的操作范围的访问。

### 代码示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，它显示如何创建用于渲染组件的自定义工具栏操作。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-toolbar-screanth项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 添加新的就地编辑器 {#add-new-in-place-editor}

### 标准就地编辑器 {#standard-in-place-editor}

在标准AEM安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   包含各种可用编辑器的定义。

1. 编辑器与每个资源类型（如组件中）之间存在连接，可以使用它：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性: `editorType`

            定义在为该组件触发就地编辑时将使用的内联编辑器类型；例如， `text`, `textimage`, `image`, `title`.

1. 可以使用包含配置的节点以及包含必要的插件配 `config` 置详细信息的其他节点来配置编辑 `plugin` 器的其他配置详细信息。

   以下是为图像组件的图像裁剪插件定义长宽比的示例。 请注意，由于屏幕大小可能非常有限，因此裁剪效果比率会移至全屏编辑器，并且只能在该处查看。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >请注意，在AEM中，由属性设置的裁剪比 `ratio` 率定义为高 **度／宽度**。 这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。The authoring users will not be aware of any difference provided you define the `name` property clearly since this is what is displayed in the UI.

#### 创建新的就地编辑器 {#creating-a-new-in-place-editor}

要实施新的就地编辑器（在clientlib中），请执行以下操作：

>[!NOTE]
>
>例如，请参阅：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）:

   * `editor.register`

1. 提供编辑器与可使用该编辑器的每个资源类型（如组件中）之间的连接。

#### 创建新就地编辑器的代码示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，它显示如何在AEM中创建新的就地编辑器。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-inplace-editor项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多个就地编辑器 {#configuring-multiple-in-place-editors}

可以配置组件，使其具有多个就地编辑器。 配置多个就地编辑器后，您可以选择适当的内容并打开相应的编辑器。 有关更 [多信息，请参阅配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md) 。

## 添加新页面操作 {#add-a-new-page-action}

要向页面工具栏添加新的页面操作，例如“返回 **站点** （控制台）”操作。

### 代码示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，它显示如何创建自定义标题栏操作以跳回站点控制台。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-header-backtosites项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自定义激活请求工作流 {#customizing-the-request-for-activation-workflow}

当内容作者没有相应的复制权限时，即 **可自动触发现成的工作流程“激活请求**”。

要在激活后进行自定义行为，您可以覆盖激活 **请求工作流** :

1. 在叠 `/apps` 加中， **站点向导** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >它本身会覆盖以下内容的常见实例：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 根据需 [要更新工作流模型](/help/sites-developing/workflows-models.md) 和相关配置／脚本。
1. 从所有相关页面的所 [ 有相 `replicate` 应用户](/help/sites-administering/security.md#actions) ，移除采取行动的权利；使此工作流在任何用户尝试发布（或复制）页面时作为默认操作触发。

