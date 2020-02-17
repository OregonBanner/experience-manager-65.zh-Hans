---
title: 叠加
seo-title: 叠加
description: AEM使用叠加原则允许您扩展和自定义控制台和其他功能
seo-description: AEM使用叠加原则允许您扩展和自定义控制台和其他功能
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 叠加{#overlays}

AEM（在此之前，CQ）一直使用叠加原则来允许您扩展和自定义控制台和 [其他功能](/help/sites-developing/customizing-consoles-touch.md) (例如，页面 [创作](/help/sites-developing/customizing-page-authoring-touch.md))。

Overlay是可在许多上下文中使用的术语。 在此上下文（扩展AEM）中，叠加意味着采用预定义的功能并将您自己的定义强制应用于该功能（以自定义标准功能）。

在标准实例中，预定义的功能保留在 `/libs` 下，建议在分支下定义叠加（自定义） `/apps` 。 AEM使用搜索路径来查找资源，首先搜索分 `/apps` 支，然后搜索分 `/libs` 支(可 [以配置搜索路径](#configuring-the-search-paths))。 此机制意味着您的叠加（以及在此定义的自定义）将具有优先级。

自AEM 6.0起，对如何实施和使用叠加进行了更改：

* 从AEM 6.0开始——适用于 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-related叠加（即触屏优化UI）

   * 方法

      * 在下重建相 `/libs` 应的结构 `/apps`。

         这不需要1:1副本， [Sling Resource Mergare](/help/sites-developing/sling-resource-merger.md) （合并资源）用于交叉引用所需的原始定义。 Sling Resource Merager通过差异（差异）机制提供访问和合并资源的服务。

      * 在下进行任何更改 `/apps`。
   * 优势

      * 对下面的更改更加强大 `/libs`。
      * 只重新定义实际需要的内容。


* AEM 6.0之前的非Granite叠加和叠加

   * 方法

      * 将内容从复制到 `/libs``/apps`

         您需要复制整个子分支，包括属性。

      * 在下进行任何更改 `/apps`。
   * 缺点

      * 尽管您所做的更改在下面发生更改时不会丢失， `/libs`但您可能必须重新创建在下面叠加中发生的某些更改 `/apps`。


>[!CAUTION]
>
>Sling Resource Merage [(](/help/sites-developing/sling-resource-merger.md) Sling Resource Mergare [)及相关方法只能与](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Granite一起使用。 这意味着创建具有骨架结构的叠加仅适用于标准的触屏优化UI。
>
>其他区域（包括经典UI）的叠加包括复制相应的节点和整个子结构，然后进行所需的更改。

对于许多更改，建议使用叠加方法，例如 [配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) , [或在侧面板（创作页面时使用）中创建资产浏览器的选择类别](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) 。 它们要求：

* 您不 ***得在分支中&#x200B;*`/libs`**进行更改。您所做的任何更改都可能会丢失，因为只要您：

   * 实例升级
   * 应用修补程序
   * 安装功能包

* 他们将更改集中在一个位置；使您能根据需要更轻松地跟踪、迁移、备份和／或调试更改。

## 配置搜索路径 {#configuring-the-search-paths}

对于叠加，交付的资源是检索到的资源和属性的集合，具体取决于可定义的搜索路径：

* 资源 **解析程序搜索路径** (在 [Apache Sling Resource Resolver Factory的OSGi配置中定义)](/help/sites-deploying/configuring-osgi.md)****。

   * 搜索路径的自上而下的顺序指示其各自的优先级。
   * 在标准安装中，主要默 `/apps`认值是 `/libs` -因此， `/apps` 其内容的优先级高于 `/libs` (即它叠加 ** )。

* 两个服务用户需要对存储脚本的位置进行JCR:READ访问。 这些用户是：components-search-service(由com.day.cq.wcm.coreto访问／缓存组件使用)和sling-scripting（由org.apache.sling.servlets.resolver用于查找servlet）。
* 还必须根据您放置脚本的位置配置以下配置（在本例中，位于/etc、/libs或/apps下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最后，还必须配置Servlet解析程序（在本例中，还要添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用示例 {#example-of-usage}

下面介绍了一些示例：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)

