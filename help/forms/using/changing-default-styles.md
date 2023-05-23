---
title: 變更HTML5表單的預設樣式
seo-title: Changing default styles of HTML5 forms
description: HTML5表單樣式是以CSS為基礎。 您可以變更表單的預設樣式。
seo-description: HTML5 forms styling is based on CSS. You can change the default styles of the form.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# 變更HTML5表單的預設樣式{#changing-default-styles-of-html-forms}

HTML5表單會使用HTML5功能演算，演算後表單的樣式會使用CSS完成。 HTML5表單的預設外觀類似於其PDF轉譯。 開發人員可使用自訂CSS來變更HTML5表單的預設外觀。

本文提供變更HTML5表單的樣式的逐步資訊，以及 [樣式簡介](/help/forms/using/css-styles.md) 本文包含有關HTML5表單各種樣式方面的詳細資訊。 在執行本文所述的步驟之前，請務必閱讀樣式簡介一文。

下列兩個影像顯示預設樣式和自訂樣式之間的差異。

![圖片–002 — 小](assets/pictures-002-small.png)

## 設定表單樣式 {#style-your-forms}

1. **選擇設定檔以新增自訂樣式**

   在URL存取CRX DE介面： **https://&lt;server>：&lt;port>/crx/de** 和建立設定檔，或選擇現有的設定檔。 若要瞭解如何建立設定檔，請參閱 [建立新的設定檔](/help/forms/using/custom-profile.md)

1. **建立CSS樣式表來設定HTML5表單的樣式**

   導覽至您建立設定檔轉譯器的資料夾，並建立CSS樣式表檔案。 請遵循下列步驟

   1. 以滑鼠右鍵按一下資料夾並選取 **建立** > **建立檔案** 從功能表

   1. 在建立檔案對話方塊中，輸入樣式表的名稱。 請務必使用.css副檔名（例如stylesheet.css）
   1. 從導覽窗格中，開啟您已建立的CSS檔案。
   1. 定義您要樣式化之元件的CSS類別，並在這些類別中新增樣式。

   若要瞭解要為HTML5表單中的特定元件建立哪些CSS類別，請參閱 [樣式簡介](/help/forms/using/css-styles.md).

1. **在設定檔轉譯器中包含樣式表**

   在CRX DE中開啟「設定檔轉譯器」頁面（jsp檔案），並將CSS檔案包含在XFA使用者端程式庫正下方的頁面中。 執行這些步驟，將CSS檔案包含在設定檔中。

   1. 在轉譯器頁面中搜尋下列行：

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 在上方的行下方插入下列內容，以包含樣式表：

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. 保存文件。
