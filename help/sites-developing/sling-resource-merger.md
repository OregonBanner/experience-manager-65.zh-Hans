---
title: AEM中Sling资源合并的应用
seo-title: AEM中Sling资源合并的应用
description: Sling Resource Merager提供访问和合并资源的服务
seo-description: Sling Resource Merager提供访问和合并资源的服务
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 1%

---


# 在AEM{#using-the-sling-resource-merger-in-aem}中使用Sling资源合并

## 用途 {#purpose}

Sling Resource Merager提供访问和合并资源的服务。 它为以下两者提供差异（差异）机制：

* **[使](/help/sites-developing/overlays.md)** 用配置的搜索路 [径覆盖资源](/help/sites-developing/overlays.md#configuring-the-search-paths)。

* **使** 用资源类型层次结构(通`cq:dialog`过属性)覆盖触屏优化UI的组件对话框 `sling:resourceSuperType`。

在Sling Resource Merabire中，叠加／覆盖资源和／或属性与原始资源／属性合并：

* 自定义定义的内容具有比原始定义更高的优先级（即，它&#x200B;*叠加*&#x200B;或&#x200B;*覆盖*&#x200B;它）。

* 在必要时，在自定义中定义[属性](#properties)，指示如何使用与原始内容合并的内容。

>[!CAUTION]
>
>Sling Resource Merage及相关方法只能与[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)一起使用。 这也意味着它仅适用于标准的触屏优化UI;尤其是，以这种方式定义的重写仅适用于组件的触屏启用对话框。
>
>其他区域（包括触屏优化组件或经典UI的其他方面）的叠加／覆盖涉及将相应的节点和结构从原始节点复制到定义自定义的位置。

### AEM {#goals-for-aem}的目标

在AEM中使用Sling Resource合并的目标是：

* 确保未在`/libs`中进行自定义更改。
* 减少从`/libs`复制的结构。

   使用Sling Resource Merage时，不建议从`/libs`复制整个结构，因为这会导致在自定义中保留过多信息（通常为`/apps`）。 在以任何方式升级系统时，重复信息会不必要地增加出现问题的可能性。

>[!NOTE]
>
>覆盖不取决于搜索路径，它们使用属性`sling:resourceSuperType`建立连接。
>
>但是，覆盖通常在`/apps`下定义，因为AEM的最佳实践是在`/apps`下定义自定义；这是因为您不得更改`/libs`下的任何内容。

>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>建议的配置和其他更改方法是：
>
>1. 在`/apps`下重新创建所需项（即，它存在于`/libs`中）
   >
   >
1. 在`/apps`中进行任何更改

>



### 属性 {#properties}

资源合并提供以下属性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隐藏的属性或属性列表。

   通配符`*`将隐藏全部。

* `sling:hideResource` ( `Boolean`)

   指示资源是否应完全隐藏，包括其子项。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隐藏的子节点或子节点的列表。 将保留节点的属性。

   通配符`*`将隐藏全部。

* `sling:orderBefore` ( `String`)

   包含当前节点应位于的前面的同级节点的名称。

这些属性影响叠加／覆盖（通常在`/apps`中）使用相应／原始资源／属性（来自`/libs`）的方式。

### 创建结构{#creating-the-structure}

要创建叠加或覆盖，您需要在目标（通常为`/apps`）下重新创建具有等效结构的原始节点。 例如：

* 叠加

   * 如边栏中所示，“站点”控制台的导航条目定义在以下位置：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 要覆盖此节点，请创建以下节点：

      `/apps/cq/core/content/nav/sites`

      然后根据需要更新属性`jcr:title`。

* 覆盖

   * 文本控制台的触屏启用对话框的定义在以下位置进行定义：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆盖此节点，请创建以下节点——例如：

      `/apps/the-project/components/text/cq:dialog`

要创建其中任何一个，您只需重新创建骨架结构。 为了简化结构的重建，所有中间节点可以是`nt:unstructured`类型(它们不必反映原始节点类型；例如，在`/libs`中。

因此，在上面的叠加示例中，需要以下节点：

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>使用Sling资源合并（即处理标准的触屏优化UI时）时，不建议从`/libs`复制整个结构，因为这会导致在`/apps`中保留过多信息。 这可能在系统以任何方式升级时导致问题。

### 用例{#use-cases}

这些功能与标准功能相结合，使您能够：

* **添加属性**

   该属性在`/libs`定义中不存在，但在`/apps`叠加／覆盖中是必需的。

   1. 在`/apps`中创建相应的节点
   1. 在此节点“”上创建新属性

* **重定义属性（非自动创建的属性）**

   属性在`/libs`中定义，但在`/apps`叠加／覆盖中需要一个新值。

   1. 在`/apps`中创建相应的节点
   1. 在此节点上创建匹配属性（在/ `apps`下）

      * 该属性将基于Sling资源解析程序配置具有优先级。
      * 支持更改属性类型。

         如果使用的属性类型与`/libs`中使用的属性类型不同，则将使用您定义的属性类型。
   >[!NOTE]
   >
   >支持更改属性类型。

* **重新定义自动创建的属性**

   默认情况下，自动创建的属性（如`jcr:primaryType`）不受叠加／覆盖的约束，以确保当前位于`/libs`下的节点类型受到尊重。 要实施叠加／覆盖，您必须在`/apps`中重新创建节点，显式隐藏该属性并重新定义它：

   1. 使用所需的`jcr:primaryType`在`/apps`下创建相应的节点
   1. 在该节点上创建属性`sling:hideProperties`，并将值设置为自动创建属性的属性；例如`jcr:primaryType`

      此属性（定义在`/apps`下）现在优先于在`/libs`下定义的属性

* **重新定义节点及其子节点**

   节点及其子项在`/libs`中定义，但在`/apps`叠加／覆盖中需要新配置。

   1. 组合下列操作：

      1. 隐藏节点的子项（保留节点的属性）
      1. 重定义属性／属性

* **隐藏属性**

   属性在`/libs`中定义，但在`/apps`叠加／覆盖中则不需要。

   1. 在`/apps`中创建相应的节点
   1. 创建`String`或`String[]`类型的`sling:hideProperties`属性。 使用它指定要隐藏／忽略的属性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子节点**

   节点及其子项在`/libs`中定义，但在`/apps`叠加／覆盖中则不是必需的。

   1. 在/apps下创建相应节点
   1. 创建属性`sling:hideResource`

      * 类型: `Boolean`
      * value: `true`

* **隐藏节点的子项（同时保留节点的属性）**

   节点、其属性及其子项在`/libs`中定义。 在`/apps`叠加／覆盖中，节点及其属性是必需的，但在`/apps`叠加／覆盖中，部分或所有子节点不是必需的。

   1. 在`/apps`下创建相应的节点
   1. 创建属性`sling:hideChildren`:

      * 类型: `String[]`
      * value:要隐藏／忽略的子节点列表（如`/libs`中定义）

      通配符&amp;ast;可用于隐藏／忽略所有子节点。


* **对节点重新排序**

   节点及其同级在`/libs`中定义。 需要新位置，因此在`/apps`叠加／覆盖中重新创建节点，其中新位置在引用`/libs`中的相应同级节点时定义。

   * 使用`sling:orderBefore`属性：

      1. 在`/apps`下创建相应的节点
      1. 创建属性`sling:orderBefore`:

         这指定了当前节点应该位于以下位置之前的节点（如`/libs`中所示）:

         * 类型: `String`
         * value:`<before-SiblingName>`

### 从代码{#invoking-the-sling-resource-merger-from-your-code}调用Sling资源合并

Sling Resource Merager包括两个自定义资源提供商——一个用于叠加，另一个用于覆盖。 可以通过使用装载点在代码中调用其中的每一个：

>[!NOTE]
>
>访问资源时，建议使用相应的装载点。
>
>这可确保调用Sling资源合并并返回完全合并的资源（减少需要从`/libs`复制的结构）。

* 叠加:

   * 目的：根据资源的搜索路径合并资源
   * 装载点：`/mnt/overlay`
   * 用法：`mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆盖：

   * 目的：根据超类型合并资源
   * 装载点：`/mnt/overide`
   * 用法：`mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 用法示例{#example-of-usage}

介绍了一些示例：

* 叠加:

   * [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆盖：

   * [配置页面属性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

