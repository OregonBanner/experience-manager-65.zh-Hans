---
title: Dynamic Media 图像配置文件
description: 创建包含USM锐化设置、智能裁剪或智能色板设置（或同时包含这两种设置）的图像配置文件，然后将该配置文件应用到图像资产的文件夹。
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: bbb64f44c80e96bafcd53277f6d753d84acf5189
workflow-type: tm+mt
source-wordcount: '3047'
ht-degree: 6%

---

# Dynamic Media 图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像配置文件应用到文件夹，在上传时自动裁剪图像。

>[!IMPORTANT]
>
>·智能裁剪仅在Dynamic Media - Scene7模式下可用。
·图像配置文件不适用于PDF、动画GIF或INDD(Adobe InDesign)文件。

## 裁切选项 {#crop-options}

在图像上实施智能裁剪时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 规定的限制 |
| --- | --- | --- |
| 每个图像的智能作物数量 | 5 | 100 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

智能裁切坐标取决于宽高比。 对于图像配置文件中的各种智能裁剪设置，如果图像配置文件中添加的维度的宽高比相同，则会将相同的宽高比发送到Dynamic Media。 Adobe建议您使用相同的裁剪区域。 这样做可确保对图像配置文件中使用的不同维度不会产生任何影响。

您创建的每个智能裁剪生成都需要额外的处理。 例如，添加五个以上的智能裁剪长宽比可能会导致资产摄取速度缓慢。 它还会增加系统的负载。 由于您可以在文件夹级别应用智能裁剪，因此Adobe建议您在文件夹上使用智能裁剪 *仅* 需要的地方。

**在图像配置文件中定义智能裁剪的准则**
为了控制智能裁剪的使用情况，并优化农作物的加工时间和存储，Adobe建议遵循以下准则和提示：

* 避免创建宽度和高度值相同的重复智能裁剪配置文件。
* 根据裁剪尺寸而不是最终使用情况来命名智能裁剪。 这样做有助于优化在多个页面上使用单个维度的重复项。
* 为特定文件夹和子文件夹创建按页面/资产类型的图像配置文件，而不是应用到所有文件夹或所有资产的通用智能裁剪配置文件。
* 应用到子文件夹的图像配置文件会覆盖应用到该文件夹的图像配置文件。
* 为特定文件夹和子文件夹创建按页面/资产类型的图像配置文件，而不是应用到所有文件夹或所有资产的通用智能裁剪配置文件。
* 您应用到子文件夹的图像配置文件会覆盖应用到该文件夹的图像配置文件。
* 理想情况下，每张图像拥有10-15种智能作物，以优化屏幕比例和处理时间。

<!--
* Image assets that are going to have a smart crop applied to them must be a minimum of 50 x 50 pixels or larger. CQDOC-20087
* An Image Profile that contains duplicate smart crop dimensions is not permitted. CQDOC-20087
* Duplicate named Image Profiles that have smart crop options set are not permitted. CQDOC-20087
* Create page-wise/asset type-wise Image Profiles for specific folders and subfolders instead of a common smart crop profile that is applied to all folders or all assets.
* An Image Profile that you apply to subfolders overrides an Image Profile that is applied to the folder.
* Ideally, have 10-15 smart crops per image to optimize for screen ratios and processing time. -->
<!-- * Avoid creating duplicate smart crop profiles that have the same width and height values. 
* Name smart crops based on crop dimensions, not on end usage. Doing so helps to optimize for duplicates where a single dimension is used on multiple pages. -->

您有两个图像裁剪选项可供您选择。 您还可以选择自动创建颜色和图像色板，或跨目标分辨率保留裁剪内容。

>[!IMPORTANT]
·Adobe建议您查看任何生成的作物和色板，以确保它们与您的品牌和价值相关且适当。
·智能裁剪不支持CMYK图像格式。

