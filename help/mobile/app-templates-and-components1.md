---
title: 应用程序模板和组件
seo-title: App Templates and Components
description: 关注此页面，了解应用程序模板和组件。 它提供有关模板结构的详细信息。
seo-description: Follow this page to learn about App Templates and Components. It provides detailed information on the structure of templates.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# 应用程序模板和组件{#app-templates-and-components}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

模板用于创建页面，并定义可以在所选范围内使用的组件。 模板是一种节点层次结构，其结构与要创建页面的结构相同，但没有任何实际内容。

每个模板都会为您提供一系列可供使用的组件。

* 模板由以下项构建： [组件](/help/sites-developing/components.md)；
* 组件使用和允许对构件的访问，构件和构件用于呈现内容。

>[!NOTE]
>
>要了解如何使用CRXDE Lite开发AEM应用程序，请参阅 [使用CRXDE Lite进行开发](/help/sites-developing/developing-with-crxde-lite.md).

模板是页面的基础。

要创建页面，必须复制模板（节点树） **/apps/&lt;myapp>/templates/&lt;mytemplate>**)中的相应位置：如果使用以下方式创建页面，则会发生这种情况 **网站** 选项卡。

此复制操作还会为页面提供其初始内容（通常为顶级内容）和属性sling：resourceType，用于呈现页面的页面组件的路径（子节点jcr：content中的所有内容）。

## 模板的结构 {#structure-of-a-template}

需要考虑两个方面：

* 模板本身的结构
* 使用模板时生成的内容的结构

在类型节点下创建模板 **cq：Template**.

可以设置各种属性，特别是：

* **jcr：title**  — 模板的标题；在创建页面时显示在对话框中。
* **jcr：description**  — 模板的描述；在创建页面时显示在对话框中。

此节点包含 *jcr：content (cq：PageContent)* 用作结果页面的内容节点基础的节点；此参考使用 *sling：resourceType*，用于呈现新页面的实际内容的组件。

>[!NOTE]
>
>要了解AEM中模板和组件的基础知识，请参阅以下资源：
>
>* [模板](/help/sites-developing/templates.md)
>* [组件](/help/sites-developing/components.md)
>

在基本了解模板和组件后，请参阅以下资源：

* [创建和添加模板和组件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳实践](/help/mobile/best-practices-aem-mobile.md)
* [开发AEM Mobile内容服务](/help/mobile/developing-content-services.md)

### 其他资源 {#additional-resources}

要了解有关移动应用程序的其他主题，请参阅以下链接：

* [通过内容同步移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [测试移动应用程序](/help/mobile/develop-mobile-apps-testing.md)
