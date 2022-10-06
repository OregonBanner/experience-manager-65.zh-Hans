---
title: 叠加
seo-title: Overlays
description: AEM使用叠加原理来允许您扩展和自定义控制台及其他功能
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# 叠加{#overlays}

AEM（在此之前，CQ）一直使用叠加原则来扩展和自定义 [控制台](/help/sites-developing/customizing-consoles-touch.md) 和其他功能(例如， [页面创作](/help/sites-developing/customizing-page-authoring-touch.md))。

叠加图是一个可在许多上下文中使用的术语。 在此上下文中(扩展AEM)，叠加意味着采用预定义的功能，并将您自己的定义强加在该上下文中（以自定义标准功能）。

在标准实例中，预定义功能保留在 `/libs` 推荐在 `/apps` 分支。 AEM使用搜索路径查找资源，首先搜索 `/apps` 分支，然后 `/libs` 分支( [可以配置搜索路径](#configuring-the-search-paths))。 此机制意味着您的叠加（以及在此处定义的自定义）将具有优先级。

自AEM 6.0起，对叠加的实施和使用方式进行了更改：

* 从AEM 6.0开始 — 用于 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)与相关的叠加（即触屏优化UI）

   * 方法

      * 重建适当的 `/libs` 结构 `/apps`.

         这不需要1:1副本， [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 用于交叉引用所需的原始定义。 Sling资源合并器通过差异（差异）机制提供访问和合并资源的服务。

      * 在下进行任何更改 `/apps`.
   * 优点

      * 更强大地处理 `/libs`.
      * 只重新定义实际需要的内容。


* 在AEM 6.0之前的非Granite叠加和叠加

   * 方法

      * 从以下位置复制内容 `/libs` to `/apps`

         您需要复制整个子分支，包括属性。

      * 在下进行任何更改 `/apps`.
   * 缺点

      * 尽管当下的某些内容发生更改时，您所做的更改不会丢失 `/libs`，则可能必须在下面的叠加中重新创建某些更改 `/apps`.


>[!CAUTION]
>
>的 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 相关方法只能与 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 这意味着创建具有骨架结构的叠加图仅适用于标准触屏UI。
>
>其他区域（包括经典UI）的叠加涉及复制相应的节点和整个子结构，然后进行所需的更改。

对于许多更改(例如， [配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 或 [在侧面板中为资产浏览器创建选择类别](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) （在创作页面时使用）。 它们要求为：

* 您 ***必须* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能会丢失，因为当您执行以下操作时，此分支将容易发生更改：

   * 在您的实例中升级
   * 应用修补程序
   * 安装功能包

* 他们将您所做的更改集中在一个位置；更便于您根据需要跟踪、迁移、备份和/或调试更改。

## 配置搜索路径 {#configuring-the-search-paths}

对于叠加图，交付的资源是检索到的资源和属性的聚合，具体取决于可定义的搜索路径：

* 资源 **解析程序搜索路径** 如 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 对于 **Apache Sling Resource Resolver Factory**.

   * 搜索路径的自上而下的顺序表示其各自的优先级。
   * 在标准安装中，主要默认值为 `/apps`, `/libs`  — 因此， `/apps` 比 `/libs` (即 *叠加* )。

* 两个服务用户需要对存储脚本的位置进行JCR:READ访问。 这些用户包括：components-search-service(由com.day.cq.wcm.coreto访问/缓存组件使用)和sling-scripting（由org.apache.sling.servlets.resolver用来查找servlet）。
* 还必须根据脚本的放置位置（在本例中为/etc、/libs或/apps下）配置以下配置。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最后，还必须配置Servlet解析程序（在本示例中，还要添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用示例 {#example-of-usage}

下面介绍了一些示例：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)
