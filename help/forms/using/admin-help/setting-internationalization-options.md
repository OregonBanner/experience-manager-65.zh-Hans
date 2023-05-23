---
title: 設定國際化選項
seo-title: Setting internationalization options
description: 瞭解如何指定用於轉譯表單的地區設定，以及如何指定用於編碼輸出資料流的字元集。
seo-description: Learn how to specify the locale used to render forms and how to specify the character set used to encode the output stream.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# 設定國際化選項{#setting-internationalization-options}

## 指定用於呈現表單的地區設定 {#specify-the-locale-used-to-render-forms}

您可以指定呈現PDF表單時使用的地區設定。 PDF表單上的欄位會使用指定的地區設定來顯示資料。 例如，如果locale設定為德文，則表單會使用德文小數分隔符號來分隔數值。 地區設定也可用來傳送驗證訊息給使用者端裝置（例如網頁瀏覽器），作為HTML轉換的一部分。

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「國際化」下的「語言」清單中，選取用來呈現表單的地區設定。 預設值為英文（美國）。
1. 单击“保存”。

## 指定用來編碼輸出資料流的字元集 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 在「國際化」下的「字元集」清單中，選取字元集。 此設定取決於所使用的API，即renderHTMLForm或renderPDFForm。 若要指定所列字元集以外的字元集，請選取「自訂」，然後在顯示的方塊中指定編碼值。

   對於HTML轉換，AEM表單支援下列定義的字元編碼值： `java.nio.charset` 封裝。 如果sFormPreference是PDForm，則僅支援特定字元集。 字元集必須是有效的正式名稱。 預設值為ISO-8859-1。

1. 单击“保存”。
