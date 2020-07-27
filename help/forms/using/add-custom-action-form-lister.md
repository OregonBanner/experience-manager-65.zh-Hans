---
title: 为表单制表人项目添加自定义操作
seo-title: 为表单制表人项目添加自定义操作
description: 表单开发人员可以在表单门户页面上为表单列表添加更多操作。 默认情况下，表单列表允许您访问、填写和提交表单。
seo-description: 表单开发人员可以在表单门户页面上为表单列表添加更多操作。 默认情况下，表单列表允许您访问、填写和提交表单。
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 为表单制表人项目添加自定义操作{#adding-custom-action-on-form-lister-items}

在AEM Forms中，您可以创建一个列出可用表单的门户页面。 默认情况下，您可以在门户页面上搜索和列表表单。 您可以打开表单以填写和提交信息。 对于门户页面上列出的表单，仅开箱即用提供渲染操作。 要进一步了解门户页面上的可用操作，请参 [阅创建表单门户页面](../../forms/using/creating-form-portal-page.md)。

可向门户页面添加其他选项。 可以通过自定义表单门户的模板自定义这些选项或操作。

本文介绍如何直接从表单门户页面创建按钮以发送表单链接。 此自定义操作需要更新搜索和制表人组件的模板。

向模板添加操作所需的代码在下面提供。 代 `onclick` 码片断中的属性具有通过电子邮件发送表单链接的脚本。

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

您可以在自定义模板中添加类似操作。 要定义JavaScript函数，请在页面级脚本上添加该函数，并将其与必需的HTML元素链接。 在上例中， `onclick` 表达式是链接函数。

对模板进行编辑后，示例门户页面包含一个按钮，用于通过电子邮件发送表单的链接，如下所示。

![email](assets/email.png)

