---
title: 应用程序模板和组件
seo-title: 应用程序模板和组件
description: 可查看本页以了解有关应用程序模板和组件的信息。 它提供了有关模板结构的详细信息。
seo-description: 可查看本页以了解有关应用程序模板和组件的信息。 它提供了有关模板结构的详细信息。
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---


# 应用程序模板和组件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

模板用于创建页面并定义可在所选范围内使用的组件。 模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。

每个模板都会为您提供一系列可用组件。

* 模板由[组件](/help/sites-developing/components.md)构建；
* 组件使用和允许访问构件，这些构件用于呈现内容。

>[!NOTE]
>
>要了解如何使用CRXDE Lite开发AEM应用程序，请参阅[使用CRXDE Lite开发](/help/sites-developing/developing-with-crxde-lite.md)。

模板是页面的基础。

要创建页面，必须将模板(node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**)复制到site-tree中的相应位置：这是使用&#x200B;**网站**&#x200B;选项卡创建页面时会发生的情况。

此复制操作还为页面提供其初始内容（通常仅限顶级内容）和属性sling:resourceType，用于呈现页面的页面组件的路径（子节点jcr:content中的所有内容）。

## 模板{#structure-of-a-template}的结构

需要考虑两个方面：

* 模板本身的结构
* 使用模板时生成的内容的结构

在类型&#x200B;**cq:Template**&#x200B;的节点下创建模板。

可以设置各种属性，特别是：

* **jcr:title** -模板的标题；创建页面时显示在对话框中。
* **jcr:description** -模板的描述；创建页面时显示在对话框中。

此节点包含&#x200B;*a jcr:content(cq:PageContent)*&#x200B;节点，该节点用作生成页面的内容节点的基础；此引用使用&#x200B;*sling:resourceType*，用于呈现新页面实际内容的组件。

>[!NOTE]
>
>要了解AEM中模板和组件的基础知识，请参阅以下资源：
>
>* [模板](/help/sites-developing/templates.md)
>* [组件](/help/sites-developing/components.md)

>



在您基本了解了模板和组件后，请参阅以下资源：

* [创建和添加模板和组件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳实践](/help/mobile/best-practices-aem-mobile.md)
* [开发AEM Mobile内容服务](//help/mobile/developing-content-services.md)

### 其他资源 {#additional-resources}

要了解有关移动应用程序的其他主题，请参阅以下链接：

* [内容同步的移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [测试移动应用程序](/help/mobile/develop-mobile-apps-testing.md)

