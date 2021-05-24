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
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---

# 编辑者{#editor}

默认情况下，从编辑器切换到经典UI的功能已被禁用。

要在&#x200B;**页面信息**&#x200B;菜单中重新启用在经典UI **中打开选项**，请执行以下步骤。

1. 使用CRXDE Lite，找到以下节点：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用&#x200B;**覆盖节点**&#x200B;选项创建覆盖；例如：

   * **路径**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆盖位置**: `/apps/`
   * **匹配节点类型**:活动（选中复选框）

1. 将以下多值文本属性添加到叠加的节点：

   `sling:hideProperties = ["granite:hidden"]`

1. 编辑页面时， **在经典UI中打开**&#x200B;选项在&#x200B;**页面信息**&#x200B;菜单中再次可用。

   ![](assets/syui-03-2019-02-27-15-19-48.png)
