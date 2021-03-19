---
title: Dynamic Media 中的辅助功能
description: 了解Dynamic Media和Dynamic Media查看器中的辅助功能支持
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: 辅助功能
role: 业务从业者，管理员
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# [!DNL Dynamic Media] {#working-with-three-d-assets-dm}中的辅助功能

[!DNL Dynamic Media] 跨创作用户界面支持键盘控制和辅助技术，如JAWS和NVDA屏幕阅读器。

## [!DNL Dynamic Media]中支持键盘辅助功能

由于[!DNL Dynamic Media]是[!DNL Adobe Experience Manager Assets]的插件，因此大多数键盘控制行为与[!DNL Experience Manager Assets]中完全相同。 例如，[!DNL Dynamic Media]中的`Cancel`按钮与[!DNL Experience Manager Assets]中的具有相同的焦点高亮，并对`Spacebar`键作出响应，与[!DNL Experience Manager Assets]中的键作出响应。 请参阅Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[键盘快捷键。

[!DNL Dynamic Media]中各个用户界面元素支持的按键在大多数情况下都显而易见，易于发现。 [!DNL Dynamic Media]中的键盘控件与以下内容相关：

* 能够使用`Tab`和`Shift+Tab`按键在页面上的交互式元素之间导航。
使用`Tab`将输入焦点按Tab键顺序提前到下一个用户界面元素；使用`Shift+Tab`将输入焦点返回到上一个用户界面元素。
焦点遍历遵循屏幕上自然的用户界面元素位置，并按从左到右、然后从上到下的顺序移动。 此外，如果任何字段有错误，可按`Tab`将焦点移到该字段。
* 能够使用`Spacebar`和`Enter`键激活标准用户界面元素，如按钮、下拉列表等。
* 能够在活动元素上查看键盘焦点突出显示。 具有输入焦点的用户界面元素可以接收可视焦点指示作为呈现在用户界面元素周围的边框。
* 在热点编辑器中，您可以使用一些自定义按键（如箭头键）与复杂的用户界面元素进行交互以重新定位热点。
* 在交互式视频编辑器中，可以使用`Spacebar`选择图像并将其添加到区段。 此外，您还可以使用`Backspace`键从&#x200B;**[!UICONTROL Content]**&#x200B;选项卡中删除选定项。 此外，按`Tab`可根据需要在页面上的交互式元素之间导航。
* 在图像裁剪/智能裁剪编辑器中，您可以执行以下操作：
   * 使用箭头键裁剪帧大小，或重新定位图像，或同时使用两者。
   * 第一个`Tab`停止将高亮显示整个图像帧。 然后，可以使用键盘上的箭头键重新定位框架。
   * 接下来的四个`Tab`停止是框架的四个角。 当焦点置于框架角上时，该角将高亮显示。 同样，您可以使用键盘上的箭头键移动聚焦的角。
请参阅[编辑单个图像的智能裁剪或智能色板](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## [!DNL Dynamic Media] {#assistive-technology-support-for-dm}中的辅助技术支持

[!DNL Dynamic Media] 用户界面元素可与屏幕阅读器等辅助技术配合使用。例如，当您使用键盘快捷键`D`或使用键盘快捷键`R`的区域导航地标时，它会识别页面上的地标。 使用标题键盘快捷键`H`导航时，还会解说标题。

## [!DNL Dynamic Media]查看器{#keyboard-accessibility-for-dm-viewers}中支持键盘辅助功能

所有现成的[!DNL Dynamic Media]查看器组件都支持客户使用键盘进行访问。

请参阅《Dynamic Media查看器参考指南》中的[键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## [!DNL Dynamic Media]查看器{#assistive-technology-support-for-dm-viewers}中的辅助技术支持

所有[!DNL Dynamic Media]查看器组件都支持ARIA（可访问的富Internet应用程序）角色和属性，以改进与屏幕阅读器等辅助技术的集成。
请参阅《Dynamic Media查看器参考指南》中任何自定义查看器主题中的**辅助技术支持**&#x200B;帮助主题。 例如，请参阅[视频查看器的辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)或交互式图像查看器的[辅助技术支持](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解决方案的可访问性](https://www.adobe.com/accessibility.html)
>* [中的辅助功能 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

