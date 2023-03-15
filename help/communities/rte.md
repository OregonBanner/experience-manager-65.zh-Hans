---
title: 富文本编辑器Essentials
seo-title: Rich Text Editor Essentials
description: 富文本编辑器功能概述
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# 富文本编辑器Essentials {#rich-text-editor-essentials}

## 概述 {#overview}

富文本编辑器(RTE)提供输入带有标记的文本的功能。

对于Communities组件，而与 [创作环境中的富文本编辑器](../../help/sites-authoring/rich-text-editor.md)，它会影响在发布环境中输入的文本。

![富文本编辑器](assets/rich-text-editor.png)

## 启用富文本编辑器 {#enabling-rich-text-editor}

可以启用允许用户生成内容(UGC)的社区组件以允许RTE。 根据组件是添加到页面还是包含在 [函数](functions.md)，默认情况下可以启用RTE，也可以不启用。

如果未启用，只需输入 [作者编辑模式](sites-console.md#authoring-site-content)，选择要编辑的组件，然后选择 `Rich Text Editor` 复选框。

RTE可用于以下Communities组件：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [评论](comments.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [消息](configure-messaging.md)
* [问题与解答](working-with-qna.md)
* [审核](reviews.md)

## 自定义 {#customization}

可以自定义富文本编辑器，因为实施基于 [CKEditor](https://www.ckeditor.com/).

Communities组件的当前配置位于 `cq.social.  scf   clientlib`，位于存储库中的

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建议修改cq.social.scf clientlib，因为未来的升级可能会覆盖任何编辑。

### 自定义示例：内联链接 {#example-customization-inline-links}

出于安全考虑，默认情况下向成员显示的富文本图标集中不包含超链接选项。 当UGC中允许href时，恶作剧的能力是广泛的。

要向工具栏添加超链接选项，请执行以下操作：

* 添加名为“”的工具栏 `links`”
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 选择 **[!UICONTROL 全部保存]**

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
