---
title: 编辑器
seo-title: Editor
description: 瞭解如何切換回傳統使用者介面編輯器。
seo-description: Learn how to switch back to the Classic UI Editor.
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
source-wordcount: '100'
ht-degree: 7%

---

# 编辑器{#editor}

根據預設，從編輯器切換到傳統UI的功能已停用。

若要重新啟用選項 **在傳統UI中開啟** 在 **頁面資訊** 選單中，請依照下列步驟操作。

1. 使用CRXDE Lite尋找下列節點：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用建立覆蓋 **覆蓋節點** 選項；例如：

   * **路径**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆盖位置**: `/apps/`
   * **符合節點型別**：作用中（選取核取方塊）

1. 將下列多值文字屬性新增至覆蓋的節點：

   `sling:hideProperties = ["granite:hidden"]`

1. 此 **在傳統UI中開啟** 選項在中再次可用 **頁面資訊** 功能表。

   ![](assets/syui-03-2019-02-27-15-19-48.png)
