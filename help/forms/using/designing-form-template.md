---
title: 為HTML5表單設計表單範本
seo-title: Designing form templates for HTML5 forms
description: AEM Forms提供轉譯XFA表單範本為HTML5格式的功能。 表單設計人員可以使用Designer設計表單範本，並使用HTML5轉譯功能。
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# 為HTML5表單設計表單範本{#designing-form-templates-for-html-forms}

AEM中的HTML5表單元件提供將XFA表單範本轉譯為HTML5格式。 表單設計人員可使用以下專案設計表單範本： [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn) 和使用HTML5轉譯功能。 這些表單範本及其資產可以存放在AEM存放庫、檔案系統中，或透過http公開。 不過，如果您打算使用Forms Manager管理表單，範本和資產應存放在AEM存放庫中。

雖然HTML5表單在很大程度上符合PDF forms的行為，但兩種格式都有某些功能不適用於其他格式。 例如，在Adobe Reader中，在PDF表單上套用條碼的方式，會因行動表單而異，或是表單經過數位簽署的方式，也會因格式而異。 如需這類變異的詳細資訊，請參閱 [HTML5表單與PDF forms之間的功能差異](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

如需常見XFA功能，請參閱下列最佳實務和指導方針，以設計可同時使用兩種格式的表單。

## 最佳實務 {#best-practices}

設計表單範本的大部分步驟（例如結構描述繫結或撰寫表單邏輯）都相同。 不過，由於Adobe Reader等厚型使用者端的轉譯和指令碼引擎與瀏覽器型表單之間固有的差異，因此中介紹了一些建議 [最佳實務](/help/forms/using/design-accessible-html5-forms.md) 文章。 這些最佳實務可協助您設計表單範本，使其在兩種格式中都能如預期般運作。

### 適用於HTML5 Forms的AEM Forms Designer功能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 預覽HTML {#preview-html}

「預覽HTML」標籤會新增至「設計」模式，供表單設計人員在設計過程中以HTML5格式預覽表單。 如需如何在AEM Forms Designer中啟用和設定此功能的詳細資訊，請參閱 [預覽HTML](../../forms/using/preview-xdp-forms-html.md).

#### 连笔签名 {#scribble-signature}

HTML5表單的主要目標是觸控裝置。 因此，在AEM Forms Designer中新增了塗鴉簽名控制項。 您可以按一下或拖放表單範本上的手寫簽名控制項並進行設定。 它在HTML5轉譯中呈現為手寫欄位，並可用於觸控裝置上的手寫簽名。 在桌上型電腦上，它可以使用滑鼠控制項做為塗鴉欄位。 如需如何使用此功能的詳細資訊，請參閱 [XFA手寫欄位](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### RTF格式 {#rich-text-format}

您可以將文字欄位轉換為RTF文字欄位。 它會將格式選項清單新增至文字欄位。 若要轉換，請開啟Forms Designer，然後點選中的文字欄位 **[!UICONTROL 設計檢視]**. 在 **[!UICONTROL 欄位]** 索引標籤，選取 **[!UICONTROL RTF文字]** 從 **[!UICONTROL 欄位格式]** 下拉式清單。 現在，當XFA表單呈現為HTML5表單時，欄位會呈現為RTF文字欄位。 點選 ![最大化](assets/maximize_icon.svg) 以檢視其他格式選項。
