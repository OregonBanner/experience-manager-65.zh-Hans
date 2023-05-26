---
title: 叠加
seo-title: Overlays
description: AEM使用叠加原理来允许您扩展和自定义控制台和其他功能
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

AEM（在那之前，CQ）一直使用叠加原理来允许您扩展和自定义 [控制台](/help/sites-developing/customizing-consoles-touch.md) 和其他功能(例如， [页面创作](/help/sites-developing/customizing-page-authoring-touch.md))。

“叠加”是一个可在许多上下文中使用的术语。 在此上下文中(扩展AEM)，叠加意味着采用预定义功能并将您自己的定义强加于此功能（以自定义标准功能）。

在标准实例中，预定义功能保存在 `/libs` 推荐做法是在下定义您的叠加（自定义） `/apps` 分支。 AEM使用搜索路径来查找资源，首先搜索 `/apps` 分支，然后 `/libs` 分支( [可以配置搜索路径](#configuring-the-search-paths))。 此机制意味着您的叠加（以及其中定义的自定义项）将具有优先级。

自AEM 6.0起，对叠加的实施和使用方式进行了更改：

* AEM 6.0及更高版本 — for [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相关叠加图（即触屏UI）

   * 方法

      * 重构适当的 `/libs` 下结构 `/apps`.

         这不需要一对一的拷贝， [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 用于交叉引用所需的原始定义。 Sling资源合并器提供通过差异（差异）机制访问和合并资源的服务。

      * 进行以下任何更改 `/apps`.
   * 优点

      * 对下的更改更强健 `/libs`.
      * 仅重新定义实际需要的内容。


* AEM 6.0之前的非Granite叠加图和叠加图

   * 方法

      * 复制内容来源 `/libs` 到 `/apps`

         您需要复制整个子分支，包括资产。

      * 进行以下任何更改 `/apps`.
   * 缺点

      * 尽管当下的某些内容发生更改时，您的更改不会丢失 `/libs`，您可能必须重新创建在下的叠加中发生的某些更改 `/apps`.


>[!CAUTION]
>
>此 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 并且相关方法只能用于 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 这意味着创建具有框架结构的叠加仅适用于支持触摸的标准用户界面。
>
>其他区域（包括经典UI）的叠加包括复制相应的节点和整个子结构，然后进行所需的更改。

叠加是进行许多更改的推荐方法，例如 [配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 或 [在侧面板中的资源浏览器中创建选择类别](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) （在创作页面时使用）。 要求它们是：

* 您 ***不得* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能会丢失，因为每当您：

   * 在您的实例上升级
   * 应用修补程序
   * 安装功能包

* 它们将您的更改集中在一个位置；使您更轻松地跟踪、迁移、备份和/或调试更改（如有必要）。

## 配置搜索路径 {#configuring-the-search-paths}

对于叠加图，交付的资源是检索到的资源和属性的汇总，具体取决于可以定义的搜索路径：

* 资源 **解析程序搜索路径** 如 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 对于 **Apache Sling资源解析程序工厂**.

   * 搜索路径的自上而下的顺序指示其各自的优先级。
   * 在标准安装中，主要缺省值为 `/apps`， `/libs`  — 因此， `/apps` 优先级高于 `/libs` （即它） *叠加* it)。

* 两个服务用户需要对存储脚本的位置具有JCR：READ访问权限。 这些用户是： components-search-service(由com.day.cq.wcm.coreto用于访问/缓存组件)和sling-scripting（由org.apache.sling.servlets.resolver用于查找servlet）。
* 还必须根据脚本放置的位置（本示例中位于/etc、/libs或/apps下）配置以下配置。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最后，还必须配置Servlet解析程序（在本例中还添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用示例 {#example-of-usage}

在以下情况下介绍了一些示例：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)
