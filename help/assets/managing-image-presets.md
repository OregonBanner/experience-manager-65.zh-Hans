---
title: 管理Dynamic Media图像预设
description: 了解Dynamic Media图像预设，并了解如何创建、修改和管理图像预设。
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Image Presets
role: User, Admin
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3839'
ht-degree: 23%

---

# 管理Dynamic Media图像预设{#managing-image-presets}

图像预设使Adobe Experience Manager资产能够动态投放不同大小、不同格式或具有动态生成的其他图像属性的图像。 每个图像预设都代表一组预定义的大小调整和格式设置命令，以用于显示图像。在创建图像预设时，您需要选择图像传送的大小。此外，还需要选择格式设置命令，以确保传送供查看的图像时，显示优化的图像外观。

管理员可以创建用于导出资产的预设。用户可以在导出图像时选择预设，这样还可以按照管理员指定的规范重新格式化图像。

您还可以创建响应式图像预设。如果您将响应式图像预设应用于资源，则这些资源会根据查看它们的设备或屏幕大小而发生更改。 您可以将图像预设配置为除了RGB或灰度之外，还在色彩空间中使用CMYK。

本节介绍如何创建、修改和一般管理图像预设。 无论您何时预览图像，都可以对图像应用图像预设。参见 [应用图像预设](/help/assets/image-presets.md).

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用，并在交付的最后毫秒内使用智能功能，以根据浏览器或网络连接速度进一步减小图像文件大小。 参见 [智能成像](/help/assets/imaging-faq.md) 了解更多信息。

## 了解Dynamic Media图像预设 {#understanding-image-presets}

与宏一样，图像预设是一组预定义的大小调整和格式设置命令，这些命令使用同一个名称进行保存。要了解图像预设的工作方式，请假设您的网站要求每个产品图像以不同的大小、不同的格式和压缩率显示，以实现桌面和移动设备交付。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下，仅图像资产支持图像预设。

您可以创建两种图像预设：一种是适用于桌面版本的 500 x 500 像素；一种是适用于移动版本的 150 x 150 像素。您可以创建两个图像预设，一个称为 `Enlarge` 要以500x500像素显示图像，且一个图像名为 `Thumbnail` 以150 x 150像素显示图像。 要传送图像，请执行以下操作 `Enlarge` 和 `Thumbnail` 尺寸，Experience Manager查找放大图像预设和缩略图图像预设的定义。 然后，Experience Manager根据每个图像预设的大小和格式规范动态生成图像。

如果图像在动态传送时大小大幅缩减，图像可能会丢失锐化和细节。由于这一原因，每个图像预设中都包含格式控制，以在传送图像时将其优化为特定大小。这些控制可确保图像在传送到网站或应用程序时具有锐化、清晰的效果。

管理员可以创建图像预设。要创建图像预设，您可以从头开始创建，也可以通过现有图像预设创建，然后使用新名称对其保存。

## 管理Dynamic Media图像预设 {#managing-image-presets-1}

