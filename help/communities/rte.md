---
title: RTF編輯器程式集
seo-title: Rich Text Editor Essentials
description: RTF編輯器功能概觀
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

# RTF編輯器程式集 {#rich-text-editor-essentials}

## 概述 {#overview}

RTF編輯器(RTE)提供輸入含標示文字的功能。

若為Communities元件，則類似於 [作者環境中的RTF編輯器](../../help/sites-authoring/rich-text-editor.md)，它會影響在發佈環境中輸入的文字。

![RTF編輯器](assets/rich-text-editor.png)

## 啟用RTF編輯器 {#enabling-rich-text-editor}

允許使用者產生內容(UGC)的Communities元件可啟用以允許RTE。 根據元件是新增至頁面還是包含在 [函式](functions.md)，RTE依預設可能會啟用，也可能不會啟用。

如果未啟用，只要輸入 [作者編輯模式](sites-console.md#authoring-site-content)，選取要編輯的元件，然後選取 `Rich Text Editor` 核取方塊。

RTE適用於下列Communities元件：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [评论](comments.md)
* [檔案庫](file-library.md)
* [论坛](forum.md)
* [消息](configure-messaging.md)
* [问题与解答](working-with-qna.md)
* [审核](reviews.md)

## 自訂 {#customization}

RTF編輯器可以自訂，因為實作是根據 [CKEditor](https://www.ckeditor.com/).

Communities元件的目前設定位於 `cq.social.  scf   clientlib`，位於存放庫中的

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建議修改cq.social.scf clientlib，因為未來的升級可能會覆寫任何編輯。

### 自訂範例：內嵌連結 {#example-customization-inline-links}

基於安全性考量，超連結選項不會包含在預設提供給成員的RTF圖示集中。 當UGC中允許href時，惡意連結的能力很強。

若要將超連結選項新增至工具列：

* 新增名為「」的工具列 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選取 **[!UICONTROL 全部儲存]**

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