| 选项 | 何时使用 | 描述 |
| --- | --- | --- |
| 像素裁剪 | 仅基于维度批量裁剪图像。 | 要使用此选项，请选择 **[!UICONTROL 像素裁剪]** 从“裁剪选项”下拉列表中。<br><br>要从图像的侧边进行裁剪，请输入要从图像的任意侧边或每侧进行裁剪的像素数。 裁剪图像的多少取决于图像文件中的ppi（像素/英寸）设置。<br><br>图像配置文件像素裁切按以下方式呈现：<br>·值包括顶部、底部、左侧和右侧。<br>·考虑左上角 `0,0` 像素裁切就从此计算。<br>·裁剪起点：左为X，上为Y<br>·水平计算：原始图像的水平像素尺寸减去“左”后减去“右”。<br>·垂直计算：垂直像素高度减去“顶部”，然后减去“底部”。<br><br>例如，假定您的图像为4000 x 3000像素。 您使用以下值：顶=250，底=500，左=300，右=700。<br><br>从左上角(300,250)使用填充空间(4000-300-700、3000-250-500或3000,2250)进行裁剪。 |
| 智能裁剪 | 根据图像的可视焦点批量裁剪图像。 | Smart Crop利用Adobe Sensei中人工智能的强大功能，快速批量自动裁剪图像。 智能裁剪可自动检测并裁剪到任何图像中的焦点以捕获预期的目标点，而无论屏幕大小如何。</p> <p>要使用智能裁剪，请选择 **[!UICONTROL 智能裁剪]** 从“裁剪选项”下拉列表中，然后在响应式图像裁剪的右侧，启用（打开）该功能。</p> <p>“大”、“中”和“小”的默认断点大小通常涵盖大多数图像在移动和平板电脑设备、台式机和横幅上使用的所有大小。 如果需要，您可以编辑默认名称“大”、“中”和“小”。</p> <p>要添加更多断点，请选择 **[!UICONTROL 添加裁剪]** 要删除裁剪，请选择垃圾箱图标。 |
| 颜色和图像样本 | 批量会为每个图像生成一个图像样本。 | **注意**:Dynamic Media Classic不支持智能色板。<br><br>自动从显示颜色或纹理的产品图像中定位并生成高质量样本。<br><br>要使用颜色和图像色板，请选择 **[!UICONTROL 智能裁剪]** 从“裁剪选项”下拉列表中，然后在“颜色”和“图像色板”的右侧，启用（打开）该功能。 在“宽度”和“高度”文本框中输入像素值。<br><br>虽然所有图像裁剪都可以从演绎版边栏中获取，但样本仅通过复制URL功能来使用。 使用您自己的查看组件在网站上渲染色板。 (此规则的例外是传送横幅。 Dynamic Media为轮播横幅中使用的色板提供查看组件。)<br><br>**使用图像色板**<br>&#x200B;图像样本的URL非常简单。 是：<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>where `:Swatch` 会附加到资产请求中。<br><br>**使用颜色色板**<br>&#x200B;要使用颜色色板，请 `req=userdata` 请求，其中包含以下内容：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的色板资产：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>下面是色板资产的相应 `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>的 `req=userdata` 响应如下：<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>您还可以请求 `req=userdata` XML或JSON格式的响应，如以下各个URL示例所示：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意：** 创建您自己的WCM组件以请求颜色样本并解析 `SmartSwatchColor` 属性，由24位RGB十六进制值表示。<br><br>另请参阅 [`userdata` （在查看器参考指南中）](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## USM 锐化 {#unsharp-mask}

使用&#x200B;**[!UICONTROL 钝化蒙版]**&#x200B;对最终取样缩小的图像微调锐化滤镜效果。您可以控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。 此效果使用的选项与Adobe Photoshop的 *钝化蒙版* 过滤器。

>[!NOTE]
USM锐化仅应用于PTIFF（金字塔tiff）中缩减采样率超过50%的缩小演绎版。 这意味着ptiff中最大大小的演绎版不会受到USM锐化的影响，而较小的演绎版（如缩略图）会发生更改（并显示USM锐化）。

在 **[!UICONTROL 钝化蒙版]**，则具有以下筛选选项：

| 选项 | 描述 |
| --- | --- |
| 数量 | 控制应用于边缘像素的对比度量。 默认值为1.75。对于高分辨率图像，最高可将其增加到5。 将“数量”视为过滤强度的度量。 范围为0-5。 |
| 半径 | 确定边缘像素周围影响锐化的像素数量。对于高分辨率图像，输入 1 到 2。低值仅锐化边缘像素；高值锐化较宽范围的像素。正确的值取决于图像大小。默认值为0.2。范围为0-250。 |
| 阈值 | 确定在应用USM锐化滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入杂色，请尝试使用0到255之间的值。 |

