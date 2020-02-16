---
title: 编辑者
seo-title: 编辑者
description: 了解如何切换回经典UI编辑器。
seo-description: 了解如何切换回经典UI编辑器。
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# 编辑者{#editor}

默认情况下，从编辑器切换到经典UI的功能已禁用。

要重新启用“页面信息” **菜单中的“在经典UI中打开** ” **选项，请执行以下步骤** 。

1. 使用CRXDE Lite，找到以下节点：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用“叠加节点” **选项创建叠加** ;例如：

   * **路径**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**:活动（选中复选框）

1. 将以下多值文本属性添加到叠加的节点：

   `sling:hideProperties = ["granite:hidden"]`

1. 编辑 **页面时，“页面信息”菜单中** ,“在经典UI中 **打开** ”选项再次可用。

   ![](assets/syui-03-2019-02-27-15-19-48.png)