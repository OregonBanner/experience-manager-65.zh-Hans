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
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---

# 客户端自定义{#client-side-customization}

| **[⇐功能要点](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

要自定义AEM Communities组件在客户端的外观和/或行为，有多种方法。

两种主要方法是叠加或扩展组件。

[](#overlays) 叠加组件会更改默认组件，并影响对该组件的每个引用。

[](#extensions) 扩展组件（其名称唯一）会限制更改的范围。术语“extend”可与“override”交替使用。

## 叠加 {#overlays}

叠加组件是对默认组件进行修改并影响所有使用默认组件的实例的方法。

叠加是通过修改/**apps**&#x200B;目录中默认组件的副本而不修改/**libs**&#x200B;目录中的原始组件来完成的。 该组件使用相同的相对路径构建，不同之处在于“lib”被替换为“apps”。

首先搜索/apps目录来解析请求，如果找不到，则使用位于/libs目录中的默认版本。

/libs目录中的默认组件绝不能修改，因为以后的修补程序和升级可以在维护公共接口时以任何必要的方式自由更改/libs目录。

这与[扩展](#extensions)默认组件不同，默认组件希望对特定用途进行修改，创建组件的唯一路径，并依赖在/libs目录中引用原始默认组件作为超级资源类型。

有关覆盖注释组件的快速示例，请尝试使用[覆盖注释组件教程](overlay-comments.md)。

## 扩展 {#extensions}

扩展（覆盖）组件是一种为特定用途进行修改，而不影响使用默认值的所有实例的方法。 扩展组件在/apps文件夹中具有唯一名称，并引用/libs文件夹中的默认组件，因此不会修改组件的默认设计和行为。

这与[覆盖](#overlays)的默认组件不同，在默认组件中，Sling的性质会先解析对应用程序/文件夹的相对引用，然后再在libs/文件夹中搜索，从而全局修改组件的设计或行为。

有关扩展注释组件的快速示例，请尝试使用[扩展注释组件教程](extend-comments.md)。

## Javascript绑定{#javascript-binding}

组件的HBS脚本必须绑定到实施此功能的JavaScript对象、模型和视图。

`data-scf-component`属性的值可能是默认值，如&#x200B;**`social/tally/components/hbs/rating`**，或用于自定义功能的扩展（自定义）组件，如&#x200B;**weretail/components/hbs/rating**。

要绑定组件，必须将整个组件脚本包含在&lt;div>元素中，并具有以下属性：

* `data-component-id`=&quot;{{id}}&quot;

   解析为上下文中的id属性

* `data-scf-component`=&quot;*&lt;resourcetype>*

例如，从`/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自订属性 {#custom-properties}

扩展或覆盖组件时，可以向修改的对话框添加属性。

可通过引用handlebars模板中的属性键来访问在组件/资源上设置的所有属性：

`{{properties.<property_name>}}`

## 设置CSS {#skinning-css}外观

可通过“设置外观”（在一定程度上更改颜色、字体、图像、按钮、链接、间距甚至定位）来自定义组件以匹配网站的整体主题。

可以通过选择性地覆盖框架样式或通过编写全新样式表来实现外观设置。 SCF组件定义命名节点、模块化和语义CSS类，这些类影响构成组件的各种元素。

要设置组件的外观，请执行以下操作：

1. 识别要更改的元素（示例 — 编辑器区域、工具栏按钮、消息字体等）。
1. 识别影响这些元素的CSS类/规则。
1. 创建样式表文件(.css)。
1. 将样式表包含在站点的客户端库文件夹([clientlibs](#clientlibs-for-scf))中，并确保它包含在模板和具有[ui:includeClientLib](../../help/sites-developing/clientlibs.md)的页面中。

1. 重定义您在样式表中标识(#2)的CSS类和规则，并添加样式。

自定义样式现在将覆盖默认框架样式，并且组件将使用新外观呈现。

>[!CAUTION]
>
>前缀为`scf-js`的任何CSS类名称在Javascript代码中具有特定用法。 这些类会影响组件的状态（例如，从隐藏切换到可见），因此不应覆盖也不应删除。
>
>虽然`scf-js`类不影响样式，但类名称可能用在样式表中，但应当注意，当它们控制元素状态时，可能会产生副作用。

## 扩展Javascript {#extending-javascript}

要扩展组件Javascript实施，您需要：

1. 为应用程序创建组件，并将jcr:resourceSuperType设置为扩展组件的jcr:resourceType的值，例如social/forum/components/hbs/forum。
1. 检查默认SCF组件的Javascript，以确定需要使用SCF.registerComponent()注册哪些方法。
1. 复制扩展组件的Javascript或从头开始。
1. 扩展方法。
1. 使用SCF.registerComponent()注册所有方法（使用缺省值或自定义对象和视图）。

### forum.js:论坛的扩展示例 — HBS {#forum-js-sample-extension-of-forum-hbs}

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

脚本标记是客户端框架的固有部分。 它们是一种胶水，可帮助将服务器端生成的标记与客户端的模型和视图绑定。

覆盖或覆盖组件时，不应删除SCF脚本中的脚本标记。 为在HTML中插入JSON而自动创建的SCF脚本标记将使用属性`data-scf-json=true`进行标识。

## 用于SCF的Clientlibs {#clientlibs-for-scf}

使用[客户端库](../../help/sites-developing/clientlibs.md)(clientlibs)，可组织和优化用于在客户端上呈现内容的Javascript和CSS。

SCF的clientlib遵循两个变体的非常特定的命名模式，这两个变体仅在类别名称中存在“author”时有所不同：

| Clientlib变体 | 类别属性的模式 |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;component name=&quot;&quot;> |
| author clientlib | cq.social.author.hbs.&lt;component name=&quot;&quot;> |

### 完成Clientlibs {#complete-clientlibs}

完整的（非作者）clientlib包含依赖项，便于在ui:includeClientLib中包含。

以下版本可在中找到：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 客户端文件夹节点：`/etc/clientlibs/social/hbs/forum`
* 类别属性：`cq.social.hbs.forum`

[社区组件指南](components-guide.md)列出了每个SCF组件所需的完整客户端库。

[Clientlibs for Communities组件介](clientlibs.md) 绍了如何向页面添加clientlibs。

### 创作Clientlibs {#author-clientlibs}

创作版本clientlib已清空到实施组件所需的最低Javascript。

这些clientlib绝不应直接包含在内，而是可嵌入到其他clientlib中，这些clientlib是为网站精心编制的。

这些版本位于SCF libs文件夹中：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 客户端文件夹节点：`/libs/social/forum/hbs/forum/clientlibs`
* 类别属性：`cq.social.author.hbs.forum`

注意：虽然作者clientlibs从不嵌入其他库，但他们会列出其依赖项。 嵌入到其他库中时，依赖关系不会自动提取，还必须嵌入。

所需的创作clientlib可通过将“author”插入[Community Components指南](components-guide.md)中为每个SCF组件列出的clientlib中来识别。

### 使用注意事项{#usage-considerations}

每个网站在管理客户端库的方式上各不相同。 各种因素包括：

* 总体速度：或许希望网站能够做出响应，但可以接受第一个页面加载速度有点慢。 如果许多页面使用相同的Javascript，则可以将各种Javascript嵌入到一个clientlib中，并从要加载的第一个页面引用。 此单次下载中的Javascript仍保持缓存状态，可最大限度地减少后续页面要下载的数据量。
* 到首页的时间很短：可能希望快速加载第一个页面。 在这种情况下，Javascript位于多个小文件中，只有在需要时才可引用。
* 在首次页面加载与后续下载之间实现平衡。

| **[⇐功能要点](essentials.md)** | **[服务器端自定义⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
