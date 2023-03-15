---
title: 在Dynamic Media中优化图像质量的最佳实践
description: 了解在Dynamic Media中优化图像质量的最佳实践
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 48%

---

# 在Dynamic Media中优化图像质量的最佳实践 {#best-practices-for-optimizing-the-quality-of-your-images}

优化图像质量可能会是一个很耗时的过程，因为渲染可接受的效果涉及到很多因素。在某种程度上，效果带有主观性，因为每个人对图像质量都会有不同的看法。结构化试验是关键所在。

Adobe Experience Manager包含100多条Dynamic Media图像投放命令，可用于调整和优化图像和渲染结果。 以下准则可以帮助您通过使用一些基本的命令和最佳实践，简化操作过程，并快速获得最佳效果。

## 图像格式的最佳实践 (`&fmt=`) {#best-practices-for-image-format-fmt}

* 如果要以良好的质量以及可管理的大小和权重来传送图像，JPG 或 PNG 是最佳选择。
* 如果 URL 中未提供任何格式命令，Dynamic Media 图像传送将默认采用 JPG 格式。
* JPG 的压缩比率为 10:1，通常生成的图像文件较小。PNG压缩的比例约为2:1，除非有时图像包含白色背景。 但是，通常 PNG 文件大于 JPG 文件。
* JPG 采用有损压缩，这意味着在压缩过程中图像元素（像素）会有所丢失。PNG 则采用无损压缩。
* 通常情况下，JPG 在压缩摄影图像时保真度会比合成图像更高，具有清晰的边缘和对比度。
* 如果您的图像包含透明度，请使用 PNG，因为 JPG 不支持透明度。

作为图像格式的最佳实践，请从最常见的设置开始 `&fmt=JPG`.

## 图像大小的最佳实践 {#best-practices-for-image-size}

动态缩减图像大小是最常见的任务之一。这涉及到指定大小，以及（可选）指定用于缩小图像的缩减采样模式。

* 对于图像大小调整，最好且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或只是 `&hei=<value>`. 这些参数会根据宽高比自动设置图像宽度。
* `&resMode=<value>`控制用于缩减像素采样的算法。 开始于 `&resMode=sharp2`. 使用此值可提供最佳图像质量。使用缩减像素取样时 `value =bilin` 速度较快，通常会导致伪像的锯齿。