有关锐化的描述，请参阅 [锐化图像](/help/assets/assets/sharpening_images.pdf).

## 创建Dynamic Media图像配置文件 {#creating-image-profiles}

要为其他资产类型定义高级处理参数，请参阅 [配置资产处理](config-dms7.md#configuring-asset-processing).

请参阅 [用于处理元数据、图像和视频的配置文件](processing-profiles.md).

另请参阅 [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).

**要创建Dynamic Media图像配置文件，请执行以下操作：**

1. 选择Adobe Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择 **[!UICONTROL 创建]** 以便您添加图像配置文件。
1. 输入USM锐化、裁切或色板的配置文件名称和值，或同时输入两者。

   使用特定于其预期目的的配置文件名称。 例如，如果您要创建仅生成色板的配置文件 — 即，禁用（关闭）智能裁剪，启用（打开）颜色和图像色板 — 使用配置文件名称“智能色板”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![农作物](assets/crop.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。新创建的用户档案将显示在可用用户档案列表中。

## 编辑或删除Dynamic Media图像配置文件 {#editing-or-deleting-image-profiles}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要编辑或删除的图像配置文件。 要编辑它，请选择 **[!UICONTROL 编辑图像配置文件]**. 要删除它，请选择 **[!UICONTROL 删除图像配置文件]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果进行编辑，请保存更改。 如果删除，请确认您要删除该用户档案。

## 将Dynamic Media图像配置文件应用到文件夹 {#applying-an-image-profile-to-folders}

当您将图像配置文件分配给文件夹后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。 此工作流意味着您只能向文件夹分配一个图像配置文件。 因此，请仔细考虑上传、存储、使用和存档资产所在的文件夹结构。

如果您为文件夹分配了其他图像配置文件，则新配置文件会覆盖之前的配置文件。 以前存在的文件夹资产将保持不变。 新配置文件会应用于稍后添加到文件夹的资产。

在用户界面中，如果文件夹分配了配置文件，则会使用卡中显示的配置文件名称来指示该文件夹。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像配置文件应用到特定文件夹或全局应用到所有资产。

您可以重新处理文件夹中的资产，该文件夹中已有您稍后更改的图像配置文件。 请参阅 [编辑文件夹中的资产处理配置文件后，会重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

### 将Dynamic Media图像配置文件应用到特定文件夹 {#applying-image-profiles-to-specific-folders}

您可以在 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中， **[!UICONTROL 属性]**. 本节将介绍这两种将图像配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅 [编辑文件夹中的资产处理配置文件后，会重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

#### 将Dynamic Media图像配置文件从配置文件用户界面应用到文件夹 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要应用于一个或多个文件夹的图像配置文件。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择 **[!UICONTROL 将处理配置文件应用到文件夹]** ，然后选择一个或多个用于接收新上传资产的文件夹，然后选择 **[!UICONTROL 应用]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 将Dynamic Media图像配置文件从属性应用到文件夹 {#applying-image-profiles-to-folders-from-properties}

1. 选择Experience League徽标并导航到 **[!UICONTROL 资产]**. 然后，导航到要将图像配置文件应用到的文件夹的父文件夹。
1. 在文件夹中，选择复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。 从 **[!UICONTROL 配置文件名称]** 下拉列表中，选择用户档案，然后选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像配置文件 {#applying-an-image-profile-globally}

除了将配置文件应用到文件夹之外，您还可以全局应用一个配置文件，以便任何文件夹中上传到Experience Manager资产的任何内容都会应用选定的配置文件。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅 [编辑文件夹中的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

**要全局应用Dynamic Media图像配置文件，请执行以下操作：**

1. 执行下列操作之一：

   * 导航到 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` ，然后应用相应的用户档案并选择 **[!UICONTROL 保存]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`.

      添加属性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 选择 **[!UICONTROL 全部保存]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 编辑单个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
·智能裁剪仅在Dynamic Media - Scene7模式下可用。

您可以手动重新调整图像的智能裁剪窗口大小或调整其大小，以进一步优化其焦点。

编辑智能裁剪并保存后，所做的更改会传播到您对特定图像使用裁剪的所有位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

另请参阅 [编辑多幅图像的智能裁切或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**要编辑单个图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁剪或智能色板图像配置文件的文件夹。

1. 选择文件夹，以便打开其内容。
1. 选择要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，选择 **[!UICONTROL 智能裁剪]**.

1. 执行以下任一操作：

   * 在页面的右上角附近，向左或向右拖动滑块条以分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁剪或色板可查看区域的大小。
   * 在图像上，将框/色板拖到新位置。 您只能编辑图像色板；颜色色板是静态的。
   * 在图像上方，选择  **[!UICONTROL 还原]** 撤消所有编辑并恢复原始裁剪或色板。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** ，以返回到资产文件夹。

## 编辑多幅图像的智能裁切或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
·智能裁剪仅在Dynamic Media - Scene7模式下可用。

将包含智能裁剪的图像配置文件应用到文件夹后，该文件夹中的所有图像都会对其应用裁剪。 如果需要，您可以 *手动* 重新调整多幅图像中智能裁剪窗口的大小或调整其大小，以进一步优化其焦点。

编辑智能裁剪并保存后，所做的更改会传播到您对特定图像使用裁剪的所有位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

**要编辑多幅图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁剪或智能色板图像配置文件的文件夹。
1. 在文件夹中，选择 **[!UICONTROL 更多操作]** (...)图标，然后选择 **[!UICONTROL 智能裁剪]**.

1. 在 **[!UICONTROL 编辑智能裁剪]** ，请执行以下任一操作：

   * 调整页面上图像的查看大小。

      在断点名称下拉列表的右侧，向左或向右拖动滑块以更改可查看图像显示的大小。

      ![edit_smart_crobs_sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称过滤可查看图像的列表。 在以下示例中，图像是在断点名称“Medium”上过滤的。

      在页面的右上角附近，从下拉列表中，选择一个断点名称以过滤您看到的图像。 （请参阅上图。）

      ![edit_smart_crobs_dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行以下任一操作：

      * 如果图像仅具有智能裁切或智能色板，则在图像上，拖动裁切框的角手柄以调整裁切可查看区域的大小。
      * 如果图像同时具有智能裁切和智能色板，则在图像上，拖动裁切框的角手柄以调整裁切可查看区域的大小。 或者，选择图像下方的智能色板（颜色色板为静态色板），然后拖动裁剪框的角手柄以调整色板可查看区域的大小。

      ![调整图像的智能裁剪大小](assets/edit_smart_crops-resize.png)

   * 移动智能裁剪框。 执行以下任一操作：

      * 如果图像仅具有智能裁剪或智能色板，则在图像上将裁剪框拖到新位置。
      * 如果图像同时具有智能裁切和智能色板，则在图像上，将智能裁切框拖到新位置。 或者，选择图像下方的智能色板（颜色色板为静态色板），然后将智能色板裁剪框拖到新位置。

      ![edit_smart_crobs_move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

      选择 **[!UICONTROL 还原]** 图像上方。

      ![edit_smart_crobs_revert](assets/edit_smart_crops-revert.png)



1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** ，以返回到资产文件夹。

## 将Dynamic Media图像配置文件从文件夹删除 {#removing-an-image-profile-from-folders}

当您将图像配置文件从文件夹删除后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。 但是，对文件夹中已发生的文件的任何处理均将保持不变。

您可以从 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中， **[!UICONTROL 属性]**. 本节将介绍这两种将图像配置文件从文件夹删除的方法。

### 通过Profiles用户界面将Dynamic Media图像配置文件从文件夹删除 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要从一个或多个文件夹中删除的图像配置文件。
1. 选择 **[!UICONTROL 从文件夹删除处理配置文件]** ，然后选择一个或多个要从中删除配置文件的文件夹，然后选择 **[!UICONTROL 删除]**.

   您可以确认图像配置文件不再应用于文件夹，因为文件夹名称的下方不再显示该名称。

### 通过属性将Dynamic Media图像配置文件从文件夹删除 {#removing-image-profiles-from-folders-via-properties}

1. 选择Experience Manager徽标并导航 **[!UICONTROL 资产]** ，然后转到要从中删除图像配置文件的文件夹。
1. 在文件夹中，选择复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。
1. 从 **[!UICONTROL 配置文件名称]** 下拉列表中，选择 **[!UICONTROL 无]**，然后选择 **[!UICONTROL 保存并关闭]**.

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
