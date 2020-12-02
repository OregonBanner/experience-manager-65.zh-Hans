---
title: 客户端自定义
seo-title: 客户端自定义
description: 在AEM Communities自定义行为或外观客户端
seo-description: 在AEM Communities自定义行为或外观客户端
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# 客户端自定义{#client-side-customization}

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars帮助器](handlebars-helpers.md)** |

要在客户端自定义AEM Communities组件的外观和／或行为，有多种方法。

叠加或扩展组件有两种主要方法。

[叠](#overlays) 加组件会更改默认组件并影响对组件的每个引用。

[扩](#extensions) 展组件（以唯一方式命名）会限制更改的范围。术语“extend”与“override”可互换使用。

## 叠加{#overlays}

覆盖组件是修改默认组件并影响所有使用默认组件的实例的方法。

通过修改/**apps**&#x200B;目录中默认组件的副本，而不是修改/**libs**&#x200B;目录中的原始组件，完成叠加。 该组件使用相同的相对路径构建，但“libs”被替换为“apps”。

/apps目录是解析请求时首先搜索的位置，如果找不到，则使用位于/libs目录中的默认版本。

/libs目录中的默认组件绝不能修改，因为以后的修补程序和升级可以在维护公共接口时以任何必要方式免费更改/libs目录。

这与[扩展](#extensions)默认组件不同，在默认组件中，您希望修改特定用途，为组件创建唯一路径，并依赖引用/libs目录中的原始默认组件作为超级资源类型。

有关覆盖注释组件的快速示例，请尝试[覆盖注释组件教程](overlay-comments.md)。

## 扩展{#extensions}

扩展（覆盖）组件是一种修改特定用途的方法，不会影响使用默认值的所有实例。 扩展组件在/apps文件夹中以唯一方式命名，并引用/libs文件夹中的默认组件，因此不会修改组件的默认设计和行为。

这与在libs/文件夹中搜索之前，将[覆盖](#overlays)默认组件不同，其中Sling的性质解析对apps/文件夹的相对引用，从而全局修改组件的设计或行为。

有关扩展注释组件的快速示例，请尝试[扩展注释组件教程](extend-comments.md)。

## Javascript绑定{#javascript-binding}

组件的HBS脚本必须绑定到实现此功能的JavaScript对象、模型和视图。

`data-scf-component`属性的值可以是默认值，如&#x200B;**`social/tally/components/hbs/rating`**，或用于自定义功能的扩展（自定义）组件，如&#x200B;**weretail/components/hbs/rating**。

要绑定组件，必须将整个组件脚本包含在&lt;div>元素中，并具有以下属性：

* `data-component-id`=&quot;{{id}}&quot;

   解析到上下文中的id属性

* `data-scf-component`=&quot;*&lt;resourcetype>*

例如，从`/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自订属性 {#custom-properties}

在扩展或覆盖组件时，可以向修改的对话框添加属性。

通过引用handlebars模板中的属性键，可以访问在组件／资源上设置的所有属性：

`{{properties.<property_name>}}`

## 设置CSS {#skinning-css}外观

自定义组件以匹配网站的整体主题可通过“设置外观”实现——在一定程度上更改颜色、字体、图像、按钮、链接、间距甚至定位。

通过有选择地覆盖框架样式或编写全新的样式表，可以实现外观设置。 SCF组件定义命名空间、模块化和语义CSS类，这些类影响构成组件的各种元素。

设置组件外观：

1. 确定要更改的元素（例如，书写器区域、工具栏按钮、消息字体等）。
1. 确定影响这些元素的CSS类／规则。
1. 创建样式表文件(.css)。
1. 将样式表包含在站点的客户端库文件夹([clientlibs](#clientlibs-for-scf))中，并确保它包含在模板和具有[ui:includeClientLib](../../help/sites-developing/clientlibs.md)的页面中。

1. 重新定义您在样式表中标识的(#2)CSS类和规则，并添加样式。

自定义样式现在将覆盖默认框架样式，并且组件将使用新外观呈现。

>[!CAUTION]
>
>前缀为`scf-js`的任何CSS类名在javascript代码中都有特定用途。 这些类影响组件的状态（例如，从隐藏切换到可见），不应覆盖也不应删除。
>
>虽然`scf-js`类不影响样式，但类名称可能在样式表中使用，但必须注意，由于它们控制元素的状态，可能会产生副作用。

## 扩展Javascript {#extending-javascript}

要扩展组件Javascript实现，您需要：

1. 为您的应用程序创建一个组件，将jcr:resourceSuperType设置为扩展组件的jcr:resourceType的值，如social/forum/components/hbs/forum。
1. 检查默认SCF组件的Javascript以确定需要使用SCF.registerComponent()注册哪些方法。
1. 从头复制扩展组件的Javascript或开始。
1. 扩展方法。
1. 使用SCF.registerComponent()注册所有具有默认值或自定义对象和视图的方法。

### forum.js:论坛扩展示例- HBS {#forum-js-sample-extension-of-forum-hbs}

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

## 脚本标记{#script-tags}

脚本标签是客户端框架的固有部分。 它们是帮助将服务器端生成的标记与客户端的型号和视图绑定在一起的粘合剂。

在覆盖或覆盖组件时，不应删除SCF脚本中的脚本标签。 为在HTML中注入JSON而自动创建的SCF脚本标记使用属性`data-scf-json=true`进行标识。

## SCF的客户端库{#clientlibs-for-scf}

使用[客户端库](../../help/sites-developing/clientlibs.md)(clientlibs)提供了一种组织和优化用于在客户端上呈现内容的Javascript和CSS的方法。

SCF的clientlibs对于两个变体遵循非常特定的命名模式，只有在类别名中存在“author”时，该模式才会有所不同：

| Clientlib变体 | 类别属性的模式 |
|--- |--- |
| 完整的clientlib | cq.social.hbs.&lt;component name=&quot;&quot;> |
| 作者clientlib | cq.social.author.hbs.&lt;component name=&quot;&quot;> |

### 完整的Clientlibs {#complete-clientlibs}

完整（非作者）clientlib包含依赖项，并且便于与ui:includeClientLib一起使用。

以下版本位于：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 客户端文件夹节点：`/etc/clientlibs/social/hbs/forum`
* 类别属性：`cq.social.hbs.forum`

[社区组件指南](components-guide.md)列表每个SCF组件所需的完整客户端库。

[社区组件的](clientlibs.md) Clientlibs介绍如何将Clientlibs添加到页面。

### 作者Clientlibs {#author-clientlibs}

创作版本clientlibs将被精简为实现该组件所需的最少Javascript。

这些clientlib永远不应直接包含在内，而是可以嵌入到为站点手工制作的其他clientlib中。

这些版本位于SCF libs文件夹中：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 客户端文件夹节点：`/libs/social/forum/hbs/forum/clientlibs`
* 类别属性：`cq.social.author.hbs.forum`

注意：虽然作者clientlibs从不嵌入其他库，但他们会列表其依赖关系。 嵌入到其他库时，依赖项不会自动拉入，还必须嵌入。

通过在[社区组件指南](components-guide.md)中为每个SCF组件列出的clientlib中插入“author”，可以识别所需的作者客户端。

### 使用注意事项{#usage-considerations}

每个站点在管理客户端库方面都有所不同。 各种因素包括：

* 总体速度：可能是希望网站能够响应，但第一页的加载速度会稍慢，这是可以接受的。 如果许多页面使用相同的Javascript，则各种Javascript可嵌入到一个clientlib中，并从要加载的第一页引用。 此次下载中的Javascript仍保持缓存状态，从而最大限度地减少后续页面的下载数据量。
* 短时间到首页：也许最好让第一页快速加载。 在这种情况下，Javascript位于多个小文件中，只在需要时引用。
* 第一页加载与后续下载之间的平衡。

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars帮助器](handlebars-helpers.md)** |