作为调整图像大小的最佳实践，请使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 图像锐化的最佳实践 {#best-practices-for-image-sharpening}

在控制网站中的图像时，图像锐化是最复杂的方面，很容易出现多种错误。请查阅以下有用资源，以详细了解锐化和USM在Experience Manager中的工作方式：

最佳实践白皮书 [在Adobe Dynamic Media Classic中锐化图像](/help/assets/assets/sharpening_images.pdf) 这也适用于Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

通过Experience Manager，您可以在摄取和/或投放时锐化图像。 但是，通常只使用一种方法或另一种方法来锐化图像，但不能同时使用这两种方法来锐化。 通常，在传送过程中通过 URL 锐化图像可实现最佳效果。

有两种可用的图像锐化方法：

* 简单锐化( `&op_sharpen`) — 与Photoshop中使用的锐化滤镜类似，简单锐化会在动态调整大小后对图像的最终视图应用基本锐化。 但是，用户不能对这种方法进行配置。最佳实践是除非需要，否则不要使用&amp;op_sharpen。
* USM锐化( `&op_USM`) — 钝化蒙版是一种行业标准的锐化滤镜。 最佳实践是按照下面的准则，使用 USM 锐化来锐化图像。您可以通过 USM 锐化控制下面的三个参数：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *数量&#x200B;*]**（0-5，效果强度。）
      * **[!UICONTROL *半径&#x200B;*]**（0-250，围绕锐化对象绘制的“锐化线”的宽度，以像素为单位。）

      请记住，参数半径和数量彼此相抵触。减小半径可以通过增加量来补偿。半径允许更细的控制，因为较低的值仅锐化边缘像素，而较高的值锐化较宽范围的像素。

      * **[!UICONTROL *阈值&#x200B;*]**（0-255，效应敏感度。）

             此参数确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素，而滤镜会锐化这些像素。 **[!UICONTROL threshold]**参数有助于避免过度锐化颜色相似的区域，如肤色。 例如，阈值为12时，会忽略肤色亮度的细微变化，以避免添加“杂色”，同时仍会为高对比度区域添加边缘对比度，如睫毛与皮肤相遇的地方。
         
         有关如何设置这三个参数的更多信息，包括使用滤镜方面的最佳实践，请参阅以下资源：

         有关锐化图像的Experience Manager帮助主题。

         最佳实践白皮书 [在Adobe Dynamic Media Classic中锐化图像](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager还允许您控制第四个参数：单色(0,1)。 此参数确定是使用值0分别将钝化蒙版应用于每个颜色组件，还是使用值1将钝化蒙版应用于图像亮度/强度。


作为最佳实践，应首先开始设置 USM 锐化 radius 参数。您可以先使用以下 radius 设置：

* **[!UICONTROL 网站]** - 0.2-0.3像素
* **[!UICONTROL 照片打印(250-300 ppi)]** - 0.3-0.5像素
* **[!UICONTROL 胶印打印(266-300 ppi)]** - 0.7-1.0像素
* **[!UICONTROL 画布打印(150 ppi)]** - 1.5-2.0像素

将 amount 从 1.75 逐渐增加至 4。如果锐化仍未达到您需要的效果，请将 radius 增加 0.1，然后再次将 amount 从 1.75 逐渐增加至 4。根据需要，重复上述步骤。

将 monochrome 参数设置保留为 0。

### JPEG压缩的最佳实践(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此参数控制 JPG 编码质量。值越大表示图像质量越高，但文件也越大；反之，值越小表示图像质量越低，但文件也越小。此参数的范围是 0-100。
* 要优化质量，切勿将该参数值设置为 100。设置为 90 或 95 与设置为 100 几乎没有什么区别，但是设置为 100 会不必要地增加图像文件的大小。因此，要优化质量但避免图像文件过大，请设置 `qlt= value` 到90或95。
* 要针对较小的图像文件大小进行优化，但使图像质量保持在可接受的级别，请设置 `qlt= value` 到80。 值低于70到75会导致图像质量显着下降。
* 作为最佳实践，要保持中立，请将 `qlt= value` 到85岁时保持中立。
* 在中使用色度标志 `qlt=`

   * 此 `qlt=` 参数具有第二个设置，允许您使用值打开RGB色度缩减像素采样 `,1` 或使用值关闭 `,0`.
   * 要保持简单，请从RGB色度缩减取样关闭(`,0`)。此设置通常可提高图像质量，尤其是对于具有大量锐边和对比度的合成图像。

作为JPG压缩的最佳实践，请使用 `&qlt=85,0`.

## JPEG 大小调整的最佳实践 (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果要确保图像不超过特定大小以传送到内存有限的设备，jpegSize是一个有用的参数。

* 此参数以千字节为单位(`jpegSize=&lt;size_in_kilobytes&gt;`)。它定义图像投放允许的最大大小。
* `&jpegSize=` 与JPG压缩参数交互 `&qlt=`. 如果JPG响应具有指定的JPG压缩参数(`&qlt=`)不超过jpegSize值，则图像返回时为 `&qlt=` （按定义）。 否则， `&qlt=` 会逐渐减小，直到图像符合允许的最大尺寸，或者直到系统确定它不能符合并返回错误。

作为最佳实践，设置 `&jpegSize=` 并添加参数 `&qlt=` 如果您要将JPG映像传送到内存有限的设备。

## 最佳实践小结 {#best-practices-summary}

作为最佳实践，要获得较高的图像质量和较小的文件大小，请首先使用以下参数组合：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

在大多数情况下，此设置组合可生成出色的效果。

如果图像需要进一步优化，请先将 radius 设置为 0.2 或 0.3，以便逐渐微调锐化（USM 锐化）参数。然后，将 amount 从 1.75 逐渐增加至最大值 4（相当于 Photoshop 中的 400%）。检查是否达到所需的效果。

如果锐化效果仍然不能让您满意，请按小数位递增的方式增大 radius。对于每次递增，重新将 amount 从 1.75 逐渐增加至 4。重复此过程，直至达到所需效果。尽管采用上述值是创意工作室已经验证过的方法，但请记住，您也可以从其他值开始设置，并遵循其他策略。关于效果是否能让您满意，这是个主观性问题，因此进行结构化的试验很关键。

在实验过程中，以下一般建议有助于进一步优化您的工作流：

* 直接在URL上实时尝试并测试不同的参数。
* 作为最佳实践，请记住，您可以将Dynamic Media图像服务命令分组到图像预设中。 图像预设基本上是带有自定义预设名称的URL命令宏，例如 `$thumb_low$` 和 `&product_high$`. URL路径中的自定义预设名称会调用这些预设。 这类功能可帮助您针对网站中图像的不同使用模式来管理命令和质量设置，并缩短 URL 的整体长度。
* Experience Manager还提供了更高级的方法来调整图像质量，例如在摄取时应用锐化图像。 对于存在优化和优化渲染结果的选项的高级用例， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可以帮助您提供自定义的洞察信息和最佳实践。
