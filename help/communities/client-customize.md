---
title: 客户端自定义
seo-title: Client-side Customization
description: 在AEM Communities中自定义客户端的行为或外观
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 客户端自定义  {#client-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

要自定义客户端上AEM Communities组件的外观和/或行为，有多种方法。

两种主要方法是叠加或扩展组件。

[覆盖](#overlays) 组件会更改默认组件并影响对该组件的每个引用。

[扩展](#extensions) 唯一命名的组件会限制更改的范围。 术语“扩展”与“覆盖”可互换使用。

## 叠加 {#overlays}

覆盖元件是对缺省元件进行修改并影响使用缺省的所有实例的一种方法。

通过修改/中的默认组件副本，可以实现覆盖&#x200B;**应用程序** 目录，而不是修改/中的原始组件&#x200B;**库** 目录。 组件使用相同的相对路径构建，但“libs”替换为“apps”除外。

/apps目录是用于解析请求的第一个搜索位置，如果未找到，则使用位于/libs目录中的默认版本。

不得修改/libs目录中的默认组件，因为将来可以随意修改补丁程序和升级，以便在维护公共接口时以任何必要的方式更改/libs目录。

这与不同 [扩展](#extensions) 一个默认组件，需要针对特定用途进行修改，创建指向该组件的唯一路径，并依赖引用/libs目录中的原始默认组件作为超级资源类型。

有关覆盖注释组件的快速示例，请尝试 [叠加注释组件教程](overlay-comments.md).

## 扩展名 {#extensions}

扩展（覆盖）组件是一种在不影响使用缺省值的所有实例的情况下针对特定用途进行修改的方法。 扩展组件在/apps文件夹中具有唯一名称，并引用/libs文件夹中的默认组件，因此组件的默认设计和行为不会受到修改。

这与不同 [覆盖](#overlays) 默认组件，其中Sling的性质解析了对apps/文件夹的相对引用，然后再在libs/文件夹中搜索，因此组件的设计或行为被全局修改。

有关扩展注释组件的快速示例，请尝试 [扩展注释组件教程](extend-comments.md).

## Javascript绑定 {#javascript-binding}

组件的HBS脚本必须绑定到实施此功能的JavaScript对象、模型和视图。

的值 `data-scf-component` 属性可以是默认值，例如 **`social/tally/components/hbs/rating`**&#x200B;或用于自定义功能的扩展（自定义）组件，例如 **weretail/components/hbs/rating**.

要绑定组件，必须将整个组件脚本封装在 &lt;div> 元素具有以下属性：

* `data-component-id`=”{{id}}”

   解析为上下文中的id属性

* `data-scf-component`=”*&lt;resourcetype>*

例如，从 `/apps/weretail/components/hbs/rating/rating.hbs`：

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自订属性 {#custom-properties}

在扩展或叠加组件时，可以将属性添加到已修改的对话框中。

通过引用handlebars模板中的属性键，可以访问组件/资源上设置的所有属性：

`{{properties.<property_name>}}`

## 设置CSS外观 {#skinning-css}

通过“外观设置”（更改颜色、字体、图像、按钮、链接、间距甚至一定程度的定位）可以实现自定义组件以匹配网站的整体主题。

可以通过有选择地覆盖框架样式或通过编写全新的样式表来实现外观设置。 SCF组件定义影响构成组件的各种元素的命名空间、模块化和语义CSS类。

要建立组件的外观，请执行以下操作：

1. 标识要更改的元素（例如，编辑器区域、工具栏按钮、消息字体等）。
1. 标识影响这些元素的CSS类/规则。
1. 创建样式表文件(.css)。
1. 将样式表包含在客户端库文件夹中([clientlibs](#clientlibs-for-scf))，并确保它包含在您的模板和页面中，具有 [ui：includeClientLib](../../help/sites-developing/clientlibs.md).

1. 重新定义已在样式表中标识(#2)的CSS类和规则，并添加样式。

现在，自定义样式将覆盖默认的框架样式，组件将以新外观呈现。

>[!CAUTION]
>
>任何带有前缀的CSS类名称 `scf-js` 在javascript代码中具有特定用途。 这些类影响组件的状态（例如，从隐藏切换到可见），并且既不应覆盖也不应删除。
>
>而 `scf-js` 类不影响样式，类名可用于样式表中，但请注意，由于类名控制元素的状态，因此可能会产生副作用。

## 扩展Javascript {#extending-javascript}

要扩展组件Javascript实施，您需要：

1. 为应用程序创建一个组件，并将jcr：resourceSuperType设置为扩展组件的jcr：resourceType的值，例如social/forum/components/hbs/forum。
1. 检查默认SCF组件的Javascript以确定需要使用SCF.registerComponent()注册哪些方法。
1. 复制扩展组件的Javascript或从头开始。
1. 扩展方法。
1. 使用SCF.registerComponent()以缺省值或定制的对象和视图注册所有方法。

### forum.js： Forum - HBS的扩展示例  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## 脚本标记 {#script-tags}

脚本标记是客户端框架的内在部分。 它们是帮助将在服务器端生成的标记与客户端的模型和视图绑定的粘合剂。

覆盖或覆盖组件时，不应删除SCF脚本中的脚本标记。 为在HTML中插入JSON而自动创建的SCF脚本标记使用属性进行标识 `data-scf-json=true`.

## 适用于SCF的Clientlibs {#clientlibs-for-scf}

使用 [客户端库](../../help/sites-developing/clientlibs.md) (clientlibs)提供了一种方法，用于组织和优化在客户端上渲染内容的Javascript和CSS。

SCF的clientlibs遵循两个变体的非常特定的命名模式，这些模式仅在类别名称中存在“author”时发生变化：

| Clientlib变量 | 类别属性的模式 |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;component name> |
| 创作clientlib | cq.social.author.hbs.&lt;component name> |

### 完整Clientlibs {#complete-clientlibs}

完整的（非创作）clientlib包含依赖项，并且便于与ui：includeClientLib一起使用。

这些版本可在以下位置找到：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 客户端文件夹节点： `/etc/clientlibs/social/hbs/forum`
* 类别属性： `cq.social.hbs.forum`

此 [社区组件指南](components-guide.md) 列出每个SCF组件所需的完整clientlibs。

[适用于社区组件的Clientlibs](clientlibs.md) 介绍如何将clientlibs添加到页面。

### 创作Clientlibs {#author-clientlibs}

作者版本clientlibs将被精简为实施组件所需的最小Javascript。

这些clientlibs绝不应该直接包含在内，而是可以嵌入到为网站手工创建的其他clientlibs中。

这些版本可在SCF libs文件夹中找到：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 客户端文件夹节点： `/libs/social/forum/hbs/forum/clientlibs`
* 类别属性： `cq.social.author.hbs.forum`

注意：虽然创作clientlibs从不嵌入其他库，但它们会列出其依赖项。 嵌入到其他库时，依赖项不会自动拉入，还必须嵌入。

可以通过将“author”插入为中的每个SCF组件列出的clientlibs来标识所需的创作clientlibs。 [社区组件指南](components-guide.md).

### 使用注意事项 {#usage-considerations}

每个站点在管理客户端库的方式上各不相同。 各种因素包括：

* 整体速度：也许是因为希望网站具有响应性，但可以接受第一页加载缓慢。 如果许多页面使用相同的Javascript，则各种Javascript可以嵌入到一个clientlib中，并从要加载的第一个页面中引用。 此单次下载中的Javascript仍保持缓存状态，从而最大限度地减少后续页面要下载的数据量。
* 首页所用时间较短：可能希望快速加载第一页。 在这种情况下，Javascript位于多个小文件中，仅在需要时引用。
* 第一页加载和后续下载之间的平衡。

| **[⇐ Feature Essentials](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
