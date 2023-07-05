---
title: 编辑器
seo-title: Editor
description: 了解如何切换回经典用户界面编辑器。
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: 1c89ac7c4740222a3f51abd677e0ce71a7004377
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 6%

---


# 编辑器{#editor}

默认情况下，已禁用从编辑器切换到经典UI的功能。

要重新启用该选项，请执行以下操作 **在经典用户界面中打开** 在 **页面信息** 菜单，请按照以下步骤操作。

1. 使用CRXDE Lite查找以下节点：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用创建叠加 **覆盖节点** 选项；例如：

   * **路径**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**：活动（选中复选框）

1. 将以下多值文本属性添加到叠加节点：

   `sling:hideProperties = ["granite:hidden"]`

1. 此 **在经典用户界面中打开** 选项在中再次可用 **页面信息** 菜单。

   ![在经典UI中打开页面信息中的选项](assets/syui-03-2019-02-27-15-19-48.png)
