---
title: 配置Dynamic Media常规设置
description: 了解如何在Dynamic Media中管理“常规设置”。 您可以在此处设置发布服务器名称和源服务器名称，并设置图像覆盖选项。 还有一些默认的上传选项，用于对图像进行USM锐化，以及上传选项，用于了解您如何处理PostScript、Adobe Photoshop、PDF和Adobe Illustrator文件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: f5989e182ee0d9075251b582fa618af5efcb9f8a
workflow-type: tm+mt
source-wordcount: '2461'
ht-degree: 4%

---


# 配置Dynamic Media常规设置

配置 **[!UICONTROL Dynamic Media常规设置]** 仅在以下情况下可用：

* 您在Scene7模式下运行Dynamic Media。 请参阅 [在Scene7模式下启用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 您拥有 *现有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5.11或更高版本中。
* 您是具有管理员权限的Experience Manager系统管理员。

Dynamic Media常规设置适用于经验丰富的网站开发人员和程序员。 AdobeDynamic Media建议更改这些发布设置的用户熟悉Adobe Experience Manager上的Dynamic Media和基本成像技术。

在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

“Dynamic Media发布设置”页面可建立默认设置，以确定如何将资产从Dynamic MediaAdobe服务器交付到网站或应用程序。 如果未指定任何设置，AdobeDynamic Media服务器将根据Dynamic Media发布设置页面上配置的默认设置来传送资产。

另请参阅 [可选 — 设置和配置Dynamic Media - Scene7模式设置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) fpr更多可选配置任务。

>[!NOTE]
>
>在Adobe Experience Manager上从Dynamic Media Classic升级到Dynamic Media? “常规设置”页面和 [发布设置](/help/assets/dm-publish-settings.md) 页面中已预填充来自Dynamic Media Classic帐户的值。 例外是 **[!UICONTROL 默认上传选项]** 中。 这些值已处于Experience Manager中。 因此，您在下进行的任何更改 **[!UICONTROL 默认上传选项]**，则通过Experience Manager用户界面，在这五个选项卡的任意一个选项卡中，都会反映在Dynamic Media中，而不是Dynamic Media Classic中。 “常规设置”页面和 [发布设置](/help/assets/dm-publish-settings.md) 页面在Dynamic Media Classic和Dynamic Media之间Experience Manager。

**要配置Dynamic Media常规设置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在“服务器”页面中，将 **[!UICONTROL 已发布的服务器名称]** 和 **[!UICONTROL 源服务器名称]**，然后使用五个选项卡为图像编辑以及Postscript、Photoshop、PDF和Illustrator文件配置默认上传选项。

   * [服务器](#server-general-setting)
   * [上载到应用程序](#upload-to-application)
   * [图像编辑](#image-editing-tab) 选项卡
   * [PostScript](#postscript-tab) 选项卡
   * [Photoshop](#photoshop-tab) 选项卡
   * [PDF](#pdf-tab) 选项卡
   * [Illustrator](#illustrator-tab) 选项卡

   ![Dynamic Media“常规设置”页面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media“常规设置”页面，其中&#x200B;**[!UICONTROL 图像编辑]**选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

## 服务器 {#server-general-setting}

在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

| 选项 | 描述 |
| --- | --- |
| **[!UICONTROL 已发布的服务器名称]** | 必填.<br>名称必须使用 `https://` 在路径中。<br>此服务器是实时CDN（内容交付网络）服务器，用于特定于您帐户的所有系统生成URL调用。 请勿更改此服务器名称，除非Adobe技术支持部门指示您更改此名称。 |
| **[!UICONTROL 原始服务器名称]** | 必填.<br>此服务器仅用于质量保证测试。 除非Adobe技术支持部门指示您更改此服务器名称，否则请勿更改此服务器名称。 |

## 上载到应用程序 {#upload-to-application}

* **[!UICONTROL 覆盖图像]**

   AdobeDynamic Media不允许两个文件具有相同的名称。 每个项目的AdobeDynamic Media ID（图像名称减去文件扩展名）必须唯一。 因为这条规则， **[!UICONTROL 上传到应用程序]** 包含覆盖。 此选项的确切效果取决于您选择的指定的覆盖图像选项。 以下选项指定了如何上传替换图像：是替换原始图像，还是变为重复图像。 重复图像将重命名为 `-1`. 例如， `chair.tif` 已重命名 `chair-1.tif`. 这些选项会影响上传到与原始文件夹不同的文件夹的图像，或文件扩展名与原始文件不同的图像，例如JPG、TIF或PNG。

   | “覆盖图像”选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 覆盖当前文件夹中相同的基本名称/扩展名]** | 仅对新Dynamic Media帐户默认。<br>此选项是最严格的替换规则。 它要求您将替换图像上传到与原始图像相同的文件夹，并且替换图像的文件扩展名与原始图像相同。 如果不满足这些要求，则会创建重复项。 |
   | **[!UICONTROL 覆盖当前文件夹中相同的基本名称，无论扩展名是什么]** | 要求您将替换图像上传到与原始图像相同的文件夹，但文件扩展名可能与原始图像不同。 例如， chair.tif将取代chair.jpg。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称和扩展名进行覆盖]** | 要求替换图像的文件扩展名与原始图像相同（例如，chair.jpg必须替换chair.jpg，而不是chair.tif）。 但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新后的图像位于新文件夹中；在文件的原始位置中无法再找到该文件。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称（不论扩展名是什么）进行覆盖]** | 此选项是包含最广的替换规则。 您可以将替换图像上传到与原始图像不同的文件夹，上传文件扩展名不同的文件，然后替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将位于上传到的新文件夹中。 |

* **[!UICONTROL 保留裁切]**

   控制对任何现有手动裁剪定义的保留。

   另请参阅 `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 和 [重新处理AssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)，均在《Dynamic Media查看器参考指南》中。

## 默认上传选项 {#default-upload-options}

### “图像编辑”选项卡 {#image-editing-tab}

此滤镜允许您对最终缩减采样图像微调锐化滤镜效果。 它有助于您控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。

“USM锐化”效果使用的选项与Photoshop的“USM锐化”滤镜的选项相同。 与名称所暗示的相反，USM锐化是一种锐化滤镜。

| 钝化蒙版选项 | 描述 |
| --- | --- |
| **[!UICONTROL 数量]** | 必填.<br>控制应用于边缘像素的对比度量。<br>把它看作效果的强度。 在AdobeDynamic Media中，“钝化蒙版”的量值与在Adobe Photoshop中的量值之间的主要区别是，Photoshop的量范围在1%到500%之间。 而在AdobeDynamic Media中，值范围是 `0.0` to `5.0`. AdobeDynamic Media中的值为5.0大致相当于Photoshop中的500%;值0.9等于90%，依此类推。 |
| **[!UICONTROL 半径]** | 必填.<br>控制效果的半径。<br>值范围为 `0` to `250`. 该效果在图像中的所有像素上运行，并在所有方向上从所有像素辐射出来。 半径以像素为单位进行测量。 例如，要对2000 x 2000像素图像和500 x 500像素图像获得类似的锐化效果，应在2000 x 2000像素图像上设置两个像素的半径。 然后，在500 x 500像素图像上设置一个像素的半径值。 像素数较多的图像会使用较大的值。 |
| **[!UICONTROL 阈值]** | 必填.<br>阈值是在应用“USM锐化”滤镜时忽略的对比度范围。 此效果很重要，因此在使用此滤镜时，图像不会引入“杂色”。 值范围为 `0` - `255`，灰度图像中的亮度步骤数。 `0`=黑色， `128`=50%灰色和 `255`=white。<br>阈值 `12` 忽略细微的变化是肤色亮度以避免添加杂色，但仍会为对比区域添加边缘对比度，如睫毛与皮肤相遇的地方。<br>如果您有某人的脸部照片，则USM锐化会影响图像的禁忌部分。 例如，睫毛和皮肤会聚以创建明显的对比度区域，以及平滑的皮肤本身。 即使最平滑的皮肤也表现出亮度值的细微变化。 如果不使用阈值，滤镜会突出皮肤像素中的这些细微更改。 反过来，产生噪声和不期望的效果，同时增加睫毛的对比度，增强锐度。<br>为避免出现此问题，引入了一个阈值，用于告知滤镜忽略不会显着更改对比度的像素，如平滑的皮肤。<br>在前面显示的拉链图中，请注意拉链旁边的纹理。 由于阈值过低，无法抑制噪声，出现图像噪声。 |
| **[!UICONTROL 单色]** | 选择以使图像亮度（强度）钝化。<br>取消选择以单独对每个颜色组件进行锐化。 |

另请参阅 [在AdobeDynamic Media和图像服务器上锐化图像](/help/assets/assets/sharpening_images.pdf).

### “PostScript”选项卡 {#postscript-tab}

您可以栅格化Adobe PostScript®文件、维护透明背景、选择分辨率和选择色彩空间。

您可以在Adobe PostScript®(EPS)AdobeDynamic Media中使用。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传PostScript(EPS)图像文件时，可以采用各种方式设置它们的格式。 您可以栅格化文件、维护透明背景、选择分辨率和选择色彩空间。

| PostScript选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”(Rasterize)将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |

### Photoshop选项卡 {#photoshop-tab}

您可以从Adobe® Photoshop®文件创建模板、维护图层、指定图层的命名方式、提取文本，以及指定图像如何定位到模板中。

| Photoshop选项 | 描述 |
| --- | --- |
| **[!UICONTROL 保持层]** | 将PSD中的层（如果有）拆分为单个资产。 资产层与PSD保持关联。 可通过在“详细信息视图”中打开PSD文件并选择层面板来查看它们。 请参阅查看和编辑PSD文件中的图层。 |
| **[!UICONTROL 创建模板]** | 从PSD文件的层创建模板。 |
| **[!UICONTROL 提取文本]** | 提取文本，以便用户在查看器中搜索文本。 |
| **[!UICONTROL 将图层扩展至背景大小]** | 将撕裂图像层的大小扩展到背景层的大小。 |
| **[!UICONTROL 图层命名]** | 将撕裂图像层的大小扩展到背景层的大小。<br>· **[!UICONTROL 层名称]**  — 将图像命名为PSD文件中图层名称之后的图像。 例如，原始PSD文件中名为“价格标签”的层将变为名为“价格标签”的图像。 但是，如果PSD文件中的层名称是默认的Photoshop层名称（背景、层1、层2等），则图像将以其在PSD文件中的层编号命名。 <br>· **[!UICONTROL Photoshop和图层编号]**  — 在PSD文件中将图像命名为图层编号之后，而忽略原始图层名称。 图像以Photoshop文件名和附加的图层编号命名。 例如，文件的第二层，名为 `Spring Ad.psd` 已命名 `Spring Ad_2` 即使它在Photoshop中具有非默认名称。<br>· **[!UICONTROL Photoshop和层名称]**  — 在PSD文件后面命名图像，后跟层名或层号。 如果PSD文件中的层名称是默认的Photoshop层名称，则使用层编号。 例如，名为 `Price Tag` 在名为的PSD文件中 `SpringAd` 已命名 `Spring Ad_Price Tag`. 将调用缺省名称为Layer 2的层 `Spring Ad_2`. |
| **[!UICONTROL 锚点]** | 指定如何在模板中锚定图像，这些模板是从PSD文件生成的分层组合生成的。 默认情况下，锚点为中心。 无论替换图像的长宽比如何，中心锚点都允许替换图像最好地填充相同的空间。 引用模板和使用参数替换时，具有不同方面的图像会替换此图像，因此，当引用模板和使用参数替换时，会有效地占用相同的空间。 如果您的应用程序需要替换图像来填充模板中分配的空间，请更改为其他设置。 |

### PDF选项卡 {#pdf-tab}

您可以选择将文件栅格化、提取搜索词和链接、设置分辨率并选择色彩空间。

| PDF选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | · **[!UICONTROL 无]**  — 未完成PDF处理。<br>· **[!UICONTROL 缩略图]**  — 拆分PDF文件中的每个页面，并将其转换为缩略图。<br> · **[!UICONTROL 光栅化]**  — 拆开PDF文件中的页面，并将矢量图形转换为位图图像。 要创建eCatalog，请选择此选项。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 无]**  — 未从PDF中提取搜索词或链接。<br>· **[!UICONTROL 搜索词]**  — 从PDF文件中提取搜索词，以便在eCatalog查看器中按关键字搜索文件。<br>· **[!UICONTROL 链接]**  — 从PDF文件中提取链接，并将其转换为在eCatalog查看器中使用的图像映射。<br>· **[!UICONTROL 搜索词和链接]**  — 提取搜索词和链接，以在eCatalog查看器中使用。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认为 150。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 维护PDF文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |

### Illustrator选项卡 {#illustrator-tab}

您可以栅格化Adobe Illustrator®文件、维护透明背景、选择分辨率和选择色彩空间。

您可以在AdobeDynamic Media中使用Adobe® Illustrator®(AI)文件。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传Illustrator(AI)图像文件时，可以采用各种方式设置它们的格式。 您可以栅格化文件、维护透明背景、选择分辨率和选择色彩空间。 在上传屏幕上的上传屏幕上，“上传作业选项”框中的“PostScript选项”和“Illustrator选项”下提供了用于设置PostScript和Illustrator文件格式的选项。


| Illustrator选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”(Rasterize)将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |
