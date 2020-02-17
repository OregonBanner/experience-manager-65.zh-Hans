---
title: 对表单制表人项目添加自定义操作
seo-title: 对表单制表人项目添加自定义操作
description: 表单开发人员可以向表单门户页面上的表单列表添加更多操作。 默认情况下，表单列表允许您访问、填写和提交表单。
seo-description: 表单开发人员可以向表单门户页面上的表单列表添加更多操作。 默认情况下，表单列表允许您访问、填写和提交表单。
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 对表单制表人项目添加自定义操作{#adding-custom-action-on-form-lister-items}

在AEM Forms中，您可以创建一个列出可用表单的门户页面。 默认情况下，您可以在门户页面上搜索和列出表单。 您可以打开表单以填写和提交您的信息。 对于在门户页面上列出的表单，仅开箱即用地提供渲染操作。 要进一步了解门户页面上的可用操作，请参阅 [创建表单门户页面](../../forms/using/creating-form-portal-page.md)。

可以向门户页面添加其他选项。 可以通过自定义表单门户的模板自定义这些选项或操作。

本文介绍如何创建按钮以直接从表单门户页面发送表单的链接。 此自定义操作需要更新Search &amp; Lister组件的模板。

向模板添加操作所需的代码如下所示。 代码 `onclick` 片断中的属性具有一个脚本，用于通过电子邮件发送表单的链接。

```mxml
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

您可以在自定义模板中添加类似的操作。 要定义JavaScript函数，请在页面级脚本上添加该函数，并将其与必需的HTML元素链接。 在上例中，表达式 `onclick` 是链接的函数。

对模板进行编辑后，示例门户页面包含一个按钮，用于通过电子邮件发送表单的链接，如下所示。

![email](assets/email.png)

