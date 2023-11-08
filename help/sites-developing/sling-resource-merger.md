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
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 1%

---

# 在AEM中使用Sling资源合并器{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling资源合并器提供访问和合并资源的服务。 它提供了以下两种情况的差异（差异）机制：

* **[叠加](/help/sites-developing/overlays.md)** 资源，使用 [已配置的搜索路径](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **覆盖** 触屏UI的组件对话框数量(`cq:dialog`)，使用资源类型层次结构(通过属性 `sling:resourceSuperType`)。

通过Sling资源合并器，覆盖/覆盖资源和/或属性与原始资源/属性合并：

* 自定义定义的内容具有比原始定义的内容更高的优先级(即 *叠加* 或 *覆盖* 它)。

* 必要时， [属性](#properties) 在自定义设置中定义，指示如何使用从原始内容中合并的内容。

>[!CAUTION]
>
>Sling资源合并器及相关方法只能用于 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 这也意味着它仅适用于标准的触屏优化UI；尤其是以这种方式定义的覆盖仅适用于组件的触屏优化对话框。
>
>其他区域（包括触屏组件或经典UI的其他方面）的覆盖/覆盖涉及将相应节点和结构从原始复制到将定义自定义的位置。

### AEM目标 {#goals-for-aem}

在AEM中使用Sling资源合并器的目标如下：

* 确保在中未进行自定义更改 `/libs`.
* 减少从复制的结构 `/libs`.

  在使用Sling资源合并器时，不建议从复制整个结构 `/libs` 因为这会导致（通常）在自定义设置中保留过多信息 `/apps`)。 在系统以某种方式升级时，不必要地复制信息会增加出现问题的机会。

>[!NOTE]
>
>覆盖不依赖于搜索路径，而是使用属性 `sling:resourceSuperType` 建立连接。
>
>但是，覆盖通常在下定义 `/apps`，因为AEM中的最佳实践是在以下位置定义自定义项 `/apps`；这是因为您不得更改下的任何内容 `/libs`.

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

### 属性 {#properties}

资源合并器提供以下属性：

* `sling:hideProperties` ( `String` 或 `String[]`)

  指定要隐藏的属性或属性列表。

  通配符 `*` 隐藏所有。

* `sling:hideResource` ( `Boolean`)

  指示是否应完全隐藏资源，包括其子资源。

* `sling:hideChildren` ( `String` 或 `String[]`)

  包含要隐藏的子节点或子节点列表。 将维护节点的属性。

  通配符 `*` 隐藏所有。

* `sling:orderBefore` ( `String`)

  包含当前节点应位于其前面的同级节点的名称。

这些属性会影响相应/原始资源/属性(来自 `/libs`)由覆盖/覆盖使用(通常在 `/apps`)。

### 创建结构 {#creating-the-structure}

要创建覆盖或覆盖，您需要在目标下重新创建具有同等结构的原始节点(通常 `/apps`)。 例如：

* 叠加

   * 站点控制台的导航条目（如边栏中所示）的定义定义定义位于：

     `/libs/cq/core/content/nav/sites/jcr:title`

   * 要叠加此节点，请创建以下节点：

     `/apps/cq/core/content/nav/sites`

     然后更新属性 `jcr:title` 根据需要。

* 替代

   * 为文本控制台定义启用了触屏的对话框的定义位于：

     `/libs/foundation/components/text/cq:dialog`

   * 要覆盖此节点，请创建以下节点 — 例如：

     `/apps/the-project/components/text/cq:dialog`

要创建其中任何一个，您只需重新创建骨架结构。 要简化结构的重新创建，所有中间节点都可以是 `nt:unstructured` (它们不必反映原始节点类型；例如，在 `/libs`)。

因此，在上述覆盖示例中，需要以下节点：

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
>在使用Sling资源合并器（即，处理标准的触屏UI时）时，不建议从复制整个结构 `/libs` 因为这会导致太多信息被保存在 `/apps`. 以任何方式升级系统时，这都可能导致问题。

### 用例 {#use-cases}

这些功能与标准功能相结合，使您能够：

* **添加属性**

  中不存在该属性 `/libs` 定义，但在以下项中是必需的： `/apps` 覆盖/覆盖。

   1. 在中创建对应的节点 `/apps`
   1. 在此节点上创建新属性»

* **重新定义属性（不是自动创建的属性）**

  属性在中定义 `/libs`，但中需要新值 `/apps` 覆盖/覆盖。

   1. 在中创建对应的节点 `/apps`
   1. 在此节点上创建匹配属性（在/下） `apps`)

      * 该资产的优先级将基于Sling资源解析程序配置。
      * 支持更改属性类型。

        如果您使用的属性类型与中使用的属性类型不同， `/libs`，然后会使用您定义的属性类型。

  >[!NOTE]
  >
  >支持更改属性类型。

