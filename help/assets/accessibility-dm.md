---
title: 中的辅助功能 [!DNL Dynamic Media]
description: 了解Dynamic Media和Dynamic Media查看器中的辅助功能
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 383f84b1a984683b3e2ce60f1a3f2191749a1561
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 中的辅助功能 [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 支持跨创作用户界面的键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## 支持 [!DNL Dynamic Media]

因 [!DNL Dynamic Media] 为是插件， [!DNL Adobe Experience Manager Assets]大多数键盘控制行为与中完全相同 [!DNL Experience Manager Assets]。 例如，中的 `Cancel` 按钮 [!DNL Dynamic Media] 的焦点突出显示与中相同， [!DNL Experience Manager Assets]并对键做出与中 `Spacebar` 相同的反应 [!DNL Experience Manager Assets]。 请参阅 [资产中的键盘快捷键](/help/assets/accessibility.md#keyboard-shortcuts)。

大多数情况下，单个用户界面元 [!DNL Dynamic Media] 素支持的按键显而易见，易于发现。 中的键盘 [!DNL Dynamic Media] 控件与以下内容相关：

* 能够使用 `Tab` 和按 `Shift+Tab` 键在页面上的交互式元素之间导航。
使用 `Tab` Tab键顺序将输入焦点提前到下一个用户界面元素；使用 `Shift+Tab` 可将输入焦点重新放回以前的用户界面元素。
焦点遍历遵循屏幕上的自然用户界面元素位置，并按从左到右、从上到下的顺序移动。 此外，如果任何字段有错误，可按 `Tab` 键将焦点移到该字段。
* 能够使用 `Spacebar` 和 `Enter` 键激活标准用户界面元素，如按钮、下拉列表等。
* 能够在活动元素上查看键盘焦点突出显示。 具有输入焦点的用户界面元素可以接收可视焦点指示作为呈现在用户界面元素周围的边框。
* 在热点编辑器中，您可以使用一些自定义按键（如箭头键）与复杂的用户界面元素进行交互，从而重新确定热点的位置。
* 在交互式视频编辑器中，您可 `Spacebar` 以使用选择图像并将其添加到区段。 此外，您还可以使用键从“内 `Backspace` 容”选项卡中删除选定 **[!UICONTROL 项]** 。 此外，按 `Tab` 所需功能可在页面上的交互式元素之间导航。
* 在图像裁剪／智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键可裁剪帧大小，或者重新定位图像，或者两者。
   * 第一个停 `Tab` 靠点高亮显示整个图像帧。 然后，可以使用键盘上的箭头键重新定位框架。
   * 接下来的 `Tab` 四个停靠点是框架的四个角。 当焦点放在框架角上时，该角将高亮显示。 同样，您可以使用键盘上的箭头键移动聚焦的角。
请参 [阅编辑单个图像的智能裁剪或智能色板](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Adobe Cloud中的 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 用户界面元素可与屏幕阅读器等辅助技术配合使用。 例如，当您使用键盘快捷键导航地标或使用键盘快捷键定位区域时，它 `D` 会识别页面上的地标 `R`。 它还会在使用标题键盘快捷键导航时解说标题 `H`。

## 查看器中支持键盘辅助 [!DNL Dynamic Media] 功能 {#keyboard-accessibility-for-dm-viewers}

所有现成的查看器组件都支 [!DNL Dynamic Media] 持为客户提供键盘辅助功能。

请参 [阅《Dynamic Media Viewers](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) Reference Guide》中的键盘辅助功能和导航。

## 查看器中的辅助技 [!DNL Dynamic Media] 术 {#assistive-technology-support-for-dm-viewers}

所有 [!DNL Dynamic Media] 查看器组件都支持ARIA（可访问的富Internet应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅 **《Dynamic Media Viewers Reference Guide** 》中任何自定义查看器主题中的辅助技术支持帮助主题。 例如，请参 [阅视频查看器的](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) “辅助型技术支持”或“ [交互式图像查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) ”的“辅助型技术支持”。

>[!MORELIKETHIS]
>
>* [Adobe解决方案的辅助功能](https://www.adobe.com/accessibility.html)
>* [中的辅助功能 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

