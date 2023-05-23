---
title: AEM Forms中的預留位置文字
seo-title: Placeholder text in AEM Forms
description: 預留位置文字的目的是在控制項沒有值時協助使用者輸入資料。 可以是範例值，或是預期格式的簡短說明。
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# AEM Forms中的預留位置文字 {#placeholder-text-in-aem-forms}

預留位置文字代表單字或短語。 其目的是協助使用者在控制項沒有值時輸入資料。 預留位置文字可以是範例值，或是預期格式的簡短說明。 預留位置文字會在使用者輸入值之前顯示，當使用者輸入或選取值時會移除預留位置文字。

>[!NOTE]
>
>預留位置文字（如果已指定）必須有一個不含新行字元的值。

![包含和不包含預留位置文字的日期元件](assets/dat-picker-place-holder-text.png)

**答：** 具有預留位置文字的日期元件 **B.** 沒有預留位置文字的日期元件

AEM Forms支援密碼方塊、日期選擇器、數值方塊和文字方塊欄位的預留位置文字。\
原生HTML5日期Widget不支援預留位置文字。 若要指定預留位置文字：

1. 以滑鼠右鍵按一下支援預留位置文字的元件，然後按一下 **編輯**. 「編輯元件」對話方塊隨即出現。

1. 開啟 **標題和文字** 標籤。
1. 在「 」中指定字詞或簡短片語 **預留位置文字方塊**. 单击&#x200B;**确定**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支援預留位置文字。
