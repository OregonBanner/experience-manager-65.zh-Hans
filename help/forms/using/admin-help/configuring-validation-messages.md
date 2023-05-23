---
title: 設定驗證訊息
seo-title: Configuring validation messages
description: 瞭解如何指定驗證訊息的顯示方式及其相對於網頁瀏覽器中傳回之表單的位置。
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%

---

# 設定驗證訊息 {#configuring-validation-messages}

對於呈現為HTML的表單，會為使用者顯示發生的表單驗證錯誤。 您可以自訂驗證訊息的顯示方式。 根據驗證訊息的顯示位置，您也可以控制訊息在表單中的位置以及框架邊框的大小。

## 指定驗證訊息的顯示方式 {#specify-how-validation-messages-are-displayed}

1. 在Administration Console中，按一下Services > forms。
1. 在「驗證輸出」下的「報表」清單中，選取下列其中一個選項：

   **訊息方塊：** 在個別的對話方塊中顯示驗證訊息。

   **影格：** 在相同視窗的框架中顯示驗證訊息。

   **無框架：** 若要在同一視窗中顯示驗證訊息，請執行下列步驟： 此值為預設值。

   **透過API （含資料）：** 透過API （包含資料）傳回驗證訊息的方式。 驗證訊息不會顯示在畫面上。

   **透過API （透過表單）：** 透過API （連同表單）傳回驗證訊息的方式。 驗證訊息不會顯示在畫面上。

   **無：** 不顯示驗證訊息。

1. 单击“保存”。

## 指定相對於網頁瀏覽器中傳回之表單的驗證訊息位置 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

當「報告」設定為「框架」或「無框架」時，您可以指定驗證訊息的位置。

1. 在「驗證輸出」下的「位置」清單中，選取下列其中一個選項：

   **左：** 在網頁瀏覽器的左側顯示驗證訊息。

   **右：** 在網頁瀏覽器的右側顯示驗證訊息。

   **上**：在網頁瀏覽器頂端顯示驗證訊息。 此值為預設值。

   **下**：在網頁瀏覽器底部顯示驗證訊息。

1. 单击“保存”。

## 指定框架邊框大小 {#specify-the-frame-border-size}

當「報表」設定為「框架」時，您可以指定框架邊框大小。

1. 在「驗證輸出」下方的「邊框大小」方塊中，輸入框架邊框的大小（畫素）。

   邊框大小必須等於或大於0。 默认值为 1。

1. 单击“保存”。
