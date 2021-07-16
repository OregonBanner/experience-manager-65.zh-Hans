---
title: 为仅用于置入的呈现版本生成Adobe InDesign
description: 使用Experience Manager资产工作流和ImageMagick生成新资产和现有资产的FPO演绎版。
contentOwner: Vishabh Gupta
role: Admin
feature: 演绎版
exl-id: null
source-git-commit: 865370e38368072c39ad337eb52259c586403efb
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# 为仅用于置入的呈现版本生成Adobe InDesign {#fpo-renditions}

将大型资产从Experience Manager放入Adobe InDesign文档时，创意专业人士必须在[放置资产](https://helpx.adobe.com/indesign/using/placing-graphics.html)后等待一段长时间。 同时，阻止用户使用InDesign。 这会中断创作流程，并对用户体验造成负面影响。 Adobe允许在InDesign文档中临时放置小型演绎版，以开始。 如果需要最终输出（例如，对于打印和发布工作流），原始的全分辨率资产将替换后台的临时演绎版。 后台的此异步更新可加快设计流程以提高生产效率，同时不会妨碍创作流程。

Adobe Experience Manager(AEM)提供仅用于放置(FPO)的演绎版。 这些FPO呈现文件大小较小，但纵横比相同。 如果FPO演绎版不适用于资产，Adobe InDesign会改用原始资产。 此回退机制可确保创意工作流持续进行，不会出现任何中断。

## 生成FPO呈现的方法 {#approach-to-generate-fpo-renditions}

Experience Manager允许使用多种方法处理可用于生成FPO呈现的图像。 最常用的两种方法是使用内置的Experience Manager工作流和使用ImageMagick。 使用这两种方法，您可以配置生成新上传资产的演绎版以及Experience Manager中存在的资产。

您可以使用ImageMagick处理图像，包括生成FPO呈现版本。 此类演绎版会进行缩减采样，即，如果原始图像的PPI大于72，则演绎版的像素尺寸会按比例减小。 请参阅[安装和配置ImageMagick以使用Experience Manager资产](best-practices-for-imagemagick.md)。

|  |使用Experience Manager的内置工作流 |使用ImageMagick工作流 |备注 |
|— |— |—|— |
|对于新资产 |启用FPO呈现([help](#generate-renditions-of-new-assets-using-aem-workflow)) |在Experience Manager工作流中添加ImageMagick命令行([help](#generate-renditions-of-new-assets-using-imagemagick)) |Experience Manager为每次上传执行DAM更新资产工作流。 |
|对于现有资产 |在新的专用Experience Manager工作流中启用FPO呈现([help](#generate-renditions-of-existing-assets-using-aem-workflow)) |在新的专用Experience Manager工作流([help](#generate-renditions-of-existing-assets-using-imagemagick))中添加ImageMagick命令行 |现有资产的FPO演绎版可以按需或批量创建。 |

>[!CAUTION]
>
>通过修改默认工作流的副本，创建工作流以生成演绎版。 它可防止在更新Experience Manager时覆盖您所做的更改，例如通过安装新的Service Pack来覆盖。

## 使用Experience Manager工作流生成新资产的演绎版 {#generate-renditions-of-new-assets-using-aem-workflow}

以下是配置DAM更新资产工作流模型以启用演绎版生成的步骤：

1. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。 选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;模型，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 选择&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤并单击&#x200B;**[!UICONTROL 配置]**。

1. 单击&#x200B;**[!UICONTROL FPO Rendition]**&#x200B;选项卡。 选择&#x200B;**[!UICONTROL 启用FPO呈现版本创建]**。

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 调整&#x200B;**[!UICONTROL 质量]**，并根据需要添加或修改&#x200B;**[!UICONTROL 格式列表]**&#x200B;值。 默认情况下，用于生成FPO呈现的MIME类型列表为pjpeg、jpeg、jpg、gif、png、x-png和tiff。 单击&#x200B;**[!UICONTROL 完成]**。

   >[!NOTE]
   >
   >文件类型JPEG、GIF、PNG、TIFF、PSD和BMP支持生成呈现版本。

1. 要激活更改，请单击&#x200B;**[!UICONTROL 同步]**。

>[!NOTE]
>
>一侧大于1280像素的图像不会保留FPO呈现中的像素大小。

## 使用ImageMagick生成新资产的演绎版 {#generate-renditions-of-new-assets-using-imagemagick}

在Experience Manager中，当上传新资产时，会执行DAM更新资产工作流。 要使用ImageMagick处理新上传资产的演绎版，请向工作流模型中添加新命令。

1. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。 选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;模型，然后单击&#x200B;**[!UICONTROL 编辑]**。

1. 单击左上角的&#x200B;**[!UICONTROL 切换侧面板]**。 搜索命令行步骤。

1. 拖动&#x200B;**[!UICONTROL 命令行]**&#x200B;步骤并将其添加到&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之前。

1. 选择&#x200B;**[!UICONTROL 命令行]**&#x200B;步骤并单击&#x200B;**[!UICONTROL 配置]**。

1. 将所需信息添加为自定义&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 例如，FPO呈现版本（由ImageMagick提供支持）。

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，添加相关的&#x200B;**[!UICONTROL Mime类型]**&#x200B;以提供应用命令的文件格式列表。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡的&#x200B;**[!UICONTROL 命令]**&#x200B;部分中，添加相关的ImageMagick命令以生成FPO呈现版本。

   以下是一个示例命令，用于生成JPEG格式的FPO呈现，将采样缩减为72 PPI，设置为10%质量，并通过拼合输出来处理多层Adobe Photoshop文件：

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 要激活更改，请单击&#x200B;**[!UICONTROL 同步]**。

有关ImageMagick命令行功能的详细信息，请参阅[https://imagemagick.org](https://imagemagick.org)。

## 使用Experience Manager工作流生成现有资产的演绎版 {#generate-renditions-of-existing-assets-using-aem-workflow}

要使用Experience Manager工作流生成现有资产的FPO呈现版本，请创建使用内置FPO呈现版本选项的专用工作流模型。

1. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。 要创建模型，请单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 创建模型]**。 添加有意义的&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 名称]**。

1. 选择模型并单击&#x200B;**[!UICONTROL 编辑]**。 单击&#x200B;**[!UICONTROL 页面信息]** > **[!UICONTROL 打开属性]**。 选择&#x200B;**[!UICONTROL 临时工作流]**。 这提高了可扩展性和性能。 选择&#x200B;******[!UICONTROL 保存并关闭]**。

1. 单击左上角的&#x200B;**[!UICONTROL 切换侧面板]**。 搜索流程缩略图步骤。 拖动&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤。

1. 选择&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;并单击&#x200B;**[!UICONTROL 配置]**。 按照[配置，使用Experience Manager工作流](#generate-renditions-of-new-assets-using-aem-workflow)生成新资产的演绎版。 要激活更改，请单击&#x200B;**[!UICONTROL 同步]**。


## 使用ImageMagick生成现有资产的演绎版 {#generate-renditions-of-existing-assets-using-imagemagick}

要使用ImageMagick处理功能生成现有资产的FPO呈现版本，请创建一个专用的工作流模型，该模型使用ImageMagick命令行执行此操作。

1. 按照[配置中的步骤1到步骤3，使用Experience Manager工作流](#generate-renditions-of-existing-assets-using-aem-workflow)部分生成现有资产的演绎版。

1. 按照[配置中的步骤4到步骤8，使用ImageMagick](#generate-renditions-of-new-assets-using-imagemagick)部分生成新资产的演绎版。


## 查看FPO呈现 {#view-fpo-renditions}

您可以在工作流完成后检查生成的FPO演绎版。 在Experience Manager资产用户界面中，单击资产以打开大型预览。 打开左边栏，然后选择演绎版。 或者，在打开预览时使用键盘快捷键`Alt + 3` 。

单击&#x200B;**[!UICONTROL FPO呈现版本]**&#x200B;以加载其预览。 或者，您也可以右键单击演绎版并将其保存到文件系统。

![rendition_list](assets/rendition_list.png)


## 提示和限制 {#tips-limitations}

* 要使用基于ImageMagick的配置，请将ImageMagick与Experience Manager安装在同一台计算机上。
* 要生成许多资产或整个存储库的FPO演绎版，请在低流量持续期间规划和执行工作流。 为大量资产生成FPO呈现是一项资源密集型活动，Experience Manager服务器必须具有足够的处理能力和可用内存。
* 有关性能和可扩展性，请参阅[微调ImageMagick](performance-tuning-guidelines.md)。
* 有关资产的通用命令行处理，请参阅[命令行处理程序以处理资产](media-handlers.md)。