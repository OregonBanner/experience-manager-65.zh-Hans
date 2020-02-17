---
title: 客户端自定义
seo-title: 客户端自定义
description: 在AEM Communities中自定义行为或外观客户端
seo-description: 在AEM Communities中自定义行为或外观客户端
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 客户端自定义 {#client-side-customization}

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义‡](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers‡](handlebars-helpers.md)** |

要自定义客户端上AEM Communities组件的外观和／或行为，有多种方法。

两种主要方法是叠加或扩展组件。

[覆盖组件](#overlays) ，将更改默认组件，并影响对组件的每个引用。

[扩展](#extensions) （以唯一名称命名）组件会限制更改的范围。 术语“extend”与“override”可互换使用。

## 叠加 {#overlays}

覆盖组件是修改默认组件并影响所有使用默认组件的实例的方法。

叠加是通过修改/**apps目录中默认组件的副本而不是修改/** libs **目录中的原始组件来完成** 的。 该组件使用相同的相对路径构建，但“lib”被替换为“apps”。

/apps目录是解析请求时首先搜索的位置，如果找不到，则使用位于/libs目录中的默认版本。

不得修改/libs目录中的默认组件，因为以后的修补程序和升级可以在维护公共接口时以任何必要的方式免费更改/libs目录。

这与扩展默认组件 [不同](#extensions) ，在该组件中，您希望修改特定用途，创建组件的唯一路径，并依赖引用/libs目录中的原始默认组件作为超级资源类型。

有关覆盖注释组件的快速示例，请尝试“叠加注 [释组件”教程](overlay-comments.md)。

## 扩展 {#extensions}

扩展（覆盖）组件是一种修改特定用途的方法，不影响使用默认值的所有实例。 扩展组件在/apps文件夹中以唯一方式命名，并引用/libs文件夹中的默认组件，因此不会修改组件的默认设计和行为。

这与覆盖默认组 [件不同](#overlays) ，在默认组件中，Sling的性质会解析对apps/文件夹的相对引用，然后在libs/文件夹中搜索，从而全局修改组件的设计或行为。

有关扩展注释组件的快速示例，请尝试“扩展 [注释组件”教程](extend-comments.md)。

## Javascript绑定 {#javascript-binding}

组件的HBS脚本必须绑定到实现此功能的JavaScript对象、模型和视图。

属性的值可 `data-scf-component` 以是默认值，如 **`social/tally/components/hbs/rating`**，或者是自定义功能的扩展（自定义）组件，如 **weretail/components/hbs/rating**。

要绑定组件，整个组件脚本必须包含在&lt;div>元素中，并具有以下属性：

* `data-component-id`=&quot;{{id}}&quot;

   解析到上下文中的id属性

* `data-scf-component`=&quot;*&lt;resourceType>*

例如，从 `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自订属性 {#custom-properties}

在扩展或覆盖组件时，可以向修改后的对话框添加属性。

通过引用handlebars模板中的属性键，可以访问组件／资源上设置的所有属性：

`{{properties.<property_name>}}`

## 设置CSS外观 {#skinning-css}

自定义组件以匹配网站的整体主题可通过“设置外观”实现——在一定程度上更改颜色、字体、图像、按钮、链接、间距甚至定位。

通过有选择地覆盖框架样式或编写全新的样式表，可以实现外观设计。 SCF组件定义命名空间、模块化和语义CSS类，这些类影响组成组件的各种元素。

设置组件外观：

1. 确定要更改的元素（例如，书写器区域、工具栏按钮、消息字体等）。
1. 识别影响这些元素的CSS类／规则。
1. 创建样式表文件(.css)。
1. 将样式表包含在站点的客户端库文件夹([clientlibs](#clientlibs-for-scf))中，并确保它包含在您的模板和包含 [ui:includeClientLib的页面中](../../help/sites-developing/clientlibs.md)。

1. 重新定义您在样式表中标识的(#2)CSS类和规则，并添加样式。

自定义样式现在将覆盖默认框架样式，并且组件将使用新外观呈现。

>[!CAUTION]
>
>前缀为** scf-js-&amp;ast;**的任何CSS类名在javascript代码中具有特定用途。 这些类影响组件的状态（例如，从隐藏切换到可见），不应覆盖也不应删除。
>
>而scf-js-amp;ast;类不影响样式，类名称可能用在样式表中，但须注意，由于它们控制元素的状态，可能会有副作用。

## 扩展Javascript {#extending-javascript}

要扩展组件Javascript实现，您只需

1. 为您的应用程序创建一个组件，并将jcr:resourceSuperType设置为扩展组件的jcr:resourceType的值，如social/forum/components/hbs/forum
1. 检查默认SCF组件的Javascript，以确定使用SCF.registerComponent()需要注册哪些方法
1. 复制扩展组件的Javascript或从头开始
1. 扩展方法
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

## 脚本标记 {#script-tags}

脚本标签是客户端框架的固有部分。 它们是帮助将服务器端生成的标记与客户端的模型和视图绑定在一起的粘合剂。

在覆盖或覆盖组件时，不应删除SCF脚本中的脚本标签。 为在HTML中注入JSON而自动创建的SCF脚本标记使用属性 `data-scf-json=`true标识。

## SCF的Clientlib {#clientlibs-for-scf}

客户端库 [](../../help/sites-developing/clientlibs.md) (clientlibs)的使用提供了一种组织和优化用于在客户端呈现内容的Javascript和CSS的方法。

SCF的clientlib遵循两个变体的非常特定的命名模式，这两个变体只因类别名称中存在“author”而异：

| Clientlib变体 | 类别属性的模式 |
|--- |--- |
| 完整的clientlib | cq.social.hbs.&lt;组件名称> |
| author clientlib | cq.social.author.hbs&lt;组件名称> |

### 完整Clientlib {#complete-clientlibs}

完整的（非作者）clientlib包含依赖关系，并且便于与ui:includeClientLib一起使用。

这些版本位于：

* /etc/clientlibs/social/hbs/&lt;component name>

例如：

* 客户端文件夹节点：/etc/clientlibs/social/hbs/forum
* 类别属性：cq.social.hbs.forum

“社 [区组件”指南列出](components-guide.md) ，每个SCF组件需要完整的客户端库。

[Clientlibs for Communities组件介绍如何向页面添加clientlibs](clientlibs.md) 。

### 作者Clientlibs {#author-clientlibs}

创作版本clientlibs将被去除，直到实现组件所需的最小Javascript。

这些clientlib永远不应直接包含在内，而是可嵌入到为站点手工制作的其他clientlib中。

这些版本位于SCF库文件夹中：

* /libs/social/&lt;feature>/components/hbs/&lt;component name>/clientlibs

例如：

* 客户端文件夹节点：/libs/social/forum/hbs/forum/clientlibs
* 类别属性：cq.social.author.hbs.forum

注意：虽然作者clientlibs从不嵌入其他库，但它们确实会列出其依赖关系。 当嵌入到其他库中时，依赖关系不会自动拉入并且也必须嵌入。

通过在“社区组件”指南中为每个SCF组件列出的clientlib中插入“author”，可以识别所需的作 [者clientlib](components-guide.md)。

### 使用注意事项 {#usage-considerations}

每个站点在管理客户端库方面都有所不同。 各种因素包括：

* 总体速度：也许希望网站能够做出响应，但第一页的加载速度有点慢是可以接受的。 如果许多页面使用相同的Javascript，则各种Javascript可嵌入到一个clientlib中，并从要加载的第一页引用。 此次下载中的Javascript将保持缓存，从而最小化后续页面的要下载的数据量。
* 短时间到首页：也许希望第一页快速加载。 在这种情况下，Javascript位于多个小文件中，只在需要时引用。
* 第一页加载与后续下载之间的平衡。

| **[‹功能基本工具](essentials.md)** | **[服务器端自定义‡](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers‡](handlebars-helpers.md)** |

