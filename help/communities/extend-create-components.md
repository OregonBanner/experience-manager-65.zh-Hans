---
title: 创建组件
description: 了解如何使用由注释和注释组件组成的注释系统来扩展组件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# 创建组件  {#create-the-components}

扩展组件的示例使用注释系统，该系统由两个组件组成。

* 注释 — 包含注释系统，是放置在页面上的组件。
* 评论 — 捕获已发布评论的实例的组件。

必须同时设置这两个组件，尤其是自定义已发布评论的外观时。

>[!NOTE]
>
>每个站点页面只允许一个注释系统。
>
>许多Communities功能已经包括注释系统，其resourceType可以修改为引用扩展的注释系统。

## 创建注释组件 {#create-the-comments-component}

这些方向指定 **组** 值除 `.hidden` 因此，组件可以从组件浏览器(sidekick)中提供。

删除自动创建的JSP文件是因为改用了默认的HBS文件。

1. 浏览至 **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 为自定义应用程序创建位置：

   * 选择 `/apps` 节点

      * **创建文件夹** 已命名 **[!UICONTROL 自定义]**

   * 选择 `/apps/custom` 节点

      * **创建文件夹** 已命名 **[!UICONTROL 组件]**

1. 选择 `/apps/custom/components` 节点

   * **[!UICONTROL 创建>组件……]**

      * **标签**： *评论*
      * **标题**： *替代注释*
      * **描述**： *替代注释样式*
      * **超级类型**： *social/commons/components/hbs/comments*
      * **组**： *自定义*

   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 确定]**

1. 展开已创建的节点： `/apps/custom/components/comments`
1. 选择 **[!UICONTROL 全部保存]**
1. 右键单击 `comments.jsp`
1. 选择 **[!UICONTROL 删除]**
1. 选择 **[!UICONTROL 全部保存]**

![create-component](assets/create-component.png)

### 创建子注释组件 {#create-the-child-comment-component}

这些方向设置 **组** 到 `.hidden` 因为页面中只应包含父组件。

删除自动创建的JSP文件是因为改用了默认的HBS文件。

1. 导航至 `/apps/custom/components/comments` 节点
1. 右键单击节点

   * 选择 **[!UICONTROL 创建]** > **[!UICONTROL 组件……]**

      * **标签**： *注释*
      * **标题**： *替代批注*
      * **描述**： *替代注释样式*
      * **超级类型**： *social/commons/components/hbs/comments/comment*
      * **组**: `*.hidden*`

   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 下一个]**
   * 选择 **[!UICONTROL 确定]**

1. 展开已创建的节点： `/apps/custom/components/comments/comment`
1. 选择 **[!UICONTROL 全部保存]**
1. 右键单击 `comment.jsp`
1. 选择 **[!UICONTROL 删除]**
1. 选择 **[!UICONTROL 全部保存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### 复制和修改默认HBS脚本 {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 复制 `comments.hbs`

   * 从 [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 编辑 `comments.hbs` 至：

   * 更改 `data-scf-component` 属性（~第20行）：

      * 发件人 `social/commons/components/hbs/comments`
      * 收件人 `/apps/custom/components/comments`

   * 修改以包含自定义注释组件（第75行）：

      * 替换 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 替换为 `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* 复制 `comment.hbs`

   * 从 [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 至 [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 编辑 `comment.hbs` 至：

   * 更改data-scf-component属性的值（~第19行）

      * 发件人 `social/commons/components/hbs/comments/comment`
      * 收件人 `/apps/custom/components/comments/comment`

* 选择 `/apps/custom` 节点
* 选择 **[!UICONTROL 全部保存]**

## 创建客户端库文件夹 {#create-a-client-library-folder}

要避免包含此客户端库，可以使用默认注释系统clientlib的类别值( `cq.social.author.hbs.comments`)。 但是，此clientlib随后也必须包含在默认组件的所有实例中。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 选择 `/apps/custom/components/comments` 节点
* 选择 **[!UICONTROL 创建节点]**

   * **名称**：`clientlibs`
   * **类型**：`cq:ClientLibraryFolder`
   * 添加至 **[!UICONTROL 属性]** 选项卡：

      * **名称** `categories` **类型** `String` **值** `cq.social.author.hbs.comments` `Multi`
      * **名称** `dependencies` **类型** `String` **值** `cq.social.scf` `Multi`

* 选择 **[!UICONTROL 全部保存]**
* 替换为 `/apps/custom/components/comments/clientlib`s节点已选中，请创建三个文件：

   * **名称**：`css.txt`
   * **名称**：`js.txt`
   * **名称**：customcommentsystem.js

* 输入&#39;customcommentsystem.js&#39;作为的内容 `js.txt`
* 选择 **[!UICONTROL 全部保存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## 注册SCF模型和视图 {#register-the-scf-model-view}

扩展（覆盖）SCF组件时，resourceType不同（覆盖使用搜索到的相对搜索机制） `/apps` 早于 `/libs` 以使resourceType保持不变)。 这就是为什么有必要编写JavaScript（在客户端库中）来注册SCF JS模型和查看自定义resourceType的原因。

输入以下文本作为的内容 `customcommentsystem.js`：

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

要在发布环境中体验扩展组件，必须复制自定义组件。

这样做的一种方式是：

* 从全局导航，

   * 选择 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**
   * 选择 **[!UICONTROL 激活树]**
   * 设置 `Start Path` 到 `/apps/custom`
   * 取消选中 **[!UICONTROL 仅已修改]**
   * 选择 **[!UICONTROL 激活]** 按钮
