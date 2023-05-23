---
title: 新增表單製作者專案的自訂動作
seo-title: Adding custom action on form lister items
description: 表單開發人員可以在表單入口網站頁面上的表單清單中新增更多動作。 依預設，表單清單可讓您存取表單、填寫並提交表單。
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 新增表單製作者專案的自訂動作{#adding-custom-action-on-form-lister-items}

在AEM Forms中，您可以建立入口網站頁面，列出可用的表單。 依預設，您可以在入口網站頁面上搜尋和列出表單。 您可以開啟表格以填寫並提交資訊。 對於入口網站頁面上列出的表單，僅提供開箱即用的轉譯動作。 若要進一步瞭解入口網站頁面上可用的動作，請參閱 [建立表單入口網站頁面](../../forms/using/creating-form-portal-page.md).

您可以將其他選項新增至入口網站頁面。 您可以自訂表單入口網站的範本，以自訂這些選項或動作。

本文示範如何建立按鈕，以直接從表單入口網站頁面傳送表單連結。 此自訂需要更新Search &amp; Lister元件的範本。

以下提供將動作新增至範本的必要程式碼。 此 `onclick` 程式碼片段中的屬性有指令碼，可透過電子郵件傳送表單的連結。

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

您可以在自訂範本中新增類似的動作。 若要定義JavaScript函式，請在頁面層級的指令碼上新增函式，並將其與必要的HTML元素連結。 在上述範例中， `onclick` 運算式是連結的函式。

對範本進行編輯後，範例入口網站頁面包含一個按鈕，可透過電子郵件傳送表單的連結，如下所示。

![email](assets/email.png)
