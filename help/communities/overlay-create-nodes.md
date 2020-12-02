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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 6%

---


# 创建节点{#create-nodes}

将从`/libs`到`/apps`所需的最少文件数复制到`/apps`中并修改它们，从而将注释系统与自定义版本叠加。

>[!CAUTION]
>
>/libs文件夹的内容从不进行编辑，因为任何重新安装或升级都可能删除或替换/libs文件夹，而/apps文件夹的内容则保持不变。

在创作实例上使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，首先在/apps文件夹中创建一个路径，该路径与/libs文件夹中叠加的组件的路径相同。

复制的路径为：

* `/libs/social/commons/components/hbs/comments/comment`

路径中的某些节点是文件夹，有些是组件。

1. 浏览至[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 创建`/apps/social`（如果它尚不存在）
   * 选择`/apps`节点
   * **[!UICONTROL “创建”>“文件夹……”]**
      * 输入姓名: `social`
1. 选择`social`节点
   * **[!UICONTROL 创建]** >文 **[!UICONTROL 件夹……]**
      * 输入姓名: `commons`
1. 选择`commons`节点
   * **[!UICONTROL “创建”>“文件夹……”]**
      * 输入姓名: `components`
1. 选择`components`节点
   * **[!UICONTROL “创建”>“文件夹。.]**.”
      * 输入姓名: `hbs`
1. 选择`hbs`节点
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件……]**
      * 输入标签：`comments`
      * 输入标题：`Comments`
      * 输入说明：`List of comments without showing avatars`
      * 超级类型: `social/commons/components/comments`
      * 输入组：`Communities`
      * 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;直到&#x200B;**[!UICONTROL 确定]**
1. 选择`comments`节点

   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件……]**

      * 输入标签：`comment`
      * 输入标题：`Comment`
      * 输入说明：`A comment instance without avatars`
      * 超级类型: `social/commons/components/comments/comment`
      * 输入组：`.hidden`
      * 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;直到&#x200B;**[!UICONTROL 确定]**
   * 选择&#x200B;**[!UICONTROL 保存全部]**
1. 删除默认`comments.jsp`
   * 选择节点`/apps/social/commons/components/hbs/comments/comments.jsp`
   * 选择&#x200B;**[!UICONTROL 删除]**
1. 删除默认的comment.jsp
   * 选择节点`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 选择&#x200B;**[!UICONTROL 删除]**
   * 选择&#x200B;**[!UICONTROL 保存全部]**

>[!NOTE]
>
>为了保留继承链，叠加组件的`Super Type`（属性`sling:resourceSuperType`）设置为与要覆盖的组件的`Super Type`相同的值，在这种情况下：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


叠加自己的`Type`（属性`sling:resourceType`）必须是相对自引用，这样在/apps中找不到的任何内容就会在/libs中查找。
* 名称: `sling:resourceType`
* 类型: `String`
* 值: `social/commons/components/hbs/comments`

1. 选择绿色`[+] Add`
   * 名称: `sling:resourceType`
   * 类型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 选择绿色`[+] Add`
   * 选择&#x200B;**[!UICONTROL 保存全部]**

![create-nodes](assets/create-nodes.png)

