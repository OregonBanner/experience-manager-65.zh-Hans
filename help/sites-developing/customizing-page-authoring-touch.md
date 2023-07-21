---
title: 自定义页面创作
description: Adobe Experience Manager (AEM)提供了各种机制，让您能够自定义页面创作功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 2%

---

# 自定义页面创作{#customizing-page-authoring}

>[!CAUTION]
>
>本文档介绍如何在启用了触屏的现代化UI中自定义页面创作，并且不适用于经典UI。

Adobe Experience Manager (AEM)提供了各种机制，让您能够自定义页面创作功能(以及 [控制台](/help/sites-developing/customizing-consoles-touch.md))。

* Clientlibs

  Clientlibs允许您扩展默认实施以实现新功能，同时重用标准函数、对象和方法。 进行自定义时，您可以在下创建自己的clientlib `/apps.` 新clientlib必须：

   * 取决于创作clientlib `cq.authoring.editor.sites.page`
   * 属于适当的 `cq.authoring.editor.sites.page.hook` 类别

* 叠加

  叠加基于节点定义，允许您叠加标准功能(在 `/libs`)中自行定制的功能(在 `/apps`)。 创建叠加时，不需要原始文件的1:1副本，因为 [sling资源合并器](/help/sites-developing/sling-resource-merger.md) 允许继承。

>[!NOTE]
>
>有关更多信息，请参阅 [JS文档集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

可通过多种方式使用这些组件来扩展AEM实例中的页面创作功能。 下面的内容介绍了所做的选择（概括）。

>[!NOTE]
>
>有关更多信息，请参阅以下内容：
>
>* 使用和创建 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和创建 [叠加](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md) 有关用于页面创作的结构区域的详细信息。
>


>[!CAUTION]
>
>***不要*** 更改 `/libs` 路径。
>
>原因在于 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 重新创建所需项目(即，它存在于 `/libs`)下 `/apps`
>1. 在中进行任何更改 `/apps`

## 添加新图层（模式） {#add-new-layer-mode}

在编辑页面时，有各种 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 可用。 这些模式通过以下方式实现 [图层](/help/sites-developing/touch-ui-structure.md#layer). 利用这些功能，可访问同一页面内容的不同功能类型。 标准层包括：编辑、预览、注释、开发人员和定位。

### 层示例：Live Copy状态 {#layer-example-live-copy-status}

标准AEM实例提供MSM层。 这将访问与以下项相关的数据： [多站点管理](/help/sites-administering/msm.md) 并在图层中将其加亮。

要查看其实际操作情况，您可以编辑任何 [We.Retail语言副本](/help/sites-developing/we-retail-globalized-site-structure.md) 页面（或任何其他live copy页面）并选择 **Live Copy状态** 模式。

可以在以下位置找到MSM层定义（供参考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例 {#code-sample}

这是一个示例包，显示如何创建层（模式），即MSM视图的新层。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-new-layer-mode项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 将新的选择类别添加到资源浏览器 {#add-new-selection-category-to-asset-browser}

资产浏览器显示各种类型/类别的资产（例如图像和文档）。 资源也可以按这些资源类别进行筛选。

### 代码示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，显示如何将组添加到资产查找器。 此示例连接到 [闪烁](https://www.flickr.com)的公开流，并将其显示在侧面板中。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-assetfinder-flickr项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 筛选资源 {#filtering-resources}

在创作页面时，用户通常必须从资源（例如，页面、组件和资产）中进行选择。 这可以采用列表形式，例如，作者必须从中选择一个项目。

要使列表保持合理的大小并符合用例，可以采用自定义谓词的形式实施过滤器。 例如，如果 [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) 组件用于允许用户选择特定资源的路径，提供的路径可通过以下方式过滤：

* 通过实施自定义谓词 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) 界面。
* 指定谓词的名称，并在使用 `pathbrowser`.

有关创建自定义谓词的更多详细信息，请参阅 [本文](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>通过实施实施自定义谓词 `com.day.cq.commons.predicate.AbstractNodePredicate` 界面在经典UI中也有效。
>
>参见 [此知识库文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 有关在经典UI中实施自定义谓词的示例。

## 将新操作添加到组件工具栏 {#add-new-action-to-a-component-toolbar}

每个组件（通常）都有一个工具栏，通过该工具栏可访问可对该组件执行的一系列操作。

### 代码示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，显示如何创建自定义工具栏操作以渲染组件。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-toolbar-screenshot项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 添加新的就地编辑器 {#add-new-in-place-editor}

### 标准就地编辑器 {#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   包含各种编辑器的可用定义。

1. 编辑器和每个可以使用它的资源类型（组件中一样）之间存在一个连接：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性: `editorType`

           定义为该组件触发就地编辑时使用的内联编辑器的类型；例如， `text`， `textimage`， `image`， `title`.

1. 可以使用配置编辑器的其他配置详细信息 `config` 包含配置和 `plugin` 节点以包含必要的插件配置详细信息。

   以下是为图像组件的图像裁剪插件定义长宽比的示例。 由于屏幕大小有限的可能性，裁切长宽比已移至全屏编辑器，并且只能在那里看到。

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
   >AEM裁切比率，由设置 `ratio` 属性，定义为 **高度/宽度**. 这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。只要您定义 `name` 属性清楚，因为这是UI中显示的内容。

#### 创建新的就地编辑器 {#creating-a-new-in-place-editor}

要实施新的就地编辑器（在clientlib中），请执行以下操作：

>[!NOTE]
>
>例如，请参阅：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）：

   * `editor.register`

1. 提供编辑器与可以使用该编辑器的每个资源类型（组件中）之间的连接。

#### 用于创建新的就地编辑器的代码示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，显示如何在AEM中创建就地编辑器。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-inplace-editor项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多个就地编辑器 {#configuring-multiple-in-place-editors}

可以配置组件，使其具有多个就地编辑器。 配置多个就地编辑器后，您可以选择相应的内容并打开相应的编辑器。 请参阅 [配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md) 文档，以了解更多信息。

## 添加新页面操作 {#add-a-new-page-action}

要向页面工具栏中添加新页面操作，例如 **返回站点** （控制台）操作。

### 代码示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，显示如何创建自定义标题栏操作以跳回站点控制台。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-header-backtosites项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自定义激活请求工作流 {#customizing-the-request-for-activation-workflow}

即装即用的工作流， **请求激活**：

* 当内容作者访问时，将自动显示在相应的菜单中 **没有** 适当的复制权限，但 **确实有** DAM用户和作者的成员资格。

* 否则，不会显示任何内容，因为复制权限已被删除。

要在此类激活中进行自定义行为，您可以叠加 **请求激活** 工作流：

1. In `/apps` 叠加 **站点** 向导：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >它本身会覆盖以下通用实例：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 更新 [工作流模型](/help/sites-developing/workflows-models.md) 以及所需的相关配置/脚本。
1. 删除的权限 [`replicate` 操作](/help/sites-administering/security.md#actions) 来自所有相关页面的所有适当用户；当任何用户尝试发布（或复制）页面时，将此工作流作为默认操作触发。
