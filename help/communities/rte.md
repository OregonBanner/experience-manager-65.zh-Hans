---
title: 富文本编辑器要点
seo-title: 富文本编辑器要点
description: 富文本编辑器功能概述
seo-description: 富文本编辑器功能概述
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# 富文本编辑器要点{#rich-text-editor-essentials}

## 概述 {#overview}

富文本编辑器(RTE)提供了使用标记输入文本的功能。

对于社区组件，虽然与创作环境](../../help/sites-authoring/rich-text-editor.md)中的[富文本编辑器类似，但它会影响在发布环境中输入的文本。

![富文本编辑器](assets/rich-text-editor.png)

## 启用富文本编辑器{#enabling-rich-text-editor}

可以启用允许用户生成内容(UGC)的社区组件来允许RTE。 根据组件是添加到页面还是包含在[函数](functions.md)中，RTE默认可能是未启用的。

如果未启用，则只需进入[作者编辑模式](sites-console.md#authoring-site-content)，选择要编辑的组件，然后选中`Rich Text Editor`复选框。

RTE可用于以下社区组件：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [评论](comments.md)
* [Filelibrary](file-library.md)
* [论坛](forum.md)
* [消息](configure-messaging.md)
* [问题与解答](working-with-qna.md)
* [审核](reviews.md)

## 自定义 {#customization}

可以自定义富文本编辑器，因为该实现基于[CKEditor](https://www.ckeditor.com/)。

Communities组件的当前配置位于`cq.social.  scf   clientlib`中，位于

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建议修改cq.social.scf clientlib，因为以后的升级可能会覆盖任何编辑。

### 示例自定义：内联链接{#example-customization-inline-links}

出于安全考虑，默认情况下，超链接选项不会包含在呈现给成员的富文本图标集中。 在UGC中允许href时，故障诊断能力较强。

要将超链接选项添加到工具栏，请执行以下操作：

* 添加名为“ `links`”的工具栏
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 选择&#x200B;**[!UICONTROL Save All]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
