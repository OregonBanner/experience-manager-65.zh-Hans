---
title: Admin Console
description: 了解如何使用AEM中提供的Admin Console。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# Admin Console{#admin-consoles}

默认情况下，通过管理控制台切换到经典UI的功能已被禁用。 因此，将鼠标悬停在特定控制台图标上时看到的弹出图标将不再显示，这些图标允许访问经典UI。

中每个具有经典UI版本的控制台 `/libs/cq/core/content/nav` 可以单独重新启用，以便 **经典Ui** 将选项悬停在控制台图标上时，该选项会再次弹出。

在本例中，我们将为站点控制台重新启用经典UI。

1. 使用CRXDE Lite，查找与要为其重新启用Classic UI的Admin Console对应的节点。 它们位于以下位置：

   `/libs/cq/core/content/nav`

   例如

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 选择与要为其重新启用经典UI的控制台对应的节点。 例如，我们将为站点控制台重新启用经典UI。

   `/libs/cq/core/content/nav/sites`

1. 使用创建叠加 **覆盖节点** 选项；例如：

   * **路径**: `/apps/cq/core/content/nav/sites`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**：活动（选中复选框）

1. 将以下布尔属性添加到叠加节点：

   `enableDesktopOnly = {Boolean}true`

1. 此 **经典Ui** 选项再次作为Admin Console中的弹出窗口选项提供。

   ![经典UI弹出窗口选项](assets/syui-01-2019-02-27-15-16-55.png)

对要为其重新启用对经典UI版本的访问权限的每个控制台重复这些步骤。
