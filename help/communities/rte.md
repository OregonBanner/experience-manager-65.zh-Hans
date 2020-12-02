---
title: 富文本编辑器基础工具
seo-title: 富文本编辑器基础工具
description: 富文本编辑器功能概述
seo-description: 富文本编辑器功能概述
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: 4b6311cbfe11a61b74f68bf5a25ad1f5faef5358
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---


# 富文本编辑器必备工具{#rich-text-editor-essentials}

## 概述 {#overview}

富文本编辑器(RTE)提供了输入带有标记的文本的功能。

对于Communities组件，它与创作环境](../../help/sites-authoring/rich-text-editor.md)中的[富文本编辑器相似，但会影响在发布环境中输入的文本。

![富文本编辑器](assets/rich-text-editor.png)

## 启用富文本编辑器{#enabling-rich-text-editor}

可以启用允许用户生成内容(UGC)的社区组件以允许RTE。 根据组件是添加到页面还是包含在[函数](functions.md)中，RTE可能默认处于启用状态，也可能未启用。

如果未启用，只需进入[作者编辑模式](sites-console.md#authoring-site-content)，选择要编辑的组件，然后选中`Rich Text Editor`复选框。

RTE可用于以下社区组件：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [评论](comments.md)
* [Filelibrary](file-library.md)
* [论坛](forum.md)
* [消息](configure-messaging.md)
* [问题与解答](working-with-qna.md)
* [审核](reviews.md)

## 自定义{#customization}

由于实现基于[CKEditor](https://www.ckeditor.com/)，因此可以自定义富文本编辑器。

Communities组件的当前配置位于`cq.social.  scf   clientlib`中，该配置位于

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建议修改cq.social.scf clientlib，因为将来的升级可能会覆盖任何编辑。

### 自定义示例：内联链接{#example-customization-inline-links}

出于安全考虑，默认情况下，向成员显示的富文本图标集中不包含超链接选项。 UGC中允许href时，其恶劣性能较为强大。

要向工具栏添加超链接选项，请执行以下操作：

* 添加名为“ `links`”的工具栏
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 选择&#x200B;**[!UICONTROL 保存全部]**

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

