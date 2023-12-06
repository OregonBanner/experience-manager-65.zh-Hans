---
title: 在Dynamic Media中优化图像质量的最佳实践
description: 了解在Dynamic Media中优化图像质量的最佳实践
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 4%

---

# 在Dynamic Media中优化图像质量的最佳实践 {#best-practices-for-optimizing-the-quality-of-your-images}

优化图像质量可能是一个耗时的过程，因为许多因素有助于呈现可接受的结果。 结果部分具有主观性，因为个人对图像质量的看法不同。 结构化试验是关键。

Adobe Experience Manager包括100多条Dynamic Media图像投放命令，用于调整和优化图像和渲染结果。 以下准则可帮助您使用一些基本命令和最佳实践来简化流程并快速获得良好结果。

## 图像格式的最佳实践(`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG或PNG是提供高品质图像并具备可管理大小和重量的最佳选择。
* 如果URL中未提供任何格式命令，则Dynamic Media图像投放默认为JPG进行投放。
* JPG按10:1的比例压缩，通常产生的图像文件较小。 PNG压缩的比例约为2:1，除非有时，例如当图像包含白色背景时。 不过，PNG文件通常比JPG文件大。
* JPG使用有损压缩，这意味着压缩期间会丢弃图片元素（像素）。 另一方面，PNG使用无损压缩。
* JPG压缩照片图像时通常比具有锐边和对比度的合成图像保真度更高。
* 如果图像包含透明度，请使用PNG，因为JPG不支持透明度。

作为图像格式的最佳实践，请从最常见的设置开始 `&fmt=JPG`.

## 图像大小的最佳实践 {#best-practices-for-image-size}

动态减小图像大小是最常见的任务之一。 它涉及指定大小，以及（可选）使用哪种缩减取样模式来缩减图像。

* 对于图像大小调整，最好且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或只是 `&hei=<value>`. 这些参数会根据长宽比自动设置图像宽度。
* `&resMode=<value>`控制用于缩减像素采样的算法。 开始于 `&resMode=sharp2`. 此值可提供最佳图像质量。 使用缩减像素取样时 `value =bilin` 速度越快，往往会导致伪像的锯齿。

