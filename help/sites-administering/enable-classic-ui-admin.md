---
title: Admin Console
seo-title: Admin Console
description: 了解如何使用AEM中提供的Admin Console。
seo-description: 了解如何使用AEM中提供的Admin Console。
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---


# Admin Console{#admin-consoles}

默认情况下，已禁用通过管理员控制台切换到经典UI的功能。 因此，将鼠标移过某些控制台图标时看到的弹出图标（允许访问经典UI）不再显示。

每个在`/libs/cq/core/content/nav`中具有经典UI版本的控制台都可以单独重新启用，这样，将鼠标移过控制台图标时，**经典UI**&#x200B;选项会再次弹出。

在此示例中，我们将重新为站点控制台启用经典UI。

1. 使用CRXDE Lite，找到要重新启用经典UI的管理控制台对应的节点。 它们位于：

   `/libs/cq/core/content/nav`

   例如

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 选择要重新启用经典UI的控制台对应的节点。 对于我们的示例，我们将重新启用“站点”控制台的经典UI。

   `/libs/cq/core/content/nav/sites`

1. 使用&#x200B;**叠加节点**&#x200B;选项创建叠加；例如：

   * **路径**: `/apps/cq/core/content/nav/sites`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**:活动（选中复选框）

1. 将以下布尔属性添加到叠加的节点：

   `enableDesktopOnly = {Boolean}true`

1. “**经典UI**”选项在管理控制台中再次作为弹出选项可用。

   ![](assets/syui-01-2019-02-27-15-16-55.png)

对要重新启用经典UI版本访问权限的每个控制台重复这些步骤。