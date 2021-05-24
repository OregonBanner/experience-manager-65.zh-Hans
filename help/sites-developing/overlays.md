---
title: 叠加
seo-title: 叠加
description: AEM使用叠加原理来允许您扩展和自定义控制台及其他功能
seo-description: AEM使用叠加原理来允许您扩展和自定义控制台及其他功能
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 叠加{#overlays}

AEM（在此之前，CQ）一直使用叠加原则来扩展和自定义[控制台](/help/sites-developing/customizing-consoles-touch.md)和其他功能（例如，[页面创作](/help/sites-developing/customizing-page-authoring-touch.md)）。

叠加图是一个可在许多上下文中使用的术语。 在此上下文中(扩展AEM)，叠加意味着采用预定义的功能，并将您自己的定义强加在该上下文中（以自定义标准功能）。

在标准实例中，预定义功能保留在`/libs`下，建议在`/apps`分支下定义叠加（自定义）。 AEM使用搜索路径来查找资源，首先搜索`/apps`分支，然后搜索`/libs`分支（[搜索路径可以配置](#configuring-the-search-paths)）。 此机制意味着您的叠加（以及在此处定义的自定义）将具有优先级。

自AEM 6.0起，对叠加的实施和使用方式进行了更改：

* 从AEM 6.0开始 — 适用于[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相关的叠加（即触屏优化UI）

   * 方法

      * 在`/apps`下重建相应的`/libs`结构。

         这不需要1:1副本，[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)用于交叉引用所需的原始定义。 Sling资源合并器通过差异（差异）机制提供访问和合并资源的服务。

      * 在`/apps`下进行任何更改。
   * 优势

      * 对`/libs`下的更改更加稳健。
      * 只重新定义实际需要的内容。


* 在AEM 6.0之前的非Granite叠加和叠加

   * 方法

      * 将内容从`/libs`复制到`/apps`

         您需要复制整个子分支，包括属性。

      * 在`/apps`下进行任何更改。
   * 缺点

      * 虽然在`/libs`下发生某些更改时，您所做的更改不会丢失，但您可能必须重新创建在`/apps`下叠加中发生的某些更改。


>[!CAUTION]
>
>[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)及相关方法只能与[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)一起使用。 这意味着创建具有骨架结构的叠加图仅适用于标准触屏UI。
>
>其他区域（包括经典UI）的叠加涉及复制相应的节点和整个子结构，然后进行所需的更改。

叠加是进行许多更改的推荐方法，例如[配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)或[在侧面板](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)中为资产浏览器创建选择类别（在创作页面时使用）。 它们要求为：

* ***不得*&#x200B;在`/libs`分支&#x200B;**中进行更改
您所做的任何更改都可能会丢失，因为当您执行以下操作时，此分支将容易发生更改：

   * 在您的实例中升级
   * 应用修补程序
   * 安装功能包

* 他们将您所做的更改集中在一个位置；更便于您根据需要跟踪、迁移、备份和/或调试更改。

## 配置搜索路径{#configuring-the-search-paths}

对于叠加图，交付的资源是检索到的资源和属性的聚合，具体取决于可定义的搜索路径：

* 资源&#x200B;**解析程序搜索路径**，在&#x200B;**Apache Sling资源解析程序工厂**&#x200B;的[OSGi配置](/help/sites-deploying/configuring-osgi.md)中定义。

   * 搜索路径的自上而下的顺序表示其各自的优先级。
   * 在标准安装中，主要默认值为`/apps`、`/libs` — 因此，`/apps`的内容具有比`/libs`更高的优先级（即&#x200B;*叠加*）。

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

## 用法示例{#example-of-usage}

下面介绍了一些示例：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md)