* **重新定义自动创建的属性**

  默认情况下，自动创建的属性(例如 `jcr:primaryType`)不受覆盖/覆盖约束，以确保当前所在的节点类型 `/libs` 受到尊重。 要实施覆盖/覆盖，您必须在中重新创建节点 `/apps`，显式隐藏属性并重新定义它：

   1. 在下创建对应的节点 `/apps` 具有所需的 `jcr:primaryType`
   1. 创建资产 `sling:hideProperties` ，且值设置为自动创建属性的值；例如， `jcr:primaryType`

      此属性，在下定义 `/apps`，优先级现在高于下定义的那个 `/libs`

* **重新定义节点及其子节点**

  节点及其子节点定义于 `/libs`，但在中需要新配置 `/apps` 覆盖/覆盖。

   1. 合并以下各项的操作：

      1. 隐藏节点的子节点（保留节点的属性）
      1. 重新定义属性/属性

* **隐藏资产**

  属性在中定义 `/libs`，但不必在 `/apps` 覆盖/覆盖。

   1. 在中创建对应的节点 `/apps`
   1. 创建资产 `sling:hideProperties` 类型 `String` 或 `String[]`. 使用此选项可指定要隐藏/忽略的属性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隐藏节点及其子节点**

  节点及其子节点定义于 `/libs`，但不必在 `/apps` 覆盖/覆盖。

   1. 在/apps下创建对应的节点
   1. 创建资产 `sling:hideResource`

      * 类型: `Boolean`
      * 值: `true`

* **隐藏节点的子节点（同时保留节点的属性）**

  节点、其属性及其子节点定义于 `/libs`. 节点及其属性需要在 `/apps` 覆盖/覆盖，但中不需要部分或全部子节点 `/apps` 覆盖/覆盖。

   1. 在下创建对应的节点 `/apps`
   1. 创建资产 `sling:hideChildren`：

      * 类型: `String[]`
      * 值：子节点的列表（如中所定义） `/libs`)以隐藏/忽略

      通配符&amp;ast；可用于隐藏/忽略所有子节点。

* **重新排序节点**

  节点及其同级在中定义 `/libs`. 需要新位置，以便在中重新创建节点 `/apps` 覆盖/覆盖，其中新位置是参考中相应的同级节点定义的 `/libs`.

   * 使用 `sling:orderBefore` 属性：

      1. 在下创建对应的节点 `/apps`
      1. 创建资产 `sling:orderBefore`：

         这会指定节点(如 `/libs`)，当前节点应位于以下位置之前：

         * 类型: `String`
         * 值: `<before-SiblingName>`

### 从您的代码调用Sling资源合并器 {#invoking-the-sling-resource-merger-from-your-code}

Sling资源合并器包含两个自定义资源提供程序 — 一个用于叠加，另一个用于覆盖。 您可以使用挂载点在代码中调用其中的每项：

>[!NOTE]
>
>在访问资源时，建议使用适当的挂载点。
>
>这可确保调用Sling资源合并器并返回完全合并的资源（减少需要复制的结构） `/libs`)。

* 叠加:

   * 用途：根据资源的搜索路径合并资源
   * 装入点： `/mnt/overlay`
   * 用法： `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 替代:

   * 用途：根据资源的超级类型合并资源
   * 装入点： `/mnt/overide`
   * 用法： `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用示例 {#example-of-usage}

下面介绍一些示例：

* 叠加:

   * [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

* 替代:

   * [配置页面属性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
