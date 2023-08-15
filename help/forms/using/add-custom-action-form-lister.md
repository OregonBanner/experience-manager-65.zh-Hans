---
title: 添加对表单列表程序项的自定义操作
seo-title: Adding custom action on form lister items
description: 表单开发人员可以在表单门户页面上向表单列表添加更多操作。 默认情况下，表单列表允许您访问表单、填写并提交表单。
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing lets you access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 添加对表单列表程序项的自定义操作{#adding-custom-action-on-form-lister-items}

在AEM Forms中，您可以创建一个门户页面，其中列出可用的表单。 默认情况下，您可以在门户页面上搜索和列出表单。 您可以打开表单填写并提交您的信息。 仅为门户页面上列出的表单提供现成的渲染操作。 要详细了解门户页面上可用的操作，请参阅 [创建表单门户页面](../../forms/using/creating-form-portal-page.md).

您可以将其他选项添加到门户页面。 通过自定义表单门户的模板，可以自定义这些选项或操作。

本文演示了如何创建按钮以直接从Forms门户页面发送表单链接。 此自定义设置需要更新Search &amp; Lister组件的模板。

下面提供了将操作添加到模板所需的代码。 此 `onclick` 代码片段中的属性具有一个脚本，用于通过电子邮件发送表单的链接。

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

您可以在自定义模板中添加类似操作。 要定义JavaScript函数，请在页面级脚本中添加该函数，并将其与必需的HTML元素链接。 在上例中， `onclick` expression是链接的函数。

在对模板进行编辑后，示例门户页面包含一个按钮，用于通过电子邮件发送表单的链接，如下所示。

![email](assets/email.png)
