---
title: 配置Dynamic Media常规设置
description: 了解如何在Dynamic Media中管理常规设置。 您可以在此处设置发布服务器名称和原始服务器名称，并设置图像覆盖选项。 此外，还有用于图像钝化蒙版的默认上传选项，以及用于指定如何处理PostScript、Adobe Photoshop、PDF和Adobe Illustrator文件的上传选项。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
source-git-commit: 9c548dbc0157607adda5ed76cab8ef970588e1e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 4%

---

# 配置Dynamic Media常规设置

配置 **[!UICONTROL Dynamic Media常规设置]** 仅在以下情况下可用：

* 您正在以Scene7模式运行Dynamic Media。 参见 [在Scene7模式下启用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 您有一个 *现有* **[!UICONTROL Dynamic Media配置]** (in **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5.11或更高版本中。 参见 [在Cloud Services中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* 您是具有管理员权限的Experience Manager系统管理员。

Dynamic Media常规设置旨在供经验丰富的网站开发人员和程序员使用。 AdobeDynamic Media建议更改这些发布设置的用户熟悉Adobe Experience Manager上的Dynamic Media和基本图像技术。

在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

“Dynamic Media发布设置”页面可建立默认设置，以确定如何将资源从AdobeDynamic Media服务器传递到网站或应用程序。 如果未指定设置，则AdobeDynamic Media服务器会根据“Dynamic Media发布设置”页面上配置的默认设置交付资源。

另请参阅 [可选 — 设置和配置Dynamic Media - Scene7模式设置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 了解更多可选配置任务。

>[!NOTE]
>
>在Adobe Experience Manager上从Dynamic Media Classic升级到Dynamic Media？ “常规设置”页面和 [发布设置](/help/assets/dm-publish-settings.md) Dynamic Media中的页面会预填充从您的Dynamic Media Classic帐户中获取的值。 例外情况是 **[!UICONTROL 默认上传选项]** 区域。 这些值已在Experience Manager中。 因此，您对以下内容所做的任何更改 **[!UICONTROL 默认上传选项]**&#x200B;通过Experience Manager用户界面，这五个选项卡中的任何一个都会反映在Dynamic Media中，而不是Dynamic Media Classic中。 “常规设置”页面和 [发布设置](/help/assets/dm-publish-settings.md) 页面会在Experience Manager时在Dynamic Media Classic和Dynamic Media之间维护。

**要配置Dynamic Media常规设置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在“服务器”页中，设置您的 **[!UICONTROL 已发布的服务器名称]** 和 **[!UICONTROL 源服务器名称]**，然后使用五个选项卡为“图像编辑”以及Postscript、Photoshop、PDF和Illustrator文件配置默认上传选项。

   * [服务器](#server-general-setting)
   * [上载到应用程序](#upload-to-application)
   * [图像编辑](#image-editing-tab) 选项卡
   * [PostScript](#postscript-tab) 选项卡
   * [Photoshop](#photoshop-tab) 选项卡
   * [PDF](#pdf-tab) 选项卡
   * [Illustrator](#illustrator-tab) 选项卡

   ![“Dynamic Media常规设置”页面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media的“常规设置”页面，带有&#x200B;**[!UICONTROL 图像编辑]**已选择选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

## 服务器 {#server-general-setting}

在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

| 选项 | 描述 |
| --- | --- |
| **[!UICONTROL 已发布的服务器名称]** | 必填.<br>名称必须使用 `https://` 在路径中。<br>此服务器是特定于您的帐户的所有系统生成URL调用中使用的实时CDN（内容分发网络）服务器。 请勿更改此服务器名称，除非Adobe技术支持指示您这样做。 |
| **[!UICONTROL 原始服务器名称]** | 必填.<br>此服务器仅用于质量保证测试。 除非经Adobe技术支持指示，否则请勿更改此服务器名称。 |

## 上载到应用程序 {#upload-to-application}

* **[!UICONTROL 覆盖图像]**

   AdobeDynamic Media不允许两个文件具有相同的名称。 每个项目的AdobeDynamic Media ID（图像名称减去文件扩展名）必须是唯一的。 因为这个规则， **[!UICONTROL 上载到应用程序]** 具有覆盖。 此选项的确切效果取决于您选择的指定覆盖图像选项。 这些选项指定如何上载替换图像：替换原始图像还是成为重复图像。 使用重命名重复图像 `-1`. 例如， `chair.tif` 已重命名 `chair-1.tif`. 这些选项会影响上传到与原始文件不同的文件夹中的图像，或者文件扩展名与原始文件扩展名不同的图像，例如JPG、TIF或PNG。

   >[!NOTE]
   >
   >要保持与Experience Manager的一致性，请选择覆盖图像选项 **[!UICONTROL 在当前文件夹内，使用相同的基本名称/扩展名进行覆盖]**.

   | “覆盖图像”选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 覆盖当前文件夹中相同的基本名称/扩展名]** | *默认* 仅用于新的Dynamic Media帐户。<br>此选项是最严格的更换规则。 它要求您将替换图像上传到与原始图像相同的文件夹，并且替换图像具有与原始图像相同的文件扩展名。 如果不满足这些要求，则会创建副本。<br>*要与Experience Manager保持一致，请选择此选项*. |
   | **[!UICONTROL 覆盖当前文件夹中相同的基本名称，不区分扩展名]** | 要求您将替换图像上传到与原始图像相同的文件夹，但文件扩展名可能与原始图像不同。 例如，chair.tif将取代chair.jpg。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称和扩展名进行覆盖]** | 要求替换图像具有与原始图像相同的文件扩展名（例如，chair.jpg必须替换chair.jpg，而不是chair.tif）。 但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新的图像驻留在新文件夹中；无法再在其原始位置找到该文件。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称（不区分扩展名）进行覆盖]** | 此选项是最具包容性的替换规则。 您可以将替换图像上载到与原始图像不同的文件夹，上载文件扩展名不同的文件，然后替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将驻留在将其上载到的新文件夹中。 |

* **[!UICONTROL 保留裁切]**

   控制任何现有手动裁切定义的保留。

   另请参阅 `preserveCrop` 在 [UploadPost作业](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 和 [重新处理资产作业](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)，两者均在Dynamic Media查看器参考指南中。

## 默认上传选项 {#default-upload-options}

### “图像编辑”选项卡 {#image-editing-tab}

通过此滤镜，可以对最终取样缩小的图像微调锐化滤镜效果。 它有助于控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。

“钝化蒙版”效果使用与Photoshop的“钝化蒙版”滤镜相同的选项。 与名称所暗示的相反，“USM锐化”是一种锐化滤镜。

| “钝化蒙版”选项 | 描述 |
| --- | --- |
| **[!UICONTROL 数量]** | 必填.<br>控制应用于边缘像素的对比度数量。<br>把它想成是效果的强度。 AdobeDynamic Media中“钝化蒙版”的量值与Adobe Photoshop中量值的主要区别在于，Photoshop具有1%到500%的量范围。 而在AdobeDynamic Media中，值范围是 `0.0` 到 `5.0`. 在AdobeDynamic Media中，值5.0大致相当于Photoshop中的500%；值0.9相当于90%，依此类推。 |
| **[!UICONTROL 半径]** | 必填.<br>控制效果的半径。<br>值范围是 `0` 到 `250`. 该效果在图像中的所有像素上运行，并从所有像素向各个方向辐射。 半径以像素为单位。 例如，要对2000 x 2000像素图像和500 x 500像素图像获得类似的锐化效果，可以在2000 x 2000像素图像上将半径设置为2像素。 然后，在500 x 500像素图像上设置一个像素的半径值。 较大的值适用于像素较多的图像。 |
| **[!UICONTROL 阈值]** | 必填.<br>阈值是应用“钝化蒙版”滤镜时忽略的对比度范围。 这种效果非常重要，因此使用此滤镜时，图像不会引入“杂色”。 值范围是 `0` - `255`，灰度图像中的亮度步骤数。 `0`=black， `128`=50%灰色和 `255`=white.<br>阈值 `12` 忽略肤色亮度的细微变化，以避免添加杂色，但仍然为对比区域（如睫毛与皮肤相遇的地方）添加边缘对比度。<br>如果您有某个人的面部照片，则“钝化蒙版”会影响图像的对比度部分。 例如，睫毛和皮肤相遇可产生明显的对比区域，而皮肤本身光滑。 即使最平滑的皮肤也会表现出亮度值的细微变化。 如果不使用阈值，则滤镜会强调外观像素中的这些细微变化。 反过来，在增加睫毛上的对比度的同时，产生噪音和不想要的效果，增强锐度。<br>为了避免此问题，引入了一个阈值，该阈值可告知滤镜忽略对比度没有显着变化的像素，如平滑外观。<br>在前面显示的拉链图形中，请注意拉链旁边的纹理。 由于阈值过低，图像噪声难以抑制。 |
| **[!UICONTROL 单色]** | 选择可钝化蒙版图像亮度（强度）。<br>取消选择可单独对每个颜色分量进行钝化蒙版。 |

另请参阅 [锐化AdobeDynamic Media和图像服务器上的图像](/help/assets/assets/sharpening_images.pdf).

### “PostScript”选项卡 {#postscript-tab}

可以栅格化Adobe PostScript®文件、保持透明背景、选择分辨率以及选择颜色空间。

您可以在AdobeDynamic Media中使用Adobe PostScript® (EPS)文件。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传PostScript (EPS)图像文件时，可以通过各种方式设置其格式。 您可以栅格化文件、保持透明背景、选择分辨率以及选择颜色空间。

| PostScript选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”以将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的颜色空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK颜色空间。<br>· **[!UICONTROL 强制为灰度]**  — 转换为灰度颜色空间。 |

### “Photoshop”选项卡 {#photoshop-tab}

您可以从Adobe®Photoshop®文件创建模板、维护图层、指定图层的命名方式、提取文本以及指定将图像锚定到模板中的方式。

| Photoshop选项 | 描述 |
| --- | --- |
| **[!UICONTROL 保持层]** | 将PSD中的图层（如果有）拆分为单独的资源。 资源层仍与PSD相关联。 通过在“详细视图”中打开PSD文件并选择图层面板来查看它们。 请参阅在PSD文件中查看和编辑图层。 |
| **[!UICONTROL 创建模板]** | 从PSD文件中的图层创建模板。 |
| **[!UICONTROL 提取文本]** | 提取文本，以便用户能够在查看器中搜索文本。 |
| **[!UICONTROL 将图层扩展至背景大小]** | 将翻录图像图层的大小扩展到背景图层的大小。 |
| **[!UICONTROL 图层命名]** | 将翻录图像图层的大小扩展到背景图层的大小。<br>· **[!UICONTROL 图层名称]**  — 在PSD文件中将图像命名为图层名称后的名称。 例如，原始PSD文件中名为“Price Tag”的图层会变成名为“Price Tag”的图像。 但是，如果PSD文件中的图层名称是默认的Photoshop图层名称（“背景”、“图层1”、“图层2”等），则图像将根据PSD文件中的图层编号进行命名。 <br>· **[!UICONTROL Photoshop和图层编号]**  — 将图像命名为PSD文件中的图层编号后名称，而忽略原始图层名称。 图像使用Photoshop文件名和附加的图层编号进行命名。 例如，文件的第二层，称为 `Spring Ad.psd` 已命名 `Spring Ad_2` 即使它在Photoshop中具有非默认名称。<br>· **[!UICONTROL Photoshop和图层名称]**  — 在PSD文件后面加上图层名称或图层编号来命名图像。 如果PSD文件中的图层名称是默认的Photoshop图层名称，则使用图层编号。 例如，一个名为的层 `Price Tag` 在名为的PSD文件中 `SpringAd` 已命名 `Spring Ad_Price Tag`. 缺省名称为Layer 2的层称为 `Spring Ad_2`. |
| **[!UICONTROL 锚点]** | 指定如何在模板中定位图像，该模板是根据PSD文件生成的图层合成生成的。 默认情况下，锚点是中心。 中心锚点允许替换图像以最佳方式填充相同的空间，而不管替换图像的长宽比如何。 当引用模板并使用参数替换时，替换此图像的不同方面的图像有效地占用了相同的空间。 如果您的应用程序要求替换图像填充模板中分配的空间，请更改为其他设置。 |

### “PDF”选项卡 {#pdf-tab}

您可以选择栅格化文件、提取搜索词和链接、设置分辨率以及选择颜色空间。

| PDF选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | · **[!UICONTROL 无]**  — 不处理PDF。<br>· **[!UICONTROL 缩略图]**  — 翻录PDF文件中的每页，并将其转换为缩略图图像。<br> · **[!UICONTROL 栅格化]**  — 翻录PDF文件中的页面，并将矢量图形转换为位图图像。 要创建eCatalog，请选择此选项。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 无]**  — 未从PDF中提取搜索词或链接。<br>· **[!UICONTROL 搜索词]**  — 从PDF文件中提取搜索词，以便在eCatalog查看器中按关键字搜索该文件。<br>· **[!UICONTROL 链接]**  — 从PDF文件中提取链接，并将其转换为eCatalog查看器中使用的图像映射。<br>· **[!UICONTROL 搜索词和链接]**  — 提取搜索词和链接以在eCatalog查看器中使用。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认为 150。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留PDF文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK颜色空间。<br>· **[!UICONTROL 强制为灰度]**  — 转换为灰度颜色空间。 |

### “Illustrator”选项卡 {#illustrator-tab}

可以栅格化Adobe Illustrator®文件、保持透明背景、选择分辨率以及选择颜色空间。

您可以在AdobeDynamic Media中使用Adobe® Illustrator® (AI)文件。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传Illustrator (AI)图像文件时，可以通过各种方式设置其格式。 您可以栅格化文件、保持透明背景、选择分辨率以及选择颜色空间。 用于格式化PostScript和Illustrator文件的选项在“上传作业选项”框中的“PostScript选项”和“Illustrator选项”下的上传屏幕上可用。


| Illustrator选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”以将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的颜色空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK颜色空间。<br>· **[!UICONTROL 强制为灰度]**  — 转换为灰度颜色空间。 |
