---
title: Dynamic Media 图像配置文件
description: 创建包含钝化蒙版和/或智能裁切或智能色板设置的图像配置文件，然后将配置文件应用到图像资源的文件夹。
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: bb0658ef33736587fbc191738d57cf586e5cba9d
workflow-type: tm+mt
source-wordcount: '3045'
ht-degree: 6%

---

# Dynamic Media 图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像配置文件应用到文件夹来在上传时自动裁切图像。

>[!IMPORTANT]
>
>·智能裁剪仅在Dynamic Media - Scene7模式下可用。
·图像配置文件不适用于PDF、动画GIF或INDD (Adobe InDesign)文件。

## 裁切选项 {#crop-options}

当您对图像实施智能裁剪时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| 每个图像的智能裁剪次数 | 5 | 100 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

智能裁剪坐标与纵横比相关。 对于图像配置文件中的各种智能裁剪设置，如果图像配置文件中添加的维度的宽高比相同，则会将相同的宽高比发送到Dynamic Media。 Adobe建议您使用相同的裁切区域。 这样做可确保对图像配置文件中使用的不同尺寸不产生任何影响。

您创建的每个智能裁剪生成都需要额外的处理。 例如，添加五个以上的智能裁切长宽比可能会导致资源摄取速度缓慢。 它还会导致系统负载增加。 由于您可以在文件夹级别应用智能裁切，因此Adobe建议您在文件夹上使用它 *仅限* 在需要的地方。

**定义图像配置文件中智能裁剪的准则**
为了控制智能裁切的使用，并优化裁切的处理时间和存储，Adobe建议以下准则和提示：

* 避免创建具有相同宽度和高度值的重复智能裁剪配置文件。
* 根据裁切维度而不是最终用途命名智能裁切。 这样做有助于优化在多个页面上使用单个维度的重复项。
* 为特定文件夹和子文件夹创建基于页面/资源类型的图像配置文件，而不是创建应用于所有文件夹或所有资源的通用智能裁剪配置文件。
* 应用于子文件夹的图像配置文件将覆盖应用于该文件夹的图像配置文件。
* 为特定文件夹和子文件夹创建页面/资源类型的图像配置文件，而不是创建应用于所有文件夹或所有资源的通用智能裁剪配置文件。
* 应用于子文件夹的图像配置文件将覆盖应用于该文件夹的图像配置文件。
* 理想情况下，每个图像应有10-15个智能裁剪，以优化屏幕比例和处理时间。

<!--
* Image assets that are going to have a smart crop applied to them must be a minimum of 50 x 50 pixels or larger. CQDOC-20087
* An Image Profile that contains duplicate smart crop dimensions is not permitted. CQDOC-20087
* Duplicate named Image Profiles that have smart crop options set are not permitted. CQDOC-20087
* Create page-wise/asset type-wise Image Profiles for specific folders and subfolders instead of a common smart crop profile that is applied to all folders or all assets.
* An Image Profile that you apply to subfolders overrides an Image Profile that is applied to the folder.
* Ideally, have 10-15 smart crops per image to optimize for screen ratios and processing time. -->
<!-- * Avoid creating duplicate smart crop profiles that have the same width and height values. 
* Name smart crops based on crop dimensions, not on end usage. Doing so helps to optimize for duplicates where a single dimension is used on multiple pages. -->

您有两个图像裁切选项可供选择：像素裁切或智能裁切。 您还可以选择自动创建颜色和图像样本。

>[!IMPORTANT]
·Adobe建议您查看任何生成的农作物和色板，以确保它们合适且与您的品牌和价值观相关。
·智能裁剪不支持CMYK图像格式。

| 选项 | 何时使用 | 描述 |
| --- | --- | --- |
| 像素裁剪 | 仅基于尺寸批量裁切图像。 | 要使用此选项，请选择 **[!UICONTROL 像素裁切]** “裁切选项”下拉列表中。<br><br>若要从图像的侧面裁切，请输入要从图像的任意侧面或每侧面裁切的像素数。 裁切图像的量取决于图像文件中的ppi（像素/英寸）设置。<br><br>图像配置文件像素裁剪通过以下方式渲染：<br>·值为Top、Bottom、Left和Right。<br>·考虑使用左上角 `0,0` 像素裁切是从此处计算的。<br>·裁切起点：左为X，上为Y<br>·水平计算：原始图像的水平像素尺寸减去“左”再减去“右”。<br>·垂直计算：垂直像素高度减“顶部”，然后减“底部”。<br><br>例如，假设您有一个4000 x 3000像素的图像。 可使用以下值：Top=250、Bottom=500、Left=300、Right=700。<br><br>从左上方(300,250)裁切，使用填充空间（4000-300-700、3000-250-500或3000,2250）。 |
| 智能裁剪 | 根据视觉焦点批量裁切图像。 | 智能裁剪利用Adobe Sensei中人工智能的强大功能快速批量自动裁剪图像。 智能裁切会自动检测并裁切到任何图像中的焦点以捕获预期的目标点，而不管屏幕大小如何。</p> <p>要使用智能裁切，请选择 **[!UICONTROL 智能裁剪]** 从裁切选项下拉列表中，然后到响应式图像裁切的右侧，启用（打开）该功能。</p> <p>大型、中型和小型的默认断点大小通常涵盖大部分图像在移动设备和平板电脑设备、台式机和横幅上使用的完整大小范围。 如果需要，可以编辑“大”、“中”和“小”的缺省名称。</p> <p>要添加更多断点，请选择 **[!UICONTROL 添加裁切]** 要删除裁切，请选择垃圾桶图标。 |
| 颜色和图像样本 | 批量生成每个图像的图像样本。 | **注释**：Dynamic Media Classic不支持智能色板。<br><br>从显示颜色或纹理的产品图像自动定位并生成高质量色板。<br><br>要使用颜色和图像样本，请选择 **[!UICONTROL 智能裁剪]** 从“裁剪选项”下拉列表中，然后在“颜色和图像样本”的右侧，启用（打开）该功能。 在“宽度”和“高度”文本框中输入像素值。<br><br>虽然所有图像裁剪都可以从“演绎版”边栏中使用，但样本只能通过“复制URL”功能使用。 使用您自己的查看组件渲染网站上的色板。 (此规则的例外是轮播横幅。 Dynamic Media为轮播横幅中使用的样本提供查看组件。)<br><br>**使用图像样本**<br>&#x200B;图像样本的URL很简单。 它是：<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>位置 `:Swatch` 会附加到资产请求中。<br><br>**使用色板**<br>&#x200B;要使用色板，请制作 `req=userdata` 请求包含以下内容：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的样本资源：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>下面是样本资产的对应项 `req=userdata` URL：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>此 `req=userdata` 响应如下：<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>您还可以请求 `req=userdata` XML或JSON格式的响应，如以下相应的URL示例所示：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意：** 创建您自己的WCM组件以请求颜色样本并解析 `SmartSwatchColor` 属性，由24位RGB的十六进制值表示。<br><br>另请参阅 [`userdata` 在查看器参考指南中](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## USM 锐化 {#unsharp-mask}

使用&#x200B;**[!UICONTROL 钝化蒙版]**&#x200B;对最终取样缩小的图像微调锐化滤镜效果。您可以控制效果的强度、效果的半径（以像素为单位）以及忽略的对比度阈值。 此效果使用与Adobe Photoshop相同的选项 *钝化蒙版* 筛选条件。

>[!NOTE]
USM锐化只应用于PTIFF（金字塔tiff）内缩减像素采样率超过50%的缩减格式副本。 这意味着ptiff中最大大小的演绎版不受钝化蒙版的影响，而较小大小的演绎版（例如缩略图）则被更改（并显示钝化蒙版）。

In **[!UICONTROL 钝化蒙版]**，则可以使用以下筛选选项：

| 选项 | 描述 |
| --- | --- |
| 数量 | 控制应用于边缘像素的对比度数量。 默认值为1.75。对于高分辨率图像，最多可将其增加到5。 将“数量”视为滤镜强度的量度。 范围是0-5。 |
| 半径 | 确定边缘像素周围影响锐化的像素数量。对于高分辨率图像，输入 1 到 2。低值仅锐化边缘像素；高值锐化较宽范围的像素。正确的值取决于图像大小。默认值为0.2。范围是0-250。 |
| 阈值 | 确定在应用钝化蒙版滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入噪声，请尝试使用0-255之间的值。 |

中介绍了锐化 [锐化图像](/help/assets/assets/sharpening_images.pdf).

## 创建Dynamic Media图像配置文件 {#creating-image-profiles}

