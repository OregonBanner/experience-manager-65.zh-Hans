---
title: Dynamic Media 中的辅助功能
description: 了解Dynamic Media和Dynamic Media查看器中的无障碍支持。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# 中的辅助功能 [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 在整个创作用户界面中支持键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## 中的键盘辅助功能支持 [!DNL Dynamic Media]

因为 [!DNL Dynamic Media] 是 [!DNL Adobe Experience Manager Assets]，则大多数键盘控制行为与中的相同 [!DNL Experience Manager Assets]. 例如， `Cancel` 按钮 [!DNL Dynamic Media] 焦点突出显示与中的相同 [!DNL Experience Manager Assets]，并对 `Spacebar` 键 [!DNL Experience Manager Assets]. 请参阅 [Assets中的键盘快捷键](/help/assets/accessibility.md#keyboard-shortcuts).

中各个用户界面元素支持的击键 [!DNL Dynamic Media] 清晰易见。 键盘控件 [!DNL Dynamic Media] 与以下内容有关：

* 使用功能 `Tab` 和 `Shift+Tab` 键击，以在页面上的交互式元素之间导航。
使用 `Tab` 按Tab键顺序将输入焦点提前到下一个用户界面元素；使用 `Shift+Tab` 将输入焦点重新引回到上一个用户界面元素。
焦点遍历遵循屏幕上自然的用户界面元素位置，并按从左到右、从上到下的顺序移动。 此外，如果有任何字段出错，您可以按 `Tab` 把焦点移到它上。
* 能够使用 `Spacebar` 和 `Enter` 用于激活标准用户界面元素（如按钮和下拉列表）的键。
* 能够查看活动元素上的键盘焦点突出显示。 具有输入焦点的用户界面元素接收作为呈现在用户界面元素周围的边框的可视焦点指示。
* 在热点编辑器中，您可以使用一些自定义键击（如箭头键）与复杂的用户界面元素进行交互，以调整热点位置。
* 在交互式视频编辑器中，您可以使用 `Spacebar` 来选择图像并将其添加到区段。 此外，您还可以使用 `Backspace` 用于从 **[!UICONTROL 内容]** 选项卡。 还有，紧 `Tab` 功能。
* 在图像裁剪/智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键裁剪帧大小，或调整图像位置，或者同时调整两者。
   * 第一个 `Tab` 停止会高亮显示整个图像帧。 然后，可使用键盘上的箭头键调整框架的位置。
   * 接下来的四个 `Tab` 停止是框架的四个角。 当焦点位于框架角上时，该角会突出显示。 再次重申，您可以使用键盘上的箭头键来移动聚焦的角。
请参阅 [编辑单个图像的智能裁剪或智能色板](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 中的辅助技术支持 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 用户界面元素可与屏幕阅读器等辅助技术配合使用。 例如，当您使用键盘快捷键导航地标时，它会识别页面上的地标 `D` 或使用键盘快捷键的区域 `R`. 使用标题键盘快捷键导航时，还会讲述标题 `H`.

## 中的键盘辅助功能支持 [!DNL Dynamic Media] 查看者 {#keyboard-accessibility-for-dm-viewers}

开箱即用 [!DNL Dynamic Media] 查看器组件支持为客户提供键盘辅助功能。

请参阅 [键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) (在《Dynamic Media查看器参考指南》中)。

## 中的辅助技术支持 [!DNL Dynamic Media] 查看者 {#assistive-technology-support-for-dm-viewers}

全部 [!DNL Dynamic Media] 查看器组件支持ARIA（无障碍的富互联网应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅 **辅助技术支持** 《Dynamic Media查看器参考指南》中任何自定义查看器主题中的帮助主题。 例如，请参阅 [辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) ，或 [辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) （对于交互式图像查看器）。

## Dynamic Media中的隐藏式字幕支持 {#closed-caption-support}

Dynamic Media支持交付带有隐藏式字幕的视频和自适应视频集。 字幕必须显示在视频内容的顶部。

请参阅 [Dynamic Media中的视频 — 在视频中添加隐藏式字幕或字幕](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [中的辅助功能 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

