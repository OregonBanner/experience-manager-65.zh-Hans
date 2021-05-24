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
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# Admin Console{#admin-consoles}

默认情况下，通过管理控制台切换到经典UI的功能已被禁用。 因此，将鼠标悬停在某些控制台图标上时显示的允许访问经典UI的弹出图标将不再显示。

每个在`/libs/cq/core/content/nav`中具有经典UI版本的控制台都可以单独重新启用，以便将鼠标悬停在控制台图标上时，再次弹出&#x200B;**经典UI**&#x200B;选项。

在此示例中，我们将为站点控制台重新启用经典UI。

1. 使用CRXDE Lite，找到与要为其重新启用经典UI的Admin Console对应的节点。 它们位于：

   `/libs/cq/core/content/nav`

   例如

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 选择与要为其重新启用经典UI的控制台对应的节点。 例如，我们将为站点控制台重新启用经典UI。

   `/libs/cq/core/content/nav/sites`

1. 使用&#x200B;**覆盖节点**&#x200B;选项创建覆盖；例如：

   * **路径**: `/apps/cq/core/content/nav/sites`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**:活动（选中复选框）

1. 将以下布尔属性添加到所覆盖的节点：

   `enableDesktopOnly = {Boolean}true`

1. **经典UI**&#x200B;选项在管理控制台中再次作为弹出窗口选项可用。

   ![](assets/syui-01-2019-02-27-15-16-55.png)

对要为其重新启用经典UI版本访问权限的每个控制台重复这些步骤。
