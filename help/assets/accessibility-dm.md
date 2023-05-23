---
title: Dynamic Media 中的辅助功能
description: 瞭解Dynamic Media和Dynamic Media檢視器中的協助工具支援。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# [!DNL Dynamic Media] 中的辅助功能 {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 在編寫使用者介面中支援鍵盤控制和輔助技術，例如JAWS和NVDA熒幕閱讀器。

## 中的鍵盤協助工具支援 [!DNL Dynamic Media]

因為 [!DNL Dynamic Media] 是外掛程式，用於 [!DNL Adobe Experience Manager Assets]，大部分的鍵盤控制行為與中的相同 [!DNL Experience Manager Assets]. 例如， `Cancel` 中的按鈕 [!DNL Dynamic Media] 與中的焦點反白顯示相同 [!DNL Experience Manager Assets]，並會對 `Spacebar` 索引鍵為 [!DNL Experience Manager Assets]. 另請參閱 [Assets中的鍵盤快速鍵](/help/assets/accessibility.md#keyboard-shortcuts).

中個別使用者介面元素支援的按鍵動作 [!DNL Dynamic Media] 清晰易懂。 中的鍵盤控制 [!DNL Dynamic Media] 內容如下：

* 使用功能 `Tab` 和 `Shift+Tab` 按鍵以導覽頁面上的互動式元素。
使用 `Tab` 將輸入焦點推進至Tab鍵瀏覽順序中的下一個使用者介面元素；使用 `Shift+Tab` 將輸入焦點帶回上一個使用者介面元素。
焦點周遊會依循熒幕上的自然使用者介面元素位置，並依序由左至右、由上至下的順序移動。 此外，如果任何欄位有錯誤，您可以按下 `Tab` 將焦點移至其中。
* 能夠使用 `Spacebar` 和 `Enter` 鍵以啟動標準使用者介面元素，例如按鈕和下拉式清單。
* 可在作用中元素上看見鍵盤焦點反白顯示。 具有輸入焦點的使用者介面元素會接收視覺焦點指示，作為呈現於使用者介面元素周圍的邊框。
* 在熱點編輯器中，您可以使用某些自訂按鍵（例如方向鍵）與複雜的使用者介面元素互動，以重新定位熱點。
* 在互動式視訊編輯器中，您可以使用 `Spacebar` 以選取影像並將其新增至區段。 此外，您可以使用 `Backspace` 鍵以從中刪除選取的專案 **[!UICONTROL 內容]** 標籤。 此外，按下 `Tab` 功能視需要導覽頁面上的互動式元素。
* 在影像裁切/智慧型裁切編輯器中，您可以執行下列動作：
   * 使用方向鍵來裁切框架大小、重新定位影像，或兩者皆使用。
   * 第一個 `Tab` 停止反白顯示整個影像框架。 然後您可以使用鍵盤上的方向鍵來重新定位框架。
   * 接下來的四個 `Tab` 止點是框架的四個轉角。 將焦點放在框架轉角上時，轉角會反白顯示。 同樣地，您可以使用鍵盤上的方向鍵來移動焦點轉角。
另請參閱 [編輯單一影像的智慧型裁切或智慧型色票](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 中的輔助技術支援 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 使用者介面元素可與熒幕閱讀器等輔助技術搭配使用。 例如，使用鍵盤快速鍵導覽地標時，它可以辨識頁面上的地標 `D` 或使用鍵盤快速鍵的區域 `R`. 它也會在使用標題鍵盤快速鍵導覽時提供標題旁白 `H`.

## 中的鍵盤協助工具支援 [!DNL Dynamic Media] 檢視者 {#keyboard-accessibility-for-dm-viewers}

所有現成可用功能 [!DNL Dynamic Media] 檢視器元件支援客戶的鍵盤協助功能。

另請參閱 [鍵盤協助工具與導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) 在Dynamic Media檢視器參考指南中。

## 中的輔助技術支援 [!DNL Dynamic Media] 檢視者 {#assistive-technology-support-for-dm-viewers}

全部 [!DNL Dynamic Media] 檢視器元件支援ARIA （可存取的豐富網際網路應用程式）角色和屬性，以改進與熒幕閱讀器等輔助技術的整合。
請參閱 **輔助技術支援** Dynamic Media檢視器參考指南中任何自訂檢視器主題的說明主題。 例如，請參閱 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) （視訊檢視器），或 [輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 互動式影像檢視器的。

## Dynamic Media中的隱藏式字幕支援 {#closed-caption-support}

Dynamic Media支援以隱藏式字幕傳送視訊和自我調整視訊集。 註解必須顯示在視訊內容的頂端。

另請參閱 [Dynamic Media中的影片 — 在影片中新增隱藏式字幕或字幕](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助工具](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]](/help/assets/accessibility.md) 中的辅助功能

