---
title: 创建节点
seo-title: 创建节点
description: 叠加注释系统
seo-description: 叠加注释系统
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# 创建节点 {#create-nodes}

通过将最少数量的文件从中复制到中并在中修改，将注释系统与自定 `/libs` 义版本 `/apps` 叠加在一起 `/apps`。

>[!CAUTION]
>
>/libs文件夹的内容从不进行编辑，因为任何重新安装或升级都可能删除或替换/libs文件夹，而/apps文件夹的内容保持不变。


在作 [者实例上使用CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) ，首先在/apps文件夹中创建一个路径，该路径与/libs文件夹中叠加的组件的路径相同。

复制的路径为：

* `/libs/social/commons/components/hbs/comments/comment`

路径中的某些节点是文件夹，有些是组件。

1. 浏览到http://localhost:4502/crx/de/index.jsp [目录](http://localhost:4502/crx/de/index.jsp)
1. 创 `/apps/social` 建（如果尚不存在）
   * 选择节 `/apps` 点
   * **[!UICONTROL “创建”>“文件夹……”]**
      * 输入姓名: `social`
1. 选择节 `social` 点
   * **[!UICONTROL 创建]** >文 **[!UICONTROL 件夹……]**
      * 输入姓名: `commons`
1. 选择节 `commons` 点
   * **[!UICONTROL “创建”>“文件夹……”]**
      * 输入姓名: `components`
1. 选择节 `components` 点
   * **[!UICONTROL “创建”>“文件夹。.]**.”
      * 输入姓名: `hbs`
1. 选择节 `hbs` 点
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件……]**
      * 输入标签： `comments`
      * Enter Title: `Comments`
      * Enter Description: `List of comments without showing avatars`
      * 超级类型: `social/commons/components/comments`
      * 输入组： `Communities`
      * 单击“下 **[!UICONTROL 一步]** ”，直到 **[!UICONTROL “确定”]**
1. 选择节 `comments` 点

   * **[!UICONTROL 创建>创建组件……]**

      * 输入标签： `comment`
      * Enter Title: `Comment`
      * Enter Description: `A comment instance without avatars`
      * 超级类型: `social/commons/components/comments/comment`
      * 输入组： `.hidden`
      * 单击“下 **[!UICONTROL 一步]** ”，直到 **[!UICONTROL “确定”]**
   * 选择 **[!UICONTROL 全部保存]**
1. 删除默认 `comments.jsp`
   * 选择节点 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 选择删 **[!UICONTROL 除]**
1. 删除默认的comment.jsp
   * 选择节点 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 选择删 **[!UICONTROL 除]**
   * 选择 **[!UICONTROL 全部保存]**

>[!NOTE]
>
>为了保留继承链，叠加组件的 `Super Type` (属性 `sling:resourceSuperType`)设置为与要覆盖的组件相同的值，在本例中 `Super Type` 为：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>



叠加自己的 `Type`(属性 `sling:resourceType`)必须是相对的自引用，这样在/apps中找不到的任何内容就会在/libs中查找。
* 名称: `sling:resourceType`
* 类型: `String`
* 值: `social/commons/components/hbs/comments`

1. 选择绿色 `[+] Add`
   * 名称: `sling:resourceType`
   * 类型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 选择绿色 `[+] Add`
   * 选择 **[!UICONTROL 全部保存]**

![chlimage_1-4](assets/chlimage_1-4.png)