作为调整图像大小的最佳实践，请使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 图像锐化的最佳实践 {#best-practices-for-image-sharpening}

图像锐化是控制网站上图像的最复杂方面，并且会产生许多错误。 请查阅以下有用资源，以详细了解锐化和USM锐化在Experience Manager中的工作方式：

最佳实践白皮书 [在Adobe Dynamic Media Classic中锐化图像](/help/assets/assets/sharpening_images.pdf) 这也适用于Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

通过Experience Manager，您可以在摄取和/或交付时锐化图像。 但是，通常只使用一种方法或另一种方法来锐化图像，但不能同时使用这两种方法来锐化。 通常，在交付、URL上锐化图像可产生最佳效果。

可以使用两种图像锐化方法：

* 简单锐化( `&op_sharpen`) — 与Photoshop中使用的锐化滤镜类似，简单锐化会在动态调整大小后对图像的最终视图应用基本锐化。 但是，此方法不可由用户配置。 除非需要，否则最佳实践为不使用&amp;op_sharpen。
* USM锐化( `&op_USM`) — 钝化蒙版是一种行业标准锐化滤镜。 最佳实践是遵循以下准则，使用钝化蒙版来锐化图像。 USM锐化允许您控制以下三个参数：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *数量&#x200B;*]**（0-5，效果强度。）
      * **[!UICONTROL *半径&#x200B;*]**（0-250，围绕锐化对象绘制的“锐化线”的宽度，以像素为单位。）

     请记住，参数半径和数量彼此对应。 减小半径可以通过增加量来补偿。 半径允许更细的控制，因为较低的值仅锐化边缘像素，而较高的值锐化较宽范围的像素。

      * **[!UICONTROL *阈值&#x200B;*]**（0-255，影响的敏感性。）

            此参数确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素，而滤镜会锐化这些像素。 **[!UICONTROL threshold]**参数有助于避免过度锐化颜色相似的区域，如肤色。 例如，阈值为12时，会忽略肤色亮度的细微变化，以避免添加“杂色”，同时仍会为高对比度区域添加边缘对比度，如睫毛与皮肤相遇的地方。
        
        有关如何设置这三个参数的更多信息（包括要与过滤器一起使用的最佳实践），请参阅以下资源：

        有关锐化图像的Experience Manager帮助主题。

        最佳实践白皮书 [在Adobe Dynamic Media Classic中锐化图像](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager还允许您控制第四个参数：单色(0,1)。 此参数确定是使用值0分别将钝化蒙版应用于每个颜色组件，还是使用值1将钝化蒙版应用于图像亮度/强度。

作为最佳实践，请从钝化蒙版半径参数开始。 可以开始使用的Radius设置如下：

* **[!UICONTROL 网站]** - 0.2-0.3像素
* **[!UICONTROL 照片打印(250-300 ppi)]** - 0.3-0.5像素
* **[!UICONTROL 胶印打印(266-300 ppi)]** - 0.7 - 1.0像素
* **[!UICONTROL 画布打印(150 ppi)]** - 1.5 - 2.0像素

逐渐将数量从1.75增加到4。 如果锐化仍不是您想要的方式，请将半径增加一个小数点，然后再次运行从1.75到4的锐化量。 根据需要重复执行上述步骤。

将单色参数设置保留为0。

### JPEG压缩的最佳实践(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此参数可控制JPG编码质量。 较高的值意味着较高质量的图像但文件大小较大；或者，较低的值意味着较低质量的图像但文件大小较小。 此参数的范围为0至100。
* 要优化质量，请勿将参数值设置为100。 设置90或95与100之间的差异几乎不可感知，但100却不必要地增加了图像文件的大小。 因此，要优化质量但避免图像文件变得过大，请设置 `qlt= value` 到90或95。
* 要优化较小的图像文件大小，但使图像质量保持在可接受的级别，请设置 `qlt= value` 到80。 值低于70到75会导致图像质量显着下降。
* 作为最佳实践，要保持中立，请将 `qlt= value` 到85岁时保持中立。
* 在中使用色度标志 `qlt=`

   * 此 `qlt=` 参数具有第二个设置，允许您使用值打开RGB色度缩减像素采样 `,1` 或使用值关闭 `,0`.
   * 为了保持简单，请从RGB色度缩减像素取样关闭开始(`,0`)。 此设置通常可以获得更好的图像质量，尤其是对于具有大量锐边和对比度的合成图像。

作为使用JPG压缩的最佳实践 `&qlt=85,0`.

## JPEG大小调整的最佳实践(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果要确保图像不超过特定大小，以便传送到内存有限的设备，jpegSize是一个很有用的参数。

* 此参数设置为KB (`jpegSize=&lt;size_in_kilobytes&gt;`)。 它定义图像投放允许的最大大小。
* `&jpegSize=` 与JPG压缩参数交互 `&qlt=`. 如果JPG响应具有指定的JPG压缩参数(`&qlt=`)不超过jpegSize值，则图像返回时为 `&qlt=` （按定义）。 否则， `&qlt=` 会逐渐减小，直到图像符合允许的最大尺寸，或者直到系统确定它不能符合并返回错误。

作为最佳实践，请设置 `&jpegSize=` 并添加参数 `&qlt=` 如果您要将JPG映像传送到内存有限的设备。

## 最佳实践摘要 {#best-practices-summary}

为了达到较高的图像质量和较小的文件大小，最好从以下参数组合开始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

这种设置组合可在大多数情况下产生卓越的效果。

如果图像需要进一步优化，请从设置为0.2或0.3的半径开始逐步微调锐化（钝化蒙版）参数。然后，逐渐将数量从1.75增加到最大值4(相当于Photoshop中的400%)。 检查是否达到了预期效果。

如果锐化结果仍然不令人满意，请以小数增量增加半径。 对于每增加一个小数，将数量重新调整为1.75，然后逐渐增加到4。 重复此过程，直到获得所需的结果。 虽然上述价值观是创意工作室已经验证的方法，但请记住，您可以从其他价值观开始，并遵循其他策略。 因此，结构化试验是关键，其结果是否满意是主观问题。

在实验过程中，以下一般建议可能会有助于进一步优化您的工作流：

* 尝试直接在URL上实时测试不同的参数。
* 作为最佳实践，请记住，您可以将Dynamic Media图像服务命令分组到图像预设中。 图像预设基本上是带有自定义预设名称的URL命令宏，例如 `$thumb_low$` 和 `&product_high$`. URL路径中的自定义预设名称将调用这些预设。 此功能可帮助您管理网站上图像不同使用模式的命令和质量设置，并缩短URL的总长度。
* Experience Manager还提供了更高级的方法来调整图像质量，例如在摄取时应用锐化图像。 对于存在优化渲染结果的选项的高级用例， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可以帮助您提供自定义的洞察信息和最佳实践。