要为其它资产类型定义高级处理参数，请参阅 [配置资源处理](config-dms7.md#configuring-asset-processing).

参见 [用于处理元数据、图像和视频的配置文件](processing-profiles.md).

另请参阅 [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).

**要创建Dynamic Media图像配置文件，请执行以下操作：**

1. 选择Adobe Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择 **[!UICONTROL 创建]** 以便添加图像配置文件。
1. 输入配置文件名称，以及钝化蒙版、裁切或色板（或两者）的值。

   使用专用于其预期用途的配置文件名称。 例如，如果要创建仅生成样本的配置文件 — 即禁用（关闭）智能裁切，启用（打开）颜色和图像样本 — 则使用配置文件名称“智能样本”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![裁切](assets/crop.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。新创建的配置文件会显示在可用配置文件的列表中。

## 编辑或删除Dynamic Media图像配置文件 {#editing-or-deleting-image-profiles}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要编辑或删除的图像配置文件。 要编辑它，请选择 **[!UICONTROL 编辑图像配置文件]**. 要删除它，请选择 **[!UICONTROL 删除图像配置文件]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果编辑，请保存更改。 如果删除，请确认您要删除配置文件。

## 将Dynamic Media图像配置文件应用到文件夹 {#applying-an-image-profile-to-folders}

将图像配置文件分配给文件夹时，任何子文件夹都会自动从其父文件夹继承配置文件。 此工作流意味着您只能将一个图像配置文件分配给文件夹。 因此，请仔细考虑上传、存储、使用和存档资产的位置的文件夹结构。

如果为文件夹分配了不同的图像配置文件，则新配置文件将覆盖以前的配置文件。 以前现有的文件夹资产保持不变。 新配置文件将应用于稍后添加到此文件夹的资产。

在用户界面中，会使用卡片中显示的配置文件名称指示已为其分配配置文件的文件夹。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像配置文件应用到特定文件夹，也可以全局应用到所有资产。

如果文件夹中已有您后来更改的现有图像配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](processing-profiles.md#reprocessing-assets).

### 将Dynamic Media图像配置文件应用到特定文件夹 {#applying-image-profiles-to-specific-folders}

您可以将图像配置文件应用到中的文件夹 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 属性]**. 本节将介绍这两种将图像配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

如果文件夹中已有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹的处理配置文件后，重新处理文件夹中的资产](processing-profiles.md#reprocessing-assets).

#### 从“配置文件”用户界面将Dynamic Media图像配置文件应用到文件夹 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要应用于一个或多个文件夹的图像配置文件。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择 **[!UICONTROL 将处理配置文件应用到文件夹]** 并选择一个或多个用于接收新上传资源的文件夹，然后选择 **[!UICONTROL 应用]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 将Dynamic Media图像配置文件从“属性”应用到文件夹 {#applying-image-profiles-to-folders-from-properties}

1. 选择Experience League徽标并导航到 **[!UICONTROL 资产]**. 然后导航到要应用图像配置文件的文件夹的父文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。 从 **[!UICONTROL 配置文件名称]** 下拉列表，选择配置文件，然后选择 **[!UICONTROL 保存并关闭]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像配置文件 {#applying-an-image-profile-globally}

除了将配置文件应用到文件夹外，您还可以全局应用配置文件，以便上传到任何文件夹中Experience Manager资源中的任何内容均已应用选定的配置文件。

如果文件夹中已有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 参见 [编辑文件夹中资产的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets).

**要全局应用Dynamic Media图像配置文件，请执行以下操作：**

1. 执行下列操作之一：

   * 导航到 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 并应用相应的配置文件，然后选择 **[!UICONTROL 保存]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite以下节点： `/content/dam/jcr:content`.

      添加属性 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 并选择 **[!UICONTROL 全部保存]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 编辑单个图像的智能裁切或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
·智能裁剪仅在Dynamic Media - Scene7模式下可用。

您可以手动重新对齐图像的智能裁切窗口或调整其大小，以进一步细化其焦点。

编辑智能裁切并保存后，所做的更改会传播到您对特定图像使用该裁切的任何位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

另请参阅 [编辑多个图像的智能裁剪或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**要编辑单个图像的智能裁切或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁切或智能色板图像配置文件的文件夹。

1. 选择文件夹以打开其内容。
1. 选择要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，选择 **[!UICONTROL 智能裁剪]**.

1. 执行以下任一操作：

   * 在页面的右上角附近，向左或向右拖动滑块可分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁切或色板的可查看区域的大小。
   * 在图像上，将框/样本拖动到新位置。 只能编辑图像样本；颜色样本是静态的。
   * 在图像上方，选择  **[!UICONTROL 还原]** 撤消所有编辑并恢复原始裁切或色板。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** 以返回到资产的文件夹。

## 编辑多个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
·智能裁剪仅在Dynamic Media - Scene7模式下可用。

将包含智能裁切的图像配置文件应用到文件夹后，该文件夹中的所有图像都会应用裁切。 如果需要，您可以 *手动* 在多个图像中重新对齐智能裁剪窗口或调整其大小，以进一步细化其焦点。

编辑智能裁切并保存后，所做的更改会传播到您对特定图像使用该裁切的任何位置。

如有必要，您可以重新运行智能裁剪以再次生成其他裁剪。

**要编辑多个图像的智能裁剪或智能色板，请执行以下操作：**

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 资产]**，然后转到应用了智能裁切或智能色板图像配置文件的文件夹。
1. 在文件夹中，选择 **[!UICONTROL 更多操作]** (...)图标，然后选择 **[!UICONTROL 智能裁剪]**.

1. 在 **[!UICONTROL 编辑智能裁剪]** 页面，执行以下任一操作：

   * 调整页面上图像的查看大小。

      在断点名称下拉列表的右侧，向左或向右拖动滑块栏以更改可视图像显示的大小。

      ![edit_smart_ranks-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称筛选可见图像的列表。 在以下示例中，图像是根据断点名称“Medium”进行筛选的。

      在页面的右上角附近，从下拉列表中选择一个断点名称，以筛选您看到的图像。 （请参阅上图。）

      ![edit_smart_rances-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行以下任一操作：

      * 如果图像仅具有智能裁切或智能色板，请在图像上拖动裁切框的角手柄以调整裁切的可查看区域的大小。
      * 如果图像同时具有智能裁切和智能色板，请在图像上拖动裁切框的角手柄以调整裁切的可查看区域的大小。 或者，选择图像下方的智能色板（颜色色板是静态的），然后拖动裁切框的角手柄以调整色板的可查看区域的大小。

      ![调整图像的智能裁剪大小](assets/edit_smart_crops-resize.png)

   * 移动智能裁剪框。 执行以下任一操作：

      * 如果图像具有智能裁剪或仅具有智能色板，请在图像上将裁剪框拖动到新位置。
      * 如果图像同时具有智能裁切和智能色板，请在图像上将智能裁切框拖动到新位置。 或者，选择图像下方的智能色板（颜色色板是静态的），然后将智能色板裁剪框拖动到新位置。

      ![edit_smart_compets-move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

      选择 **[!UICONTROL 还原]** 在图像上方。

      ![edit_smart_compets-revert](assets/edit_smart_crops-revert.png)



1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 关闭]** 以返回到资产的文件夹。

## 从文件夹中删除Dynamic Media图像配置文件 {#removing-an-image-profile-from-folders}

当您从文件夹中删除图像配置文件时，任何子文件夹都会自动继承从其父文件夹中删除的配置文件的操作。 但是，在文件夹内发生的任何文件处理都保持不变。

您可以从中的文件夹删除图像配置文件 **[!UICONTROL 工具]** 菜单，或者如果您在文件夹中，则从 **[!UICONTROL 属性]**. 本节将介绍这两种将图像配置文件从文件夹删除的方法。

### 通过“配置文件”用户界面从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 选择Experience Manager徽标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像配置文件]**.
1. 选择要从一个或多个文件夹中删除的图像配置文件。
1. 选择 **[!UICONTROL 从文件夹中删除处理配置文件]** 并选择一个或多个要从中删除配置文件的文件夹，然后选择 **[!UICONTROL 移除]**.

   您可以确认图像配置文件不再应用于文件夹，因为该名称不再显示在文件夹名称下方。

### 通过属性从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-properties}

1. 选择Experience Manager徽标并导航 **[!UICONTROL 资产]** 然后转到要删除图像配置文件的文件夹。
1. 在文件夹中，选中复选标记以将其选中，然后选择 **[!UICONTROL 属性]**.
1. 选择 **[!UICONTROL 图像配置文件]** 选项卡。
1. 从 **[!UICONTROL 配置文件名称]** 下拉列表，选择 **[!UICONTROL 无]**，然后选择 **[!UICONTROL 保存并关闭]**.

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
