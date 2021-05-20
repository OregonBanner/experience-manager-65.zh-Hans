---
title: 创建节点
seo-title: 创建节点
description: 覆盖评论系统
seo-description: 覆盖评论系统
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 6%

---

# 创建节点{#create-nodes}

将从`/libs`到`/apps`中复制所需的最小文件数，并在`/apps`中对其进行修改，从而使用自定义版本覆盖注释系统。

>[!CAUTION]
>
>/libs文件夹的内容从不进行编辑，因为任何重新安装或升级都可能删除或替换/libs文件夹，而/apps文件夹的内容将保持不变。

在创作实例上使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) ，首先在/apps文件夹中创建一个路径，该路径与/libs文件夹中叠加的组件的路径相同。

复制的路径为：

* `/libs/social/commons/components/hbs/comments/comment`

路径中的某些节点是文件夹，而某些节点是组件。

1. 浏览到[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 创建`/apps/social`（如果它不存在）
   * 选择`/apps`节点
   * **[!UICONTROL 创建>文件夹……]**
      * 输入姓名: `social`
1. 选择`social`节点
   * **[!UICONTROL 创建]**  >文 **[!UICONTROL 件夹……]**
      * 输入姓名: `commons`
1. 选择`commons`节点
   * **[!UICONTROL 创建>文件夹……]**
      * 输入姓名: `components`
1. 选择`components`节点
   * **[!UICONTROL 创建>文件夹……]**.
      * 输入姓名: `hbs`
1. 选择`hbs`节点
   * **[!UICONTROL 创建]**  >  **[!UICONTROL 创建组件……]**
      * 输入标签：`comments`
      * 输入标题：`Comments`
      * 输入描述：`List of comments without showing avatars`
      * 超级类型: `social/commons/components/comments`
      * 输入群组：`Communities`
      * 单击&#x200B;**[!UICONTROL Next]**&#x200B;直到&#x200B;**[!UICONTROL OK]**
1. 选择`comments`节点

   * **[!UICONTROL 创建]**  >  **[!UICONTROL 创建组件……]**

      * 输入标签：`comment`
      * 输入标题：`Comment`
      * 输入描述：`A comment instance without avatars`
      * 超级类型: `social/commons/components/comments/comment`
      * 输入群组：`.hidden`
      * 单击&#x200B;**[!UICONTROL Next]**&#x200B;直到&#x200B;**[!UICONTROL OK]**
   * 选择&#x200B;**[!UICONTROL Save All]**
1. 删除默认的`comments.jsp`
   * 选择节点`/apps/social/commons/components/hbs/comments/comments.jsp`
   * 选择&#x200B;**[!UICONTROL Delete]**
1. 删除默认的comment.jsp
   * 选择节点`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 选择&#x200B;**[!UICONTROL Delete]**
   * 选择&#x200B;**[!UICONTROL Save All]**

>[!NOTE]
>
>为了保留继承链，叠加组件的`Super Type`（属性`sling:resourceSuperType`）被设置为与所叠加组件的`Super Type`相同的值，在此例中为：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


叠加图的自身`Type`（属性`sling:resourceType`）必须是相对的自引用，以便在/apps中找不到的任何内容随后都会在/libs中查找。
* 名称: `sling:resourceType`
* 类型: `String`
* 值: `social/commons/components/hbs/comments`

1. 选择绿色的`[+] Add`
   * 名称: `sling:resourceType`
   * 类型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 选择绿色的`[+] Add`
   * 选择&#x200B;**[!UICONTROL Save All]**

![创建节点](assets/create-nodes.png)
