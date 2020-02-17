---
title: 在AEM中使用Sling资源合并
seo-title: 在AEM中使用Sling资源合并
description: Sling Resource Merage（Sling资源合并）提供访问和合并资源的服务
seo-description: Sling Resource Merage（Sling资源合并）提供访问和合并资源的服务
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 在AEM中使用Sling资源合并{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Mergare提供访问和合并资源的服务。 它为以下两者提供差异（差异）机制：

* **[使用](/help/sites-developing/overlays.md)**已配置的搜索路径[的资源叠加](/help/sites-developing/overlays.md#configuring-the-search-paths)。

* **使用** 资源类型层次结构(通过属性`cq:dialog`)覆盖触屏优化UI()的组件对话框 `sling:resourceSuperType`。

通过Sling Resource Mergare，叠加／覆盖资源和／或属性与原始资源／属性合并：

* 自定义定义的内容的优先级高于原始定义的优先级(即它 *叠*&#x200B;加&#x200B;*或覆盖* )。

* 在必要时， [在自定义中定义的属性](#properties) ，指示如何使用从原始内容合并的内容。

>[!CAUTION]
>
>Sling Resource Merage及相关方法只能与 [Granite一起使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 这也意味着它仅适用于标准的触屏优化UI;尤其是，以这种方式定义的覆盖仅适用于组件的触屏启用对话框。
>
>其他区域（包括触屏支持组件或经典UI的其他方面）的叠加／覆盖涉及将相应的节点和结构从原始节点复制到定义自定义的位置。

### AEM目标 {#goals-for-aem}

在AEM中使用Sling Resource Merage的目标是：

* 确保未在中进行自定义更改 `/libs`。
* 减少复制的结构 `/libs`。

   使用Sling Resource Merage时，建议不要从中复制整个结构， `/libs` 因为这会导致在自定义中保留过多信息(通常 `/apps`)。 在以任何方式升级系统时，重复信息会不必要地增加出现问题的可能性。

>[!NOTE]
>
>覆盖不取决于搜索路径，它们使用属性 `sling:resourceSuperType` 建立连接。
>
>但是，覆盖通常在下定义 `/apps`，因为AEM的最佳实践是在下定义自定义 `/apps`;因为你不能改下去什么 `/libs`.

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



### 属性 {#properties}

资源合并提供以下属性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隐藏的属性或属性列表。

   通配符将隐 `*` 藏全部内容。

* `sling:hideResource` ( `Boolean`)

   指示资源是否应完全隐藏，包括其子项。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隐藏的子节点或子节点列表。 将保留节点的属性。

   通配符将隐 `*` 藏全部内容。

* `sling:orderBefore` ( `String`)

   包含当前节点应位于的前面的同级节点的名称。

这些属性影响叠加／覆盖(通常在中 `/libs`)使用相应／原始资源／属性的方 `/apps`式。

### 创建结构 {#creating-the-structure}

要创建叠加或覆盖，您需要在目标（通常）下重新创建具有等效结构的原始节 `/apps`点。 例如：

* 叠加

   * “站点”控制台的导航条目的定义，如边栏中所示，定义位于：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 要覆盖此节点，请创建以下节点：

      `/apps/cq/core/content/nav/sites`

      然后根据需要更 `jcr:title` 新属性。

* 覆盖

   * 文本控制台的触屏启用对话框的定义在以下位置进行定义：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆盖此项，请创建以下节点——例如：

      `/apps/the-project/components/text/cq:dialog`

要创建其中任何一个，您只需重新创建骨架结构。 为了简化结构的重建，所有中间节点都可以是类型 `nt:unstructured` 的(它们不必反映原始节点类型；例如，在 `/libs`中。

因此，在上述叠加示例中，需要以下节点：

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
>使用Sling资源合并（即，在处理标准的触屏优化UI时）时，不建议从中复制整个结构，因为这会导致 `/libs` 包含过多信息 `/apps`。 这在以任何方式升级系统时都可能导致问题。

### Use Cases {#use-cases}

这些功能与标准功能结合使用，使您能够：

* **添加属性**

   该属性在定义中不存 `/libs` 在，但在叠加／覆盖中 `/apps` 是必需的。

   1. 在 `/apps`
   1. 在此节点“”上创建新属性

* **重新定义属性（不是自动创建的属性）**

   该属性在中定 `/libs`义，但是叠加／覆盖中需要 `/apps` 一个新值。

   1. 在 `/apps`
   1. 在此节点上创建匹配属性(在／下 `apps`)

      * 该属性将具有基于Sling资源解析程序配置的优先级。
      * 支持更改属性类型。

         如果您使用的属性类型与中使用的属性类型不同， `/libs`则将使用您定义的属性类型。
   >[!NOTE]
   >
   >支持更改属性类型。

* **重新定义自动创建的属性**

   默认情况下，自动创建的属性(如 `jcr:primaryType`)不受叠加／覆盖的约束，以确保遵守当前在下的节点 `/libs` 类型。 要实施叠加／覆盖，您必须在中重新创建节点 `/apps`，请显式隐藏属性并重新定义它：

   1. 在下创建相应的节 `/apps` 点，并满足所需 `jcr:primaryType`
   1. 在该节 `sling:hideProperties` 点上创建属性，并将值设置为自动创建属性的值；例如， `jcr:primaryType`

      此属性(定义于 `/apps`)现在将优先于定义于 `/libs`

* **重新定义节点及其子节点**

   节点及其子项在中定义 `/libs`，但叠加／覆盖中需要新 `/apps` 的配置。

   1. 组合下列操作：

      1. 隐藏节点的子项（保留节点的属性）
      1. 重新定义属性／属性

* **隐藏属性**

   属性在中定义， `/libs`但在叠加／覆盖中 `/apps` 不是必需的。

   1. 在 `/apps`
   1. 创建或类 `sling:hideProperties` 型的 `String` 属性 `String[]`。 使用此选项可指定要隐藏／忽略的属性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子项**

   节点及其子项在中定义， `/libs`但在叠加／覆盖中 `/apps` 不是必需的。

   1. 在/apps下创建相应的节点
   1. 创建属性 `sling:hideResource`

      * 类型: `Boolean`
      * value: `true`

* **隐藏节点的子项（同时保留节点的属性）**

   节点、其属性及其子项在中定义 `/libs`。 叠加／覆盖中需要节点及其属 `/apps` 性，但叠加／覆盖中不需要部分或所有子节 `/apps` 点。

   1. 在 `/apps`
   1. 创建属性 `sling:hideChildren`:

      * 类型: `String[]`
      * value:要隐藏／忽略的子节点列表(如 `/libs`中定义)
      通配符&amp;ast;可用于隐藏／忽略所有子节点。


* **对节点重新排序**

   节点及其同级在中定义 `/libs`。 需要新位置，因此在叠加／覆盖中重新创建节点，其中新位置是在引用中相应的同级节点时定义的 `/apps``/libs`。

   * 使用属 `sling:orderBefore` 性：

      1. 在 `/apps`
      1. 创建属性 `sling:orderBefore`:

         这指定了当前节点应在以 `/libs`下位置之前放置的节点（如中所示）:

         * 类型: `String`
         * value: `<before-SiblingName>`

### 从代码中调用Sling资源合并 {#invoking-the-sling-resource-merger-from-your-code}

Sling资源合并包括两个自定义资源提供商——一个用于叠加，另一个用于覆盖。 可以通过使用装载点在您的代码中调用其中的每一个：

>[!NOTE]
>
>访问资源时，建议使用相应的装载点。
>
>这可确保调用Sling Resource Mergabile（合并）并返回完全合并的资源(减少需要从中复制的结构 `/libs`)。

* 叠加:

   * 目的：根据资源的搜索路径合并资源
   * 装载点： `/mnt/overlay`
   * usage: `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆盖：

   * 目的：根据超类型合并资源
   * 装载点： `/mnt/overide`
   * usage: `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用示例 {#example-of-usage}

下面介绍了一些示例：

* 叠加:

   * [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆盖：

   * [配置页面属性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

