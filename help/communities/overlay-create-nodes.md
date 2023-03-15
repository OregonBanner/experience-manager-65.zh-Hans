---
title: 创建节点
seo-title: Create Nodes
description: 覆盖评论系统
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 7%

---

# 创建节点 {#create-nodes}

通过复制以下位置所需的最少文件数，使用自定义版本覆盖评论系统： `/libs` 到 `/apps` 并在中修改它们 `/apps`.

>[!CAUTION]
>
>永远不会编辑/libs文件夹的内容，因为任何重新安装或升级操作都可能会删除或替换/libs文件夹，而/apps文件夹的内容保持不变。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 在创作实例上，首先在/apps文件夹中创建一条路径，该路径与/libs文件夹中覆盖组件的路径相同。

要复制的路径为：

* `/libs/social/commons/components/hbs/comments/comment`

路径中的某些节点是文件夹，而某些节点是组件。

1. 浏览到 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 创建 `/apps/social` （如果它尚不存在）
   * 选择 `/apps` 节点
   * **[!UICONTROL 创建>文件夹……]**
      * 输入姓名: `social`
1. 选择 `social` 节点
   * **[!UICONTROL 创建]** > **[!UICONTROL 文件夹……]**
      * 输入姓名: `commons`
1. 选择 `commons` 节点
   * **[!UICONTROL 创建>文件夹……]**
      * 输入姓名: `components`
1. 选择 `components` 节点
   * **[!UICONTROL 创建>文件夹……]**.
      * 输入姓名: `hbs`
1. 选择 `hbs` 节点
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件……]**
      * 输入标签： `comments`
      * 输入标题： `Comments`
      * 输入描述: `List of comments without showing avatars`
      * 超级类型: `social/commons/components/comments`
      * 输入组： `Communities`
      * 单击 **[!UICONTROL 下一个]** 直到 **[!UICONTROL 确定]**
1. 选择 `comments` 节点

   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件……]**

      * 输入标签： `comment`
      * 输入标题： `Comment`
      * 输入描述: `A comment instance without avatars`
      * 超级类型: `social/commons/components/comments/comment`
      * 输入组： `.hidden`
      * 单击 **[!UICONTROL 下一个]** 直到 **[!UICONTROL 确定]**
   * 选择 **[!UICONTROL 全部保存]**
1. 删除默认值 `comments.jsp`
   * 选择节点 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 选择 **[!UICONTROL 删除]**
1. 删除默认的comment.jsp
   * 选择节点 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 选择 **[!UICONTROL 删除]**
   * 选择 **[!UICONTROL 全部保存]**

>[!NOTE]
>
>为了保留继承链， `Super Type` (属性 `sling:resourceSuperType`)的值设置为与相同的值 `Super Type` 在本例中，覆盖的组件包括：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


叠加本身的 `Type`(属性 `sling:resourceType`)必须为相对自引用，以便在/apps中未找到的任何内容随后会在/libs中查找。
* 名称: `sling:resourceType`
* 类型: `String`
* 值: `social/commons/components/hbs/comments`

1. 选择绿色 `[+] Add`
   * 名称: `sling:resourceType`
   * 类型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 选择绿色 `[+] Add`
   * 选择 **[!UICONTROL 全部保存]**

![create-nodes](assets/create-nodes.png)