您可以通过点按或单击Experience Manager徽标来访问全局导航控制台，然后点按或单击Experience Manager图标并导航到 **[!UICONTROL 资产>图像预设]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>在预览或交付资产时，您创建的任何图像预设也可用作动态演绎版。
>
>In *Dynamic Media - Scene7模式*，您需要 *非* 需要发布图像预设，因为图像预设会自动发布。
>
>In *Dynamic Media — 混合模式*&#x200B;中，您必须手动发布图像预设。
>
>参见 [发布图像预设](#publishing-image-presets).

>[!NOTE]
>
>当您选择时，系统会显示各种演绎版 **[!UICONTROL 演绎版]** 在资产的“详细信息”视图中。 您可以增加或减少显示的图像预设数量。 参见 [增加显示的图像预设数量](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### 智能裁切、Adobe Illustrator (AI)、Postscript (EPS)和PDF文件格式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>本主题仅适用于Dynamic Media — 混合模式。

如果您打算支持摄取AI、EPS和PDF文件，以便生成这些文件格式的动态演绎版，请在创建图像预设之前查看以下信息。

Adobe Illustrator的文件格式是PDF的变体。 在Experience Manager Assets的环境中，主要区别如下：

* Adobe Illustrator文档由带多个图层的单个页面组成。 每个图层都提取为Illustrator主资源下的PNG子资源。
* PDF文档由一个或多个页面组成。 每页都提取为多页PDF主文档下的单页PDF子资源。

子资源由创建 `Create Sub Asset process` 整体中的组件 `DAM Update Asset` 工作流。 要在工作流中查看此流程组件，请点按 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新资产]** > **[!UICONTROL 编辑]**.

另请参阅 [查看多页文件的页面](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

在打开资产时，点按“内容”菜单，然后选择 **[!UICONTROL 子资产]** 或 **[!UICONTROL 页面]**. 子资产是真正的资产。 即，PDF页面由提取 `Create Sub Asset` 工作流组件。 然后，它们存储为 `page1.pdf`， `page2.pdf`，以此类推，位于主资产下方。 存储之后， `DAM Update Asset` 工作流会处理它们。

要使用Dynamic Media预览和生成AI、EPS或PDF文件的动态演绎版，需要执行以下处理步骤：

1. 在 `DAM Update Asset` 工作流， `Rasterize PDF/AI Image Preview Rendition` 流程组件使用配置的分辨率将原始资源的第一页栅格化为 `cqdam.preview.png` 演绎版。

1. 此 `cqdam.preview.png` 随后，演绎版将由 `Dynamic Media Process Image Assets` 工作流中的流程组件。

>[!NOTE]
>
>在 [!UICONTROL DAM更新资产] 工作流， **[!UICONTROL EPS缩略图]** 步骤为EPS文件生成缩略图。

#### PDF/AI/EPS资源元数据属性 {#pdf-ai-eps-asset-metadata-properties}

| **元数据属性** | **描述** |
|---|---|
| `dam:Physicalwidthininches` | 文档宽度（以英寸为单位）。 |
| `dam:Physicalheightininches` | 文档高度（以英寸为单位）。 |

您访问 `Rasterize PDF/AI Image Preview Rendition` 流程组件选项 `DAM Update Asset` 工作流。

点按左上角的Adobe Experience Manager，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**. 在“工作流模型”页面上，选择 **[!UICONTROL DAM更新资产]**，然后单击工具栏上的点按 **[!UICONTROL 编辑]**. 在 [!UICONTROL DAM更新资产] 工作流页面，双击 `Rasterize PDF/AI Image Preview Rendition` 流程组件，打开其“步骤属性”对话框。

#### 栅格化PDF/AI图像预览演绎版选项 {#rasterize-pdf-ai-image-preview-rendition-options}

![栅格化PDF或AI工作流的参数](assets/rasterize_pdf_ai_image_preview.png)

栅格化PDF或AI工作流的参数

<table>
 <tbody>
  <tr>
   <td><strong>进程参数</strong></td>
   <td><strong>默认设置</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>Mime 类型</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>视为PDF或Illustrator文档的文档MIME类型列表。<br /> </td>
  </tr>
  <tr>
   <td>最大宽度</td>
   <td>2048</td>
   <td>生成的预览演绎版的最大宽度（以像素为单位）。<br /> </td>
  </tr>
  <tr>
   <td>最大高度</td>
   <td>2048</td>
   <td>生成的预览演绎版的最大高度（以像素为单位）。<br /> </td>
  </tr>
  <tr>
   <td>解决方法</td>
   <td>72</td>
   <td>栅格化第一页的分辨率，以ppi为单位（每英寸像素）。</td>
  </tr>
 </tbody>
</table>

使用默认进程参数，PDF/AI文档的第一页栅格化为72 ppi，生成的预览图像大小为2048 x 2048像素。 对于典型部署，您可能希望将分辨率提高到至少150 ppi或更高。 例如，300 ppi的美国信件大小文档的最大宽度和高度分别需要2550 x 3300像素。

“最大宽度”和“最大高度”可限制栅格化分辨率。 例如，如果最大值保持不变，分辨率设置为300 ppi，则US Letter文档将栅格化为186 ppi。 也就是说，文档是1581 x 2046像素。

此 `Rasterize PDF/AI Image Preview Rendition` 流程组件定义了最大值，以确保它不会在内存中创建过大的图像。 如此大的映像可能会使提供给JVM (Java™虚拟机)的内存溢出。 必须注意为JVM提供足够的内存，以便管理配置的并行工作流数量，每个工作流都有可能以配置的最大大小创建映像。

### InDesign(INDD)文件格式 {#indesign-indd-file-format}

如果要支持INDD文件的摄取，以便生成此文件格式的动态演绎版，则可能需要在创建图像预设之前查看以下信息。

对于InDesign文件，仅当Adobe InDesign Server与Experience Manager集成时，才会提取子资源。 引用的资产会根据其元数据进行链接。 链接不需要InDesign Server。 但是，在处理InDesign文件之前，引用的资源必须存在于Experience Manager中，才能在InDesign文件和引用的资源之间创建链接。

参见 [将Experience Manager Assets与InDesign Server集成](/help/assets/indesign.md).

中的媒体提取流程组件 `DAM Update Asset` 工作流运行多个预配置的扩展脚本以处理InDesign文件。

![媒体提取过程的参数中的ExtendScript路径](assets/6_5_mediaextractionprocess.png)

中的媒体提取流程组件的参数中的ExtendScript路径 [!UICONTROL DAM更新资产] 工作流。

Dynamic Media集成使用以下脚本：

<table>
 <tbody>
  <tr>
   <td><strong>ExtendScript名称</strong></td>
   <td><strong>默认</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>是</td>
   <td>生成300-ppi <code>thumbnail.jpg</code> 通过以下方式优化并转换为PTIFF演绎版的演绎版 <code>Dynamic Media Process Image Assets</code> 流程组件。<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>是</td>
   <td>为每页生成一个300 PPIJPEG子资源。 JPEG子资源是存储在InDesign资源下的实际资源。 它还经过优化，并通过以下代码转换为PTIFF <code>DAM Update Asset</code> 工作流。<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>否</td>
   <td>为每个页面生成一个PDF子资源。 将按前面所述处理PDF子资源。 由于PDF仅包含单个页面，因此不会生成任何子资源。<br /> </td>
  </tr>
 </tbody>
</table>

## 配置图像缩略图大小 {#configuring-image-thumbnail-size}

您可以通过在以下位置配置这些设置来配置缩略图的大小： **[!UICONTROL DAM更新资产]** 工作流。 工作流中有两个步骤，您可以在其中配置图像资源的缩略图大小。 尽管(**[!UICONTROL Dynamic Media流程图像资源]**)用于动态图像资产，以及(**[!UICONTROL 进程缩略图]**)用于生成静态缩略图，或者当所有其他进程无法生成缩略图时， *两者* 必须具有相同的设置。

在 **[!UICONTROL Dynamic Media 流程图像资产]**&#x200B;步骤中，缩略图由图像服务器生成，此配置与应用于&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤的配置无关。通过&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤生成缩略图是创建缩览图最耗时、内存占用最多的方法。

缩略图大小按照以下格式定义： **[!UICONTROL 宽度:height:居中]**&#x200B;例如 `80:80:false`. 宽度和高度决定缩略图的大小（以像素为单位）。 中心值为false或true，如果设置为true，则表示缩略图图像大小与配置中给定的大小完全一样。 如果调整大小的图像较小，则它将在缩略图内居中。

>[!NOTE]
>
>* EPS文件的缩略图大小配置于 **[!UICONTROL EPS缩略图]** 步骤，在 **[!UICONTROL 参数]** 选项卡。
>
>* 视频的缩略图大小可在 **[!UICONTROL FFmpeg缩略图]** 步骤，在 **[!UICONTROL 进程]** 选项卡位于 **[!UICONTROL 参数]**.
>


**要配置图像缩略图大小，请执行以下操作：**

1. 点按 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新资产]** > **[!UICONTROL 编辑]**.
1. 点按 **[!UICONTROL Dynamic Media流程图像资源]** 步骤并点按或单击 **[!UICONTROL 缩略图]** 选项卡。 根据需要更改缩略图大小，然后点按&#x200B;**[!UICONTROL 确定]**。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. 点按&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤，然后点按&#x200B;**[!UICONTROL 缩略图]**&#x200B;选项卡。根据需要更改缩略图大小，然后点按&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >**[!UICONTROL 流程缩略图]**&#x200B;步骤的缩略图参数中的值必须与 **[!UICONTROL Dynamic Media 流程图像资产]**&#x200B;步骤中的缩略图参数相匹配。

1. 点按 **[!UICONTROL 保存]** 以将更改保存到工作流。

### 增加或减少显示的Dynamic Media图像预设数量 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

在预览资源时，您创建的图像预设可用作动态演绎版。 Experience Manager在从查看资源时显示各种动态演绎版 **[!UICONTROL “详细信息视图”>“呈现版本”]**. 您可以增加或减少显示的演绎版限制。

**增加或减少显示的Dynamic Media图像预设数量：**

1. 导航到CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 导航到图像预设列表节点，网址为 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 导航到位于的图像预设数据源 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 在limit属性中，将数字更改为所需的数字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 点按 **[!UICONTROL 全部保存]**.

## 创建Dynamic Media图像预设 {#creating-image-presets}

通过创建Dynamic Media图像预设，您可以在预览或发布时将这些设置应用于任何图像。

>[!NOTE]
>
>如果使用 Internet Explorer 9，创建的预设在保存后不会立即显示在预设列表中。要解决此问题，请禁用 IE9 的缓存。

如果您打算支持摄取AI、PDF和EPS文件，以便生成这些文件格式的动态演绎版，请在创建图像预设之前查看以下信息。
参见 [Adobe Illustrator (AI)、Postscript (EPS)和PDF文件格式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

如果要支持INDD文件的摄取，以便生成此文件格式的动态演绎版，则可能需要在创建图像预设之前查看以下信息。
参见 [InDesign(INDD)文件格式](#indesign-indd-file-format).

>[!NOTE]
>
>要创建Dynamic Media图像预设，您必须具有Experience Manager管理员或Admin Console管理员的管理员权限。

**要创建Dynamic Media图像预设，请执行以下操作：**

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像预设]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。此时将打开&#x200B;**[!UICONTROL 编辑图像预设]**&#x200B;窗口。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >要使此图像预设具有响应性，请擦除&#x200B;**[!UICONTROL 宽度]**&#x200B;和&#x200B;**[!UICONTROL 高度]**&#x200B;字段中的值，并将其留空。

1. 根据需要，在&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡中输入值，包括名称。图像预设选项中概 [述了这些选项](#image-preset-options)。 预设显示在左窗格中，并可以与其他资产一起动态使用。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 单击“**[!UICONTROL 保存]**”。

## 创建响应式图像预设 {#creating-a-responsive-image-preset}

要创建响应式图像预设，请执行[创建图像预设](#creating-image-presets)中的步骤。在&#x200B;**[!UICONTROL 编辑图像预设]**&#x200B;窗口中输入高度和宽度时，请清除这两个字段的值，并将其保留为空。

将其保留为空将告知Experience Manager此图像预设可响应。 您可以视需要调整其他值。



>[!NOTE]
>
>要在将图像预设应用到资产时显示 **[!UICONTROL URL]** 和 **[!UICONTROL RESS]** 按钮，必须先发布资产。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>在Dynamic Media - Scene7模式下，图像预设和图像资源会自动发布。
>
>在Dynamic Media — 混合模式下，您必须手动发布图像预设和图像资源。

### 图像预设选项 {#image-preset-options}

在创建或编辑图像预设时，您可以使用本节介绍的几种选项。此外，Adobe建议从以下“最佳实践”选项开始：

* **[!UICONTROL 格式]** (**[!UICONTROL 基本]** 选项卡) — 选择 **[!UICONTROL JPEG]** 或其他符合您要求的格式。所有Web浏览器都支持JPEG图像格式；它在小文件大小和图像质量之间提供了良好的平衡。但是，JPEG格式图像使用有损压缩方案，如果压缩设置太低，则会引入不需要的图像伪影。 因此，Adobe 建议将压缩质量设置为 75。此设置在图像质量和小文件大小之间提供了良好的平衡。

* **[!UICONTROL 启用简单锐化]** - 请勿选择&#x200B;**[!UICONTROL 启用简单锐化]**（此锐化滤镜提供的控制度低于“钝化蒙版”设置）。

* **[!UICONTROL 锐化：重新取样模式]**  — 选择 **[!UICONTROL 锐化2]**.

#### “基本”选项卡选项 {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>字段</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>名称</strong></td>
   <td>输入一个描述性名称，不加任何空格。在名称中包含图像大小规范，以便帮助用户识别此图像预设。</td>
  </tr>
  <tr>
   <td><strong>宽度和高度</strong></td>
   <td>输入传送图像时所用的像素大小。宽度和高度必须大于 0 像素。如果任一值为 0，则无法创建预设。如果两个值均为空，则表示已经创建了响应式图像预设。</td>
  </tr>
  <tr>
   <td><strong>格式</strong></td>
   <td><p>从菜单中选择一个格式。</p> <p>选择 <strong>JPEG</strong> 可提供以下更多选项。</p>
    <ul>
     <li><strong>质量</strong>  — 控制JPEG压缩级别。此设置会影响文件大小和图像质量。JPEG质量范围为1-100。拖动滑块时，缩放是可见的。</li>
     <li><strong>启用JPG色度缩减像素采样</strong>  — 由于眼睛对高频颜色信息的敏感度低于高频亮度，因此JPEG图像将图像信息划分为亮度和颜色分量。当JPEG图像被压缩时，亮度分量保持全分辨率，而颜色分量通过平均像素组一起被缩减取样。缩减取样会将数据量减少一半或三分之一，几乎不影响感知质量。缩减像素取样不适用于灰度图像。此技术可减少对高对比度的图像（例如，具有叠加文本的图像）有用的压缩量。</li>
    </ul>
    <div>
      选择 <strong>GIF</strong> 或<strong>带有 Alpha 的 GIF</strong> 可提供以下更多 <strong>GIF 颜色量化</strong>选项：
    </div>
    <ul>
     <li><strong>类型 </strong> — 选择 <strong>自适应</strong> （默认）， <strong>Web</strong>，或 <strong>Macintosh</strong>.如果您选择 <strong>带有Alpha的GIF</strong>，则Macintosh选项不可用。</li>
     <li><strong>仿色</strong>  — 选择 <strong>扩散</strong> 或 <strong>关闭</strong>.</li>
     <li><strong>颜色数量 </strong> — 输入从2到256的数字。</li>
     <li><strong>颜色列表</strong> - 输入一个以逗号分隔的列表。例如，对于白色、灰色和黑色，输入 <code>000000,888888,ffffff</code>.</li>
    </ul>
    <div>
      选择 <strong>PDF</strong>、<strong>TIFF</strong> 或<strong>带有 Alpha 的 TIFF</strong> 可提供以下更多选项：
    </div>
    <ul>
     <li><strong>压缩</strong> - 选择一种压缩算法。PDF的算法选项包括 <strong>无</strong>， <strong>Zip</strong>、和 <strong>Jpeg</strong>；对于TIFF，选项为 <strong>无</strong>， <strong>LZW</strong>， <strong>Jpeg</strong>、和 <strong>Zip</strong>；对于带有Alpha的TIFF，为 <strong>无</strong>， <strong>LZW</strong>、和 <strong>Zip</strong>.</li>
    </ul> <p>如果选择 <strong>PNG</strong>、<strong>带有 Alpha 的 PNG</strong>，或者选择 <strong>EPS</strong>，则不提供其他选项。</p> </td>
  </tr>
  <tr>
   <td><strong>锐化</strong></td>
   <td>选择<strong>启用简单锐化</strong>选项可在执行所有缩放操作后对图像应用基本锐化滤镜。锐化有助于弥补在以不同大小显示图像时可能产生的模糊。 </td>
  </tr>
 </tbody>
</table>

#### “高级”选项卡选项 {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>字段</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>色彩空间</strong></td>
   <td>选择 <strong>RGB， CMYK，</strong> 或 <strong>灰度</strong> 颜色空间。</td>
  </tr>
  <tr>
   <td><strong>颜色配置文件</strong></td>
   <td>选择资源与工作配置文件不同时应转换为的输出色彩空间配置文件。</td>
  </tr>
  <tr>
   <td><strong>渲染方法</strong></td>
   <td>可以覆盖默认的渲染方法。 渲染意图确定无法在目标颜色配置文件（超出色域）中重现的颜色发生了什么情况。 如果渲染意图与ICC配置文件不兼容，则会被忽略。
    <ul>
     <li>选择 <strong>可感知</strong> 当原始图像中的一个或多个颜色超出目标颜色空间的色域时，将总色域从一个颜色空间压缩到另一个颜色空间。</li>
     <li>选择 <strong>相对比色</strong> 当前颜色空间中的颜色超出目标颜色空间中的色域时。 并且，您希望将其映射到目标颜色空间色域内尽可能最接近的颜色，而不影响任何其他颜色。 </li>
     <li>选择 <strong>饱和度</strong> 如果要在转换为目标颜色空间时重现原始图像颜色饱和度，请执行以下操作。 </li>
     <li>选择 <strong>绝对比色</strong> 以完全匹配颜色，而不调整会改变图像亮度的白点或黑点。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黑场补偿</strong></td>
   <td>如果输出配置文件支持此功能，请选择此选项。 如果黑场补偿与指定的ICC配置文件不兼容，则忽略黑场补偿。</td>
  </tr>
  <tr>
   <td><strong>仿色</strong></td>
   <td>选择此选项可避免或减少颜色分段伪像。 </td>
  </tr>
  <tr>
   <td><strong>锐化类型</strong></td>
   <td><p>选择<strong>无</strong>、<strong>锐化</strong>或 <strong>USM 锐化</strong>。 </p>
    <ul>
     <li>选择 <strong>无</strong> 如果要禁用锐化，请执行以下操作。</li>
     <li>选择 <strong>锐化</strong> 如果要在执行所有缩放后对图像应用基本锐化滤镜，请执行以下操作。 锐化有助于弥补在以不同大小显示图像时可能产生的模糊。 </li>
     <li>选择<strong> 钝化蒙版</strong> 如果要对最终缩减取样图像微调锐化滤镜效果。 您可以控制效果的强度、效果的半径（以像素为单位）以及忽略的对比度阈值。 此效果使用与Photoshop的“钝化蒙版”滤镜相同的选项。</li>
    </ul> <p>在 <strong>USM 锐化</strong>中，您可以设置以下选项：</p>
    <ul>
     <li><strong>金额</strong>  — 控制应用于边缘像素的对比度数量。 缺省实数值为1.0。对于高分辨率图像，最高可将其增加到5.0。将“数量”视为滤镜强度的量度。</li>
     <li><strong>半径</strong>  — 确定边缘像素周围影响锐化的像素数。 对于高分辨率图像，请输入从1到2的实数。 低值仅锐化边缘像素；高值锐化较宽范围的像素。 正确的值取决于图像大小。</li>
     <li><strong>阈值</strong>  — 确定应用钝化蒙版滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入噪声，请尝试使用2到20的整数值。 </li>
     <li><strong>应用到</strong>  — 确定取消锐化是应用于每种颜色还是亮度。</li>
    </ul>
    <div>
      有关“锐化”的信息，请参阅<a href="https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf">锐化图像</a>。
    </div> </td>
  </tr>
  <tr>
   <td><strong>重新取样模式</strong></td>
   <td>选择一个<strong>重新取样模式</strong>选项。在缩减像素采样时，这些选项会锐化图像：
    <ul>
     <li><strong>双线性</strong>  — 最快速的重新取样方法。会出现一些锯齿伪像。</li>
     <li><strong>双三次</strong>  — 增加CPU使用率，但生成更锐利的图像，出现的锯齿伪像较少。</li>
     <li><strong>锐化2</strong>  — 可以生成比两次立方稍微锐利的结果，但其CPU成本更高。</li>
     <li><strong>两次锐化</strong>  — 选择用于减小图像大小的Photoshop默认重新取样器，称为 <strong>双三次锐化</strong> 在Adobe Photoshop中。</li>
     <li><strong>每种颜色</strong>和<strong>亮度</strong> - 每种方法均可基于颜色或亮度。默认情况下将选择<strong>每种颜色</strong>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>打印分辨率</strong></td>
   <td>选择此图像的打印分辨率；默认值为 72 像素。</td>
  </tr>
  <tr>
   <td><strong>图像修饰符</strong></td>
   <td><p>除了UI中可用的常见图像设置之外，Dynamic Media还支持您可以在 <strong>图像修饰符</strong> 字段。 这些参数在 <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api">图像服务器协议命令参考</a>.</p> <p>重要信息：不支持API中列出的以下功能：</p>
    <ul>
     <li>基本模板和文本渲染命令： <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> 和 <code>textPs=</code></li>
     <li>本地化命令： <code>locale=</code> 和 <code>req=xlate</code></li>
     <li><code>req=set</code> 不可用于一般用途。</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>非核心Dynamic Media服务：SVG、图像渲染和Web打印</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 使用图像修饰符定义图像预设选项 {#defining-image-preset-options-with-image-modifiers}

除了“基本”和“高级”选项卡中提供的选项外，您还可以定义图像修饰符，以便在定义图像预设时有更多选择。图像渲染依赖于中详细定义的图像渲染API [HTTP协议参考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api).

下面的一些基本示例显示了可以使用图像修饰符实现的操作。

>[!NOTE]
>
>一些图像修饰符 [无法在Experience Manager中使用](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api)  — 反转每个颜色分量以获得负图像效果。

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api) - 向图像应用模糊滤镜。

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* 组合命令 - op_blur 和 op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api)  — 降低或增加亮度。

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api) - 调整图像不透明度。可用于降低前景不透明度。

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## 编辑图像预设 {#modifying-image-presets}

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 图像预设]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. 选择一个预设，然后单击 **[!UICONTROL 编辑]**.此 **[!UICONTROL 编辑图像预设]** 窗口打开。
1. 进行更改，然后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改，或单击&#x200B;**[!UICONTROL 取消]**&#x200B;以取消更改。

## 发布Dynamic Media图像预设 {#publishing-image-presets}

如果您正在运行Dynamic Media — 混合模式，则必须手动发布图像预设。

(如果您正在运行Dynamic Media - Scene7模式，则会自动为您发布图像预设；您无需完成这些步骤。)

**要在Dynamic Media — 混合模式下发布图像预设，请执行以下操作：**

1. 在Experience Manager中，点按或单击Experience Manager徽标以访问全局导航控制台，然后点按或单击“工具”图标并导航到 **[!UICONTROL 资产]** > **[!UICONTROL 图像预设]**.
1. 从图像预设列表中选择图像预设或多个图像预设，然后单击或点按 **[!UICONTROL Publish]**.
1. 图像预设发布后，状态将从未发布更改为已发布。

   ![chlimage_1-81](assets/chlimage_1-505.png)

## 删除Dynamic Media图像预设 {#deleting-image-presets}

1. 在Experience Manager中，点按或单击Experience Manager徽标以访问全局导航控制台。
1. 点按 **[!UICONTROL 工具]** 图标，然后导航到 **[!UICONTROL 资产]** > **[!UICONTROL 图像预设]**.
1. 选择一个预设，然后单击 **[!UICONTROL 删除]**. Dynamic Media会确认您要删除它。 点按 **[!UICONTROL 删除]** 删除或点按 **[!UICONTROL 取消]** 以中止。
