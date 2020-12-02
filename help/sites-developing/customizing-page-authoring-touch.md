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
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---


# 自定义页面创作{#customizing-page-authoring}

>[!CAUTION]
>
>本文档介绍如何在现代化的触屏优化UI中自定义页面创作，但不适用于经典UI。

AEM提供了各种机制，使您能够自定义创作实例的页面创作功能（和[consoles](/help/sites-developing/customizing-consoles-touch.md)）。

* Clientlibs

   Clientlibs允许您扩展默认实现以实现新功能，同时重用标准函数、对象和方法。 自定义时，您可以在`/apps.`下创建自己的clientlib。新的clientlib必须：

   * 取决于创作clientlib `cq.authoring.editor.sites.page`
   * 是相应`cq.authoring.editor.sites.page.hook`类别的一部分

* 叠加

   叠加基于节点定义，允许您将标准功能（在`/libs`中）与您自己的自定义功能（在`/apps`中）进行叠加。 创建叠加时，不需要原始资源的1:1副本，因为[sling资源合并](/help/sites-developing/sling-resource-merger.md)允许继承。

>[!NOTE]
>
>有关详细信息，请参阅[JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。

这些功能可以通过多种方式在AEM实例中扩展页面创作功能。 下面介绍了一个选项（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用并创建[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和创建[叠加](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM触屏优化UI的结](/help/sites-developing/touch-ui-structure.md) 构，以了解用于页面创作的结构区域的详细信息。

>
>
[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)会话- [AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html)用户界面自定义中也介绍了本主题。

>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>建议的配置和其他更改方法是：
>
>1. 在`/apps`下重新创建所需项（即，它存在于`/libs`中）
>1. 在`/apps`中进行任何更改


## 添加新层（模式）{#add-new-layer-mode}

编辑页面时，有各种[模式](/help/sites-authoring/author-environment-tools.md#page-modes)可用。 这些模式是使用[层](/help/sites-developing/touch-ui-structure.md#layer)实现的。 这些功能允许对同一页面内容访问不同类型的功能。 标准层有：编辑、预览、批注、开发人员和定位。

### 图层示例：Live Copy状态{#layer-example-live-copy-status}

标准AEM实例提供MSM层。 这访问与[多站点管理](/help/sites-administering/msm.md)相关的数据，并在层中加亮显示它。

要查看其实际操作情况，您可以编辑任何[We.Retail语言副本](/help/sites-developing/we-retail-globalized-site-structure.md)页面（或任何其他Live Copy页面），然后选择&#x200B;**Live Copy状态**&#x200B;模式。

可在以下位置找到MSM层定义（供参考）:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例{#code-sample}

这是一个示例包，它显示如何创建新层（模式），这是MSM视图的新层。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-new-layer-mode项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 向资产浏览器{#add-new-selection-category-to-asset-browser}添加新的选择类别

资产浏览器显示各种类型/类别(如图像、文档等)的资产。 资产也可以按这些资产类别进行筛选。

### 代码示例{#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，它显示如何向资产查找器添加新组。此示例连接到[Flickr](https://www.flickr.com)的公共流并在侧面板中显示它们。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-assetfinder-flickr项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 筛选资源{#filtering-resources}

创作页面时，用户通常必须从资源（例如页面、组件、资产等）中进行选择。 这可以采用列表的形式，例如，作者必须从中选择项目。

为了使列表保持为合理的大小并且与用例相关，可以以自定义谓词的形式实现过滤器。 例如，如果使用[`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui)组件允许用户选择特定资源的路径，则可以按以下方式过滤显示的路径：

* 通过实现[`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html)接口实现自定义谓词。
* 指定谓词的名称，并在使用`pathbrowser`时引用该名称。

有关创建自定义谓词的详细信息，请参阅[此文章](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>通过实现`com.day.cq.commons.predicate.AbstractNodePredicate`接口实现自定义谓词也适用于经典UI。
>
>有关在经典UI中实现自定义谓词的示例，请参阅[此知识库文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html)。

## 将新操作添加到组件工具栏{#add-new-action-to-a-component-toolbar}

每个组件（通常）都有一个工具栏，它提供对可对该组件执行的一系列操作的访问。

### 代码示例{#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，它显示如何创建自定义工具栏操作来渲染组件。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-toolbar-screestop项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 添加新的就地编辑器{#add-new-in-place-editor}

### 标准就地编辑器{#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   包含各种可用编辑器的定义。

1. 编辑器与每个资源类型（如组件中）之间有连接，可以使用它：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性: `editorType`

            定义在为该组件触发就地编辑时将使用的内联编辑器类型；例如，`text`、`textimage`、`image`、`title`。

1. 可以使用包含配置的`config`节点以及另一个`plugin`节点配置编辑器的其他配置详细信息，以包含必要的插件配置详细信息。

   以下是为图像组件的图像裁剪插件定义长宽比的示例。 请注意，由于屏幕大小可能非常有限，因此裁剪截图比率会移至全屏编辑器，并且只能在此处查看。

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
   >请注意，在AEM裁剪比率中，如`ratio`属性所设置，定义为&#x200B;**height/width**。 这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。如果您明确定义`name`属性，创作用户将不会发现任何差异，因为这是UI中显示的内容。

#### 创建新的就地编辑器{#creating-a-new-in-place-editor}

要实施新的就地编辑器（在clientlib中）:

>[!NOTE]
>
>例如，请参阅：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）:

   * `editor.register`

1. 提供编辑器与可使用它的每个资源类型（如组件中）之间的连接。

#### 创建新就地编辑器的代码示例{#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，它显示如何在AEM中创建新的就地编辑器。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-inplace-editor项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多个就地编辑器{#configuring-multiple-in-place-editors}

可以配置组件，使其具有多个就地编辑器。 配置多个就地编辑器后，您可以选择适当的内容并打开相应的编辑器。 有关详细信息，请参阅[配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md)文档。

## 添加新页面操作{#add-a-new-page-action}

要向页面工具栏添加新的页面操作，例如&#x200B;**返回站点**（控制台）操作。

### 代码示例{#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，它显示如何创建自定义标题栏操作以跳回站点控制台。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-extension-header-backtosites项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自定义激活工作流请求{#customizing-the-request-for-activation-workflow}

当内容作者没有适当的复制权限时，系统会自动触发现成的工作流&#x200B;**激活请求**。

要在此类激活上具有自定义行为，您可以叠加&#x200B;**激活请求**&#x200B;工作流：

1. 在`/apps`叠加中，**站点**&#x200B;向导：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >它本身将覆盖以下示例的通用实例：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 根据需要更新[工作流模型](/help/sites-developing/workflows-models.md)和相关配置／脚本。
1. 从所有相关页面的所有适当用户中删除[ `replicate`操作](/help/sites-administering/security.md#actions)的权限；以在任何用户尝试发布（或复制）页面时，将此工作流作为默认操作触发。

