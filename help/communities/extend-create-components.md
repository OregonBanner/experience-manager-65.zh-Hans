---
title: 创建组件
seo-title: 创建组件
description: 创建注释组件
seo-description: 创建注释组件
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 创建组件 {#create-the-components}

扩展组件的示例使用注释系统，该系统实际上由两个组件组成

* 注释——包含注释系统，它是放置在页面上的组件
* 评论——捕获已发布评论的实例的组件

这两个组件都需要到位，尤其是自定义已发布评论的外观时。

>[!NOTE]
>
>每个站点页面仅允许一个评论系统。
>
>许多Communities功能已经包括一个注释系统，其resourceType可以修改为引用扩展注释系统。

## 创建注释组件 {#create-the-comments-component}

这些方向指定 **组值** ，而不是指定组值， `.hidden` 以便组件可以从组件浏览器(Sidekick)中使用。

删除自动创建的JSP文件是因为将使用默认的HBS文件。

1. 浏览至 **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 为自定义应用程序创建一个位置：

   * 选择节 `/apps` 点

      * **创建名为** custom的文 **[!UICONTROL 件夹]**
   * 选择节 `/apps/custom` 点

      * **创建名为组件的文件夹** (Folder **[!UICONTROL )]**


1. 选择节 `/apps/custom/components` 点

   * **[!UICONTROL 创建>组件……]**

      * **标签**:评 *论*
      * **标题**:替 *代注释*
      * **说明**:替 *代注释样式*
      * **超类型**: *social/commons/components/hbs/comments*
      * **组**:自定 *义*
   * Select **[!UICONTROL Next]**
   * Select **[!UICONTROL Next]**
   * Select **[!UICONTROL Next]**
   * 选择确 **[!UICONTROL 定]**


1. 展开刚刚创建的节点： `/apps/custom/components/comments`
1. 选择 **[!UICONTROL 全部保存]**
1. 右键单击 `comments.jsp`
1. 选择删 **[!UICONTROL 除]**
1. 选择 **[!UICONTROL 全部保存]**

![chlimage_1-70](assets/chlimage_1-70.png)

### 创建子注释组件 {#create-the-child-comment-component}

这些方 **向将** Group设置为 `.hidden` ，因为页面中应仅包含父组件。

删除自动创建的JSP文件是因为将使用默认的HBS文件。

1. 导航到节 `/apps/custom/components/comments` 点
1. 右键单击节点

   * 选择 **[!UICONTROL 创建>组件……]**

      * **标签**:评 *论*
      * **标题**:替 *代注释*
      * **说明**:替 *代注释样式*
      * **超类型**: *social/commons/components/hbs/comments/comments*
      * **组**: `*.hidden*`
   * Select **[!UICONTROL Next]**
   * Select **[!UICONTROL Next]**
   * Select **[!UICONTROL Next]**
   * 选择确 **[!UICONTROL 定]**


1. 展开刚刚创建的节点： `/apps/custom/components/comments/comment`
1. 选择 **[!UICONTROL 全部保存]**
1. 右键单击 `comment.jsp`
1. 选择删 **[!UICONTROL 除]**
1. 选择 **[!UICONTROL 全部保存]**

![chlimage_1-71](assets/chlimage_1-71.png) ![chlimage_1-72](assets/chlimage_1-72.png)

### 复制和修改默认HBS脚本 {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 复制 `comments.hbs`

   * From [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 编辑 `comments.hbs` 到：

   * 更改属性的 `data-scf-component` 值(~line 20):

      * 发件人 `social/commons/components/hbs/comments`
      * 收件人 `/apps/custom/components/comments`
   * 修改以包含自定义注释组件（~第75行）:

      * 替换 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * With `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* 复制 `comment.hbs`

   * From [/libs/social/commons/components/hbs/comments/comments/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 收件人 [/apps/custom/components/comments/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 编辑 `comment.hbs` 到：

   * 更改data-scf-component属性的值(~ line 19)

      * 发件人 `social/commons/components/hbs/comments/comment`
      * 收件人 `/apps/custom/components/comments/comment`

* 选择节 `/apps/custom` 点
* 选择 **[!UICONTROL 全部保存]**

## 创建客户端库文件夹 {#create-a-client-library-folder}

为避免显式包含此客户端库，可以使用默认注释系统的clientlib的类别值( `cq.social.author.hbs.comments`)，但随后也会为默认组件的所有实例包含此clientlib。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 选择节 `/apps/custom/components/comments` 点
* 选择 **[!UICONTROL 创建节点]**

   * **名称**: `clientlibs`
   * **类型**: `cq:ClientLibraryFolder`
   * 添加到“属 **[!UICONTROL 性]** ”选项卡：

      * **名称**`categories` Type **Value** `String` Zh ****`cq.social.author.hbs.comments` Play `Multi`
      * **名称**`dependencies` Type **Value** `String` Zh ****`cq.social.scf` Play `Multi`

* 选择 **[!UICONTROL 全部保存]**
* 选择 `/apps/custom/components/comments/clientlib`s节点后，创建3个文件：

   * **名称**: `css.txt`
   * **名称**: `js.txt`
   * **名称**:customcommentsystem.js

* 输入“customcommentsystem.js”作为 `js.txt`
* 选择 **[!UICONTROL 全部保存]**

![chlimage_1-73](assets/chlimage_1-73.png)

## 注册SCF模型和视图 {#register-the-scf-model-view}

在扩展（覆盖）SCF组件时，resourceType是不同的(覆盖利用以前搜索的相对搜索机制，以 `/apps` 便 `/libs` resourceType保持不变)。 因此，必须编写JavaScript（在客户端库中）来注册自定义resourceType的SCF JS模型和视图。

输入以下文本作为内容 `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* 选择 **[!UICONTROL 全部保存]**

## 发布应用程序 {#publish-the-app}

要体验发布环境中的扩展组件，必须复制自定义组件。

这样做的一个方法是

* 从全局导航

   * 选择“ **[!UICONTROL 工具”>“部署”>“复制”]**
   * 选择 `Activate Tree`
   * 设置 `Start Path`:to `/apps/custom`
   * 取消选中 `Only Modified`
   * 选择按 `Activate`钮

