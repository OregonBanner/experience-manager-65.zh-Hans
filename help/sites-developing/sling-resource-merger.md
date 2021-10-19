---
title: 在AEM中使用Sling资源合并器
seo-title: Using the Sling Resource Merger in AEM
description: Sling资源合并器提供访问和合并资源的服务
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: c07fa148054b69b0da7bb402ef96a50d0895abfa
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# 在AEM中使用Sling资源合并器{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling资源合并器提供访问和合并资源的服务。 它为以下两者提供了差异（差异）机制：

* **[叠加](/help/sites-developing/overlays.md)** 资源使用情况 [配置的搜索路径](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **覆盖** 触屏UI的组件对话框(`cq:dialog`)，使用资源类型层次结构(通过属性 `sling:resourceSuperType`)。

通过Sling资源合并器，叠加/覆盖资源和/或属性将与原始资源/属性合并：

* 自定义定义的内容比原始定义的内容具有更高的优先级(即 *叠加* 或 *覆盖* )。

* 必要时， [属性](#properties) 在自定义中定义，指示如何使用从原始内容合并的内容。

>[!CAUTION]
>
>Sling资源合并器及相关方法只能与 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 这也意味着它仅适用于标准触屏UI;特别是，以这种方式定义的覆盖仅适用于组件的触屏对话框。
>
>其他区域（包括触屏组件或经典UI的其他方面）的叠加/覆盖涉及将相应的节点和结构从原始节点复制到定义自定义的位置。

### AEM目标 {#goals-for-aem}

在AEM中使用Sling资源合并器的目标是：

* 确保未在 `/libs`.
* 减少从 `/libs`.

   使用Sling资源合并器时，不建议从 `/libs` 因为这会导致在自定义中保留太多信息(通常 `/apps`)。 复制信息会不必要地增加系统以任何方式升级时出现问题的可能性。

>[!NOTE]
>
>覆盖不取决于搜索路径，它们使用属性 `sling:resourceSuperType` 建立连接。
>
>但是，覆盖通常在 `/apps`，因为AEM的最佳实践是在 `/apps`;这是因为您不能更改 `/libs`.

>[!CAUTION]
>
>您 ***必须*** 不会更改 `/libs` 路径。
>
>这是因为 `/libs` 在下次升级实例时被覆盖（当您应用修补程序或功能包时，可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 重新创建所需项目(即， `/libs`)下 `/apps`
>
>1. 在 `/apps`

>


### 属性 {#properties}

资源合并器提供以下属性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隐藏的属性或属性列表。

   通配符 `*` 全部隐藏。

* `sling:hideResource` ( `Boolean`)

   指示是否应完全隐藏资源，包括其子资源。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隐藏的子节点或子节点列表。 将维护节点的属性。

   通配符 `*` 全部隐藏。

* `sling:orderBefore` ( `String`)

   包含当前节点应位于前面的同级节点的名称。

这些属性会影响相应/原始资源/属性(从 `/libs`)由叠加/覆盖使用(通常在 `/apps`)。

### 创建结构 {#creating-the-structure}

要创建叠加或覆盖，您需要在目标(通常为 `/apps`)。 例如：

* 叠加

   * 站点控制台的导航条目的定义（如边栏中所示）在以下位置定义：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 要覆盖此节点，请创建以下节点：

      `/apps/cq/core/content/nav/sites`

      然后，更新资产 `jcr:title` 。

* 替代

   * 文本控制台的触屏启用对话框的定义在以下位置定义：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆盖此节点，请创建以下节点 — 例如：

      `/apps/the-project/components/text/cq:dialog`

要创建其中任一结构，您只需重新创建骨架结构。 为了简化结构的重构，所有中间节点都可以是类型 `nt:unstructured` (无需反映原节点类型；例如， `/libs`)。

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
>使用Sling资源合并器（即，处理标准触屏UI时）时，不建议从 `/libs` 因为这会导致信息被保存得太多 `/apps`. 这可能会在系统以任何方式升级时导致问题。

### 用例 {#use-cases}

这些功能与标准功能结合使用，使您能够：

* **添加资产**

   属性在 `/libs` 定义，但在 `/apps` 覆盖/覆盖。

   1. 在中创建相应的节点 `/apps`
   1. 在此节点“ ”上创建新属性

* **重定义属性（非自动创建的属性）**

   属性在 `/libs`，但需要在 `/apps` 覆盖/覆盖。

   1. 在中创建相应的节点 `/apps`
   1. 在此节点上创建匹配属性（在/下） `apps`)

      * 根据Sling资源解析程序配置，属性将具有优先级。
      * 支持更改属性类型。

         如果您使用的资产类型与 `/libs`，则将使用您定义的属性类型。
   >[!NOTE]
   >
   >支持更改属性类型。

* **重定义自动创建的属性**

   默认情况下，自动创建的属性(例如 `jcr:primaryType`)不受覆盖/覆盖的影响，以确保当前位于 `/libs` 受到尊重。 要实施叠加/覆盖，您必须在 `/apps`，则显式隐藏并重定义该属性：

   1. 在下创建相应的节点 `/apps` ，并且 `jcr:primaryType`
   1. 创建资产 `sling:hideProperties` 在该节点上，将值设置为自动创建属性的值；例如， `jcr:primaryType`

      此属性在下定义 `/apps`，将优先于 `/libs`

* **重新定义节点及其子节点**

   节点及其子项在 `/libs`，但需要在 `/apps` 覆盖/覆盖。

   1. 组合以下操作：

      1. 隐藏节点的子项（保留节点的属性）
      1. 重定义属性/属性

* **隐藏资产**

   属性在 `/libs`，但不是 `/apps` 覆盖/覆盖。

   1. 在中创建相应的节点 `/apps`
   1. 创建资产 `sling:hideProperties` 类型 `String` 或 `String[]`. 使用此选项可指定要隐藏/忽略的属性。 也可使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子节点**

   节点及其子项在 `/libs`，但不是 `/apps` 覆盖/覆盖。

   1. 在/apps下创建相应的节点
   1. 创建资产 `sling:hideResource`

      * 类型: `Boolean`
      * 选定: `true`

* **隐藏节点的子项（同时保留节点的属性）**

   节点、其属性及其子项在 `/libs`. 节点及其属性需要在 `/apps` 覆盖/覆盖，但是在 `/apps` 覆盖/覆盖。

   1. 在下创建相应的节点 `/apps`
   1. 创建资产 `sling:hideChildren`:

      * 类型: `String[]`
      * 值：子节点的列表(如 `/libs`)隐藏/忽略

      通配符&amp;ast;可用于隐藏/忽略所有子节点。


* **重新排序节点**

   节点及其同级在 `/libs`. 需要新位置，以便在 `/apps` 覆盖/覆盖，其中新位置在引用中的相应同级节点时定义 `/libs`.

   * 使用 `sling:orderBefore` 属性：

      1. 在下创建相应的节点 `/apps`
      1. 创建资产 `sling:orderBefore`:

         这会指定节点(如 `/libs`)当前节点应位于以下位置之前：

         * 类型: `String`
         * 选定: `<before-SiblingName>`

### 从代码中调用Sling资源合并器 {#invoking-the-sling-resource-merger-from-your-code}

Sling资源合并器包括两个自定义资源提供程序 — 一个用于叠加，另一个用于覆盖。 可以使用装载点在代码中调用以下每个值：

>[!NOTE]
>
>访问资源时，建议使用适当的装载点。
>
>这可确保调用Sling资源合并器并返回完全合并的资源（减少需要从中复制的结构） `/libs`)。

* 叠加:

   * 目的：根据资源的搜索路径合并资源
   * 装入点： `/mnt/overlay`
   * 用法： `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 替代:

   * 目的：根据其超类型合并资源
   * 装入点： `/mnt/overide`
   * 用法： `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用示例 {#example-of-usage}

下面介绍了一些示例：

* 叠加:

   * [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

* 替代:

   * [配置页面属性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
