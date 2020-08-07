---
title: 在中管理您的数字资产 [!DNL Adobe Experience Manager Assets]。
description: 了解资产管理任务，如上传、下载、编辑、搜索、删除、批注以及对数字资产进行版本管理。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d6f48896a56950d44dfe0d1f9b712157951af83c
workflow-type: tm+mt
source-wordcount: '9240'
ht-degree: 8%

---


# 管理您的数字资产 {#manage-digital-assets}

在此 [!DNL Adobe Experience Manager Assets] 中，您可以执行的不仅仅是存储和管理资产。 [!DNL Experience Manager] 优惠企业级资产管理功能。 您可以编辑和共享资产、运行高级搜索、创建数十种受支持文件格式的多个再现、管理版本和数字权限、自动处理资产、管理和管理元数据、使用批注进行协作等。

本文描述基本的资产管理任务，如创建或上传；元数据更新；复制、移动和删除；发布、取消发布和搜索资产。 要了解用户界面，请参 [阅资产用户界面快速入门](/help/sites-authoring/basic-handling.md)。 要管理内容片段，请参 [阅管理内容片段](/help/assets/content-fragments/content-fragments-managing.md) 资产。

## 创建文件夹 {#creating-folders}

在组织资产集合（例如，所有图像）时，您 `Nature` 可以创建文件夹来将它们放在一起。 您可以使用文件夹对资产进行分类和组织。 [!DNL Experience Manager Assets] 不要求您组织文件夹中的资产以更好地工作。

>[!NOTE]
>
>* 共享 [!DNL Assets] 到Marketing Cloud时， `sling:OrderedFolder` 不支持共享类型的文件夹。 如果要共享文件夹，请不要在创建文 [!UICONTROL 件夹时] 选择“已排序”。
>* [!DNL Experience Manager] 不允许将 `subassets` word用作文件夹的名称。 它是为包含复合资产子资产的节点保留的关键字。


1. 导航到数字资产文件夹中要创建新文件夹的位置。 在菜单中，单击“ **[!UICONTROL 创建]**”。 选择 **[!UICONTROL 新建文件夹]**。
1. 在“标 **[!UICONTROL 题]** ”字段中，提供文件夹名称。 默认情况下，DAM使用您提供的标题作为文件夹名称。 创建文件夹后，您可以覆盖默认文件夹并指定其他文件夹名称。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的文件夹会显示在数字资产文件夹中。

不支持以下(以空格分隔的列表)字符：

* 资产文件名不能包含以下任意字符： `* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称不能包含以下任意字符： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

不要在资源文件名的扩展名中包含特殊字符。

## Upload assets {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

您可以将各种类型的资源（包括图像、PDF文件、RAW文件等）从本地文件夹或网络驱动器上传到 [!DNL Experience Manager Assets]。

>[!NOTE]
>
>在Dynamic Media -Scene7模式下，您只能上传文件大小为2 GB或更小的资产。

您可以选择将资产上传到文件夹，无论是否分配了处理用户档案。

对于分配了处理用户档案的文件夹，用户档案名显示在卡视图的缩略图上。 在列表视图中，用户档案名称显示在处理 **用户档案列** 。 请参阅[处理配置文件](/help/assets/processing-profiles.md)。

上传资产之前，请确保其格 [式支](/help/assets/assets-formats.md)[!DNL Experience Manager Assets] 持。

1. In the [!DNL Assets] user interface, navigate to the location where you want to add digital assets.
1. 要上传资产，请执行以下操作之一：

   * 在工具栏中，单击“ **[!UICONTROL 创建]**”。 然后，在菜单中，单击“ **[!UICONTROL 文件]**”。 如果需要，可以重命名显示的对话框中的文件。
   * 在支持HTML5的浏览器中，直接将资源拖动到用户 [!DNL Assets] 界面上。 不显示要重命名文件的对话框。

   ![创建选项以上传资产](assets/create-options.png)

   要选择多个文件，请按Ctrl或Command键，然后在文件选取器对话框中选择资产。 使用iPad时，一次只能选择一个文件。

   您可以暂停上传大型资产（大于500 MB），稍后从同一页面继续上传。 单击 **[!UICONTROL 上传开始]** 时显示的进度栏旁边的“暂停”。

   ![上传资产进度栏](assets/upload-progress-bar.png)

   资产被视为大资产的大小可以配置。 例如，您可以配置系统，将1000 MB以上（而不是500 MB）的资产视为大资产。 在这种情况下，当 **[!UICONTROL 上传大]** 于1000 MB的资产时，进度栏上会显示“暂停”。

   如果上载的文件大于1000 MB且文件小于1000 MB，则“暂停”按钮不显示。 但是，如果取消少于1000 MB的文件上传，将显示“ **[!UICONTROL 暂停]** ”按钮。

   要修改大小限制，请在CRX `chunkUploadMinFileSize` 存储库中 `fileupload`配置节点的属性。

   单击“暂 **[!UICONTROL 停]**”时，它切换到“播 **[!UICONTROL 放]** ”选项。 要继续上传，请单击“ **[!UICONTROL 播放]**”。

   ![恢复暂停的资产上传](assets/resume-paused-upload.png)

   To cancel an ongoing upload, click close (`X`) next to the progress bar. 取消上传操作时，将删 [!DNL Assets] 除资产部分上传的部分。

   在低带宽情况和网络故障中，恢复上传的功能尤为有用，因为上传大型资产需要很长时间。 您可以暂停上传操作，稍后在情况好转时继续。 在继续时，从暂停的位置上传开始。

   在上传操作过程中， [!DNL Experience Manager] 将要上传的资产部分作为数据块保存在CRX存储库中。 上载完成后， [!DNL Experience Manager] 将这些区块合并到存储库中的单个数据块中。

   要为未完成的区块上传作业配置清除任务，请转至 `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`。

   如果您上传的资产名称与您上传资产的位置中已有资产的名称相同，则会显示一个警告对话框。

   您可以选择替换现有资产，创建另一个版本，或者重命名上传的新资产以同时保留两个资产。如果您替换现有资产，则资产的元数据以及您对现有资产所做的任何先前修改（例如注释或裁剪）都将被删除。 如果您选择保留这两个资产，则会重命名新资产，并在其名称 `1` 中附加数字。

   ![用于解决资产名称冲突的名称冲突对话框](assets/resolve-naming-conflict.png)

   >[!NOTE]
   >
   >在名称冲 **[!UICONTROL 突]** 对话框 [!UICONTROL 中选择替] 换时，将为新资产重新生成资产ID。 此ID与上一个资产的ID不同。
   >
   >如果启用“资产分析”以通过Adobe Analytics跟踪展示次数／点击次数，则重新生成的资产ID将使在Analytics上为资产捕获的数据失效。

   If the asset you upload exists in [!DNL Assets], the **[!UICONTROL Duplicates Detected]** dialog warns that you are attempting to upload a duplicate asset. 仅当现有资产的二进制文 `SHA 1` 件的校验和值与您上传的资产的校验和值匹配时，才会显示该对话框。 在这种情况下，资产名称无关紧要。

   >[!NOTE]
   >
   >The [!UICONTROL Duplicates Detected] dialog appears only when the duplicate detection feature is enabled. To enable the duplicate detection feature, see [Enable Duplicate Detection](/help/assets/duplicate-detection.md).

   ![重复资产检测到对话框](assets/duplicate-asset-detected.png)

   要在中保留重复资 [!DNL Assets]产，请单 **[!UICONTROL 击保留]**。 要删除您上传的重复资产，请单击 **[!UICONTROL 删除]**。

   [!DNL Experience Manager Assets] 阻止您上传文件名中带有禁止字符的资产。 如果您尝试上传包含不允许的字符或更多字符的资产，则会显 [!DNL Assets] 示一条警告消息，并停止上传，直到您删除这些字符或使用允许的名称进行上传。

   为了符合组织的特定文件命名约定，您 [!UICONTROL 可以在“上传资产] ”对话框中为上传的文件指定长名。

   但是，不支持以下(以空格分隔的列表)字符：

   * 资产文件名不能包含 `* / : [ \\ ] | # % { } ? &`
   * 资产文件夹名称不能包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

   不要在资源文件名的扩展名中包含特殊字符。

   ![上传进度对话框显示成功上传的文件和无法上传的文件的状态](assets/bulk-upload-progress.png)

   此外，用户 [!DNL Assets] 界面还显示您上传的最新资产或您首先创建的文件夹。

   如果在上传文件之前取消上传操作，则停 [!DNL Assets] 止上传当前文件并刷新内容。 但是，不会删除已上传的文件。

   中的上传进度 [!DNL Assets] 对话框显示成功上传的文件和无法上传的文件计数。

### 串行上传 {#serialuploads}

批量上传大量资产会消耗大量I/O资源，这可能会对部署性能产生不利影响。 [!DNL Assets] 尤其是，如果Internet连接速度较慢，则由于磁盘I/O激增，上传的时间会显着增加。此外，您的Web浏览器可能会对并发资产上传可处理的POST请 [!DNL Assets] 求数量引入额外限制。 因此，上传操作将失败或提前终止。 换句话说，在 [!DNL Experience Manager Assets] 摄取大量文件时可能会丢失某些文件，或者完全无法摄取任何文件。

要克服这种情况， [!DNL Assets] 请在批量上传操作期间一次摄取一个资产（串行上传），而不是同时摄取所有资产。

资产的串行上传默认处于启用状态。 要禁用该功能并允许并发上传，请 `fileupload` 在Crx-de中叠加节点，并将属性的值 `parallelUploads` 设置为 `true`。

### 使用FTP上传资产 {#uploading-assets-using-ftp}

Dynamic Media支持通过FTP服务器批量上传资产。 如果您要上传大型资产(>1 GB)或上传整个文件夹和子文件夹，您应使用FTP。 您甚至可以设置FTP上传，以定期进行。

>[!NOTE]
>
>在Dynamic Media -Scene7模式下，您只能上传文件大小为2 GB或更小的资产。

>[!NOTE]
>
>要在Dynamic Media -Scene7模式下通过FTP上传资产，请在创作实例上安装功 [!DNL Experience Manager] 能包18912。 联 [系Adobe客](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) 户关怀部门以访问FP-18912并完成FTP帐户的设置。 有关详细信息，请参 [阅安装功能包18912以实现批量资源迁移](/help/assets/bulk-ingest-migrate.md)。
>
>如果您使用FTP上传资产，则中指定的上传设 [!DNL Experience Manager] 置将被忽略。 而是使用在Dynamic Media Classic中定义的文件处理规则。

**使用FTP上传资产**

1. 使用您选择的FTP客户端，使用您从供应电子邮件收到的FTP用户名和密码登录到FTP服务器。 在FTP客户端中，将文件或文件夹上传到FTP服务器。
1. [使用从供应电子邮件收到的凭据](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) ，登录到Dynamic Media Classic。 在全局导航栏上，单击“ **[!UICONTROL 上传]**”。

1. 在上传页面左上角附近，单击通过FTP **[!UICONTROL 选项卡]** 。
1. 在页面左侧，选择要从中上传文件的FTP文件夹；在页面的右侧，选择目标文件夹。
1. 在页面右下角附近，单击作 **[!UICONTROL 业选项]** ，然后根据您选择的文件夹中的资产设置所需的选项。

   请参 [阅上传作业选项](#upload-job-options)。

   >[!NOTE]
   >
   >当您通过FTP上传资产时，您在Dynamic Media Classic(S7)中设置的上传作业选项优先于在中设置的资产处理参数 [!DNL Experience Manager]。

1. 在“上传作业选项”对话框的右下角，单击“保 **[!UICONTROL 存”]**。
1. 在上传页面的右下角，单击“提交 **[!UICONTROL 上传”]**。

   要视图上传进度，请在全局导航栏上单击“作 **[!UICONTROL 业”]**。 “作业”页面显示上传的进度。 您可以随时继 [!DNL Experience Manager] 续在Dynamic Media Classic中工作并返回“作业”页面，以查看进行中的作业。
要取消正在进行的上载作业，请单击“持 **[!UICONTROL 续时间]** ”旁边的“取消”。

#### 上传作业选项 {#upload-job-options}

| 上传选项 | 子选项 | 描述 |
|---|---|---|
| 作业名称 |  | 文本字段中预填充的默认名称包括用户输入的名称部分以及日期和时间戳。 您可以使用默认名称，或为此上传作业输入您自己创建的名称。 <br>作业以及其他上传和发布作业将记录在“作业”页面上，您可以在该页面检查作业的状态。 |
| 上传后发布 |  | 自动发布您上传的资产。 |
| 在任意文件夹中覆盖相同的基本资产名称，而不考虑扩展名 |  | 如果希望上传的文件用相同的名称替换现有文件，请选择此选项。 此选项的名称可能不同，具体取决于“应用程序设置”>“常规 **[!UICONTROL 设置]** ”>“上 **[!UICONTROL 传到应用程]** 序”>“覆 **[!UICONTROL 盖图像”中]******&#x200B;的设置。 |
| 上传时解压缩Zip或Tar文件 |  |  |
| 作业选项 |  | 单击 **[!UICONTROL 作业选项]** ，打开“上 [!UICONTROL 传作业选项] ”对话框，然后选择影响整个上传作业的选项。 这些选项对于所有文件类型都是相同的。<br>您可以从“应用程序常规设置”页面开始选择上传文件的默认选项。 要打开此页，请选择“设 **[!UICONTROL 置”]** >“应 **[!UICONTROL 用程序设置]**”。 单击“默 **[!UICONTROL 认上传选项]** ”按钮以打开“ [!UICONTROL 上传作业选项] ”对话框。 |
|  | 当 | 选择一次或重复。 要设置重复作业，请选择“重复”选项（每日、每周、每月或自定义），以指定要重复FTP上传作业的时间。 然后根据需要指定计划选项。 |
|  | 包含子文件夹 | 上传您要上传的文件夹中的所有子文件夹。 您上传的文件夹及其子文件夹的名称会自动输入 [!DNL Experience Manager Assets]。 |
|  | 裁剪选项 | 要从图像两侧手动裁剪，请选择“裁剪”菜单，然后选择“手动”。 然后输入要从图像的任何一侧或每一侧裁剪的像素数。 裁剪的图像多少取决于图像文件中的 ppi（每英寸像素数）设置。例如，如果图像显示 150 ppi，您在“顶部”、“右”、“底部”和“左”文本框中分别输入 75，则会从每个侧边裁剪半英寸。<br> 要自动裁切图像中的空白像素，请打开“裁剪”菜单，选择“手动”，然后在“顶部”、“右”、“底部”和“左”字段中输入像素度量值以从两侧进行裁剪。 您还可以在“裁剪”菜单上选择“修剪”并选择以下选项：<br> **根据裁切** <ul><li>**颜色** -选择颜色选项。 然后，选择“角”菜单，选择图像的角，其颜色最能代表您要裁剪的空白颜色。</li><li>**透明度** -选择“透明度”选项。<br> **容差** -拖动滑块以指定从0到1的容差。对于基于颜色的修剪，指定0仅在像素与您在图像角中选择的颜色完全匹配时裁剪像素。 接近1的数字允许更多的颜色差异。<br>对于基于透明度的修剪，指定0可仅裁剪透明像素。 接近1的数字意味着更加透明。</li></ul><br>请注意，这些裁剪选项是无损的。 |
|  | 颜色用户档案选项 | 在创建用于投放的优化文件时选择颜色转换：<ul><li>默认颜色保留：当图像包含色彩空间信息时，保留源图像颜色；没有颜色转换。 现在几乎所有图像都已嵌入相应的颜色用户档案。 但是，如果CMYK源图像不包含嵌入的颜色用户档案，则这些颜色将转换为sRGB（标准红绿蓝）色彩空间。 sRGB是用于在网页上显示图像的推荐色彩空间。</li><li>保留原始色彩空间：保留原始颜色，点上不进行任何颜色转换。 对于没有嵌入颜色用户档案的图像，任何颜色转换均使用在“发布”设置中配置的默认颜色用户档案进行。 颜色用户档案可能与使用此选项创建的文件中的颜色不对齐。 因此，建议您使用默认颜色保留选项。</li><li>“自定义自”>“至<br> ”打开菜单，因此您可以选择“转换自”和“转换至色彩空间”。 此高级选项将覆盖嵌入在源文件中的任何颜色信息。 当您提交的所有图像都包含不正确或缺少颜色用户档案数据时，请选择此选项。</li></ul> |
|  | 图像编辑选项 | 您可以在图像中保留剪切蒙版，并选择颜色用户档案。<br> 请参 [阅在上传时设置图像编辑选项](#setting-image-editing-options-at-upload)。 |
|  | Postscript选项 | 您可以栅格化PostScript®文件、裁剪文件、维护透明背景、选择分辨率和选择色彩空间。<br> 请参 [阅设置PostScript和Illustrator上传选项](#setting-postscript-and-illustrator-upload-options)。 |
|  | Photoshop选项 | 您可以从Adobe®Photoshop®文件创建模板、维护图层、指定如何命名图层、提取文本以及指定如何将图像定位到模板中。<br> 请注意，中不支持模板 [!DNL Experience Manager]。<br> 请参阅 [设置Photoshop上传选项](#setting-photoshop-upload-options)。 |
|  | PDF选项 | 您可以栅格化文件、提取搜索词和链接、自动生成电子目录、设置分辨率和选择色彩空间。<br> 请注意，中不支持eCatalog [!DNL Experience Manager]。 <br> 请参 [阅设置PDF上传选项](#setting-pdf-upload-options)。 |
|  | Illustrator选项 | 您可以栅格化Adobe Illustrator®文件、保持透明背景、选择分辨率和选择色彩空间。<br> 请参 [阅设置PostScript和Illustrator上传选项](#setting-postscript-and-illustrator-upload-options)。 |
|  | EVideo选项 | 您可以通过选择视频预设对视频文件进行转码。<br> 请参 [阅设置eVideo上传选项](#setting-evideo-upload-options)。 |
|  | 批集预设 | 要从上传的文件创建图像集或旋转集，请单击要使用的预设的活动列。 您可以选择多个预设。 您可以在Dynamic Media Classic的“应用程序设置／批集预设”页面中创建预设。<br> 请参 [阅将批集预设配置为自动生成图像集和旋转集](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) ，以了解有关创建批集预设的更多信息。<br> 请参 [阅在上传时设置批集预设](#setting-batch-set-presets-at-upload)。 |

#### 在上传时设置图像编辑选项 {#setting-image-editing-options-at-upload}

上传图像文件（包括AI、EPS和PSD文件）时，可以在“上传作业选项”对话框中执 [!UICONTROL 行以下编辑] 操作：

* 从图像边缘裁切空格（请参阅上表中的说明）。
* 从图像两侧手动裁切（请参阅上表中的说明）。
* 选择颜色用户档案（请参阅上表中的选项说明）。
* 从剪切路径创建蒙版。
* 使用USM锐化选项锐化图像
* 挖空背景

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop’s Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone’s face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or “turn on” the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### 设置PostScript和Illustrator上传选项 {#setting-postscript-and-illustrator-upload-options}

上传PostScript(EPS)或Illustrator(AI)图像文件时，可以采用各种格式设置它们。 您可以栅格化文件、保持透明背景、选择分辨率和选择色彩空间。 “PostScript选项”和“Illustrator选项”下的“上 [!UICONTROL 传作业选项] ”对话框中提 [!UICONTROL 供格式化PostScript] 和 [!UICONTROL “Illustrator]选项”选项。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 正在处理 |  | 选 **[!UICONTROL 择栅格]** ，将文件中的矢量图形转换为位图格式。 |
| 在渲染后的图像中保持透明背景 |  | 保持文件的背景透明度。 |
| 分辨率 |  | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| 色彩空间 |  | 选择“色彩空间”菜单，并从以下色彩空间选项中进行选择： |
|  | 自动检测 | 保留文件的色彩空间。 |
|  | 强制为RGB | 转换为RGB色彩空间。 |
|  | 强制为CMYK | 转换为CMYK色彩空间。 |
|  | 强制为灰度 | 转换为灰度色彩空间。 |

#### 设置Photoshop上传选项 {#setting-photoshop-upload-options}

Photoshop文档(PSD)文件最常用于创建图像模板。 上传PSD文件时，可以自动从文件创建图像模板(在“上传”屏 [!UICONTROL 幕上选择] “创建模板”选项)。

如果您使用PSD文件创建模板，Dynamic Media会使用图层从PSD文件创建多个图像；它为每个图层创建一个图像。

使用上 [!UICONTROL 述的裁剪][!UICONTROL 选项和颜]色用户档案选项，以及Photoshop上传选项。

>[!NOTE]
>
>中不支持模板 [!DNL Experience Manager]。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 维护图层 |  | 将PSD中的图层（如果有）拆分为单个资源。 资产图层仍与PSD关联。 可以通过在“细节”视图中打开PSD文件并选择图层面板来视图它们。 |
| 创建模板 |  | 从PSD文件中的图层创建模板。 |
| 提取文本 |  | 提取文本，以便用户在查看器中搜索文本。 |
| 将图层扩展到背景大小 |  | 将已撕开的图像图层的大小扩展到背景图层的大小。 |
| 图层命名 |  | PSD文件中的图层作为单独的图像上传。 |
|  | 图层名称 | 在PSD文件中将图像命名为图层名称之后。 例如，原始PSD文件中名为Price Tag的图层将变为名为Price Tag的图像。 但是，如果PSD文件中的图层名称是默认的Photoshop图层名称（背景、图层1、图层2等），则图像将以PSD文件中的图层编号命名，而不是以其默认图层名称命名。 |
|  | Photoshop和层号 | 在PSD文件中将图像命名为图层编号之后的图像，而忽略原始图层名称。 图像以Photoshop文件名和附加的图层编号命名。 例如，名为Spring Ad.psd的文件的第二个层被命名为Spring Ad_2，即使它在Photoshop有非默认名称。 |
|  | Photoshop和图层名称 | 在PSD文件之后命名图像，后跟图层名称或图层编号。 如果PSD文件中的图层名称是默认的Photoshop图层名称，则使用图层编号。 例如，在名为SpringAd的PSD文件中名为Price Tag的图层被命名为Spring Ad_Price Tag。 具有默认名称Layer 2的层称为Spring Ad_2。 |
| 锚点 |  | 指定如何在从PSD文件生成的分层合成生成的模板中定位图像。 默认情况下，锚点为中心。 无论替换图像的长宽比如何，中心锚点都允许替换图像以最佳方式填充相同的空间。 当引用模板并使用参数替换时，具有替换此图像的不同方面的图像会有效地占据相同的空间。 如果应用程序需要替换图像以填充模板中分配的空间，请更改为其他设置。 |

#### 设置PDF上传选项 {#setting-pdf-upload-options}

上传PDF文件时，可以采用各种格式设置它。 您可以裁切其页面、提取搜索词、输入每英寸像素分辨率并选择色彩空间。 PDF文件通常包含裁切边距、裁切标记、套准标记和其他打印机标记。 在上传PDF文件时，可以从页面两侧裁切这些标记。

>[!NOTE]
>
>eCatalogs在中不受支持 [!DNL Experience Manager]。

从以下选项中进行选择：

| 选项 | 子选项 | 描述 |
|---|---|---|
| 正在处理 | 栅格化 | （默认）翻页PDF文件中的页面，并将矢量图形转换为位图图像。 选择此选项可创建电子目录。 |
| 提取 | 搜索词 | 从PDF文件提取单词，以便在eCatalog查看器中按关键字搜索文件。 |
|  | 链接 | 从PDF文件提取链接并将其转换为在电子目录查看器中使用的图像映射。 |
| 从多页PDF自动生成电子目录 |  | 自动从PDF文件创建电子目录。 电子目录以您上传的PDF文件命名。 （只有在上传PDF文件时栅格化该文件时，此选项才可用。） |
| 分辨率 |  | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认为 150。 |
| 色彩空间 |  | 选择“色彩空间”菜单并为PDF文件选择色彩空间。 大多数PDF文件同时具有RGB和CMYK彩色图像。 RGB色彩空间是联机查看的首选。 |
|  | 自动检测 | 保留PDF文件的色彩空间。 |
|  | 强制为RGB | 转换为RGB色彩空间。 |
|  | 强制为CMYK | 转换为CMYK色彩空间。 |
|  | 强制为灰度 | 转换为灰度色彩空间。 |

#### 设置eVideo上传选项 {#setting-evideo-upload-options}

要通过从各种视频预设中进行选择来转码视频文件。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 自适应视频 |  | 可与任何宽高比配合使用的单个编码预设，用于为投放到移动设备、平板电脑和桌面创建视频。 使用此预设编码的已上传源视频的高度设置为固定。 但是，宽度会自动缩放以保留视频的宽高比。 <br>最佳实践是使用自适应视频编码。 |
| 单个编码预设 | 对编码预设进行排序 | 选择“名称”或“大小”，按名称或分辨率大小对在桌面、移动设备和平板电脑下列出的编码预设进行排序。 |
|  | 桌面设备 | 创建MP4文件，为台式计算机提供流式或渐进式视频体验。根据所需的分辨率大小和目标数据速率选择一个或多个长宽比。 |
|  | 移动设备 | 创建MP4文件以在iPhone或Android移动设备上进行投放。选择一个或多个长宽比，其分辨率大小和目标数据速率均符合您的要求。 |
|  | 平板电脑 | 创建MP4文件以在iPad或Android平板电脑设备上投放。根据所需的分辨率大小和目标数据速率选择一个或多个长宽比。 |

#### 在上传时设置批集预设 {#setting-batch-set-presets-at-upload}

如果要从已上传的图像自动创建图像集或旋转集，请单击要使用的预设的活动列。 您可以选择多个预设。

请参 [阅将批集预设配置为自动生成图像集和旋转集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) ，以了解有关创建批集预设的更多信息。

### 流式上传 {#streamed-uploads}

如果将许多资产上传到Adobe Experience Manager，则对服务器的I/O请求会显着增加，这会降低上传效率，甚至会导致一些上传任务超时。 [!DNL Experience Manager Assets] 支持流式上传资产。 流式上传通过在将磁盘复制到存储库之前避免在服务器上的临时文件夹中存储资产，减少了上传操作期间的磁盘I/O。 而是直接将数据传输到存储库。 这样，上传大型资产的时间和超时的可能性就会减少。 默认情况下，在中启用流式上传 [!DNL Assets]。

>[!NOTE]
>
>对于在JEE服务器上运行的版本低于3.1的servlet-api的Adobe Experience Manager，禁用流上传。

### 提取包含资产的ZIP存档 {#extractzip}

您可以像上传任何其他受支持的资产一样上传ZIP存档。 同一文件名规则适用于ZIP文件。 [!DNL Experience Manager] 允许您将ZIP存档解压到DAM位置。 如果存档文件不包含ZIP作为扩展名，请使用内容启用文件类型检测。

一次选择一个ZIP归档，单击“解 **[!UICONTROL 压归档]**”，然后选择目标文件夹。 选择一个选项以处理冲突（如果有）。 如果目标文件夹中已存在ZIP文件中的资产，您可以选择以下选项之一：跳过提取、替换现有文件、重命名以保留两个资产或创建新版本。

提取完成后， [!DNL Experience Manager] 在通知区域通知您。 在 [!DNL Experience Manager] 提取ZIP时，您可以返回工作，而不中断提取。

![ZIP文件提取通知](assets/Zip-extraction-notification.png)

该功能的一些限制是：

* 如果目标位置存在同名的文件夹，则ZIP文件中的资产会解压缩到现有文件夹中。
* 如果取消提取，则不会删除已提取的资产。
* 不能同时选择两个ZIP文件并解压它们。 一次只能解压一个ZIP存档。
* 上传ZIP存档时，如果上传对话框显示500服务器错误，请在安装最新的服务包后重试。

## 预览资产 {#previewing-assets}

要预览资产，请执行以下步骤。

1. 在用 [!DNL Assets] 户界面中，导航到要预览的资产所在的位置。
1. 单击所需的资产以将其打开。

1. 在预览模式下，缩放选项可用于支持的 [图像类型](/help/assets/assets-formats.md#supported-raster-image-formats) （通过交互式编辑）。

   要放大资产，请单 `+` 击（或单击资产上的放大镜）。 要缩小，请单击 `-`。 放大时，可以通过平移来仔细查看图像上的任意区域。重置缩放箭头可让您返回原始视图。 要将视图重置为原始大小，请单击“重 **[!UICONTROL 置]**![重置视图](assets/do-not-localize/revert.png)”。

**预览仅使用键盘键**

要使用键盘预览资产，请执行以下步骤：

1. 在用户 [!DNL Assets] 界面中，使用箭头键和箭头键导航到 `Tab` 所需的资产。

1. 按 `Enter` 所需资产上的键打开它。 您可以在预览模式下缩放资源。

1. 要放大资产，请执行以下操作：
   1. 使 `Tab` 用键移动焦点以放大选项。
   1. 使 `Enter` 用键放大图像。

   要缩小， `Tab` 请使用键将焦点移到缩小选项并按 `Enter`。

1. 使用 `Shift` + `Tab` 键将焦点移回图像上。

1. 使用箭头键在缩放的图像周围移动。

>[!MORELIKETHIS]
>
>* [预览Dynamic Media资产](/help/assets/previewing-assets.md)。
>* [视图子资产](managing-linked-subassets.md#viewing-subassets)。


## 编辑属性和元数据 {#editing-properties}

1. 导航到资产所在的位置以编辑其元数据。

1. 选择资产，然后单击工 **[!UICONTROL 具栏]** 中的属性以视图资产属性。 或者，选择资 **[!UICONTROL 产卡]** 上的属性快速操作。

   ![资产卡视图的属性快速操作](assets/properties_quickaction.png)

1. 在“属 [!UICONTROL 性] ”页面中，编辑各个选项卡下的元数据属性。 例如，在“基 **[!UICONTROL 本]** ”选项卡下，编辑标题、说明等。

   >[!NOTE]
   >
   >“属性”页面 [!UICONTROL 的布局] 和可用的元数据属性取决于基础元数据模式。 要了解如何修改“属性”页面的 [!UICONTROL 布局] ，请参阅元 [数据模式](/help/assets/metadata-schemas.md)。

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![日期时间选取器或使用“开始时间”(On Time)字段中的键盘键添加资产激活的日期和时间](assets/datepicker.png)

   *图：使用日期选取器计划资产激活。*

1. 要在特定持续时间后取消激活资产，请从关闭时间字段旁边的日期选取器中选择取消激 **[!UICONTROL 活日期]** /时间。 取消激活日期应晚于资产的激活日期。 结束 [!UICONTROL 时间后]，资产及其演绎版不能通过Web界面 [!DNL Assets] 或通过HTTP API使用。

1. 在“标 **[!UICONTROL 记]** ”字段中，选择一个或多个标记。 要添加自定义标记，请在框中键入标记名称，然后按Enter。 新标记保存在中 [!DNL Experience Manager]。 [!DNL YouTube] 需要标记才能发布。 See [publish videos to YouTube](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >要创建标记，您需要在CRX存储库 `/content/cq:tags/default` 中的写入权限。

1. To provide a rating to the asset, click the **[!UICONTROL Advanced]** tab and then click the star at the appropriate position to assign the desired rating.

   ![资产属性中用于分配评级的高级选项卡](assets/ratings.png)

   您为资产分配的评级分数将显示在您的 **[!UICONTROL 评级下]**。 对资产进行评级的用户收到的资产的平均评级分数会显示在“评 **[!UICONTROL 级”下]**。 此外，在“评级细分”下显示对平均评级得分有贡献的评级分 **[!UICONTROL 数的分解]**。 您可以根据平均评级分数搜索资产。

1. 要视图资产的使用情况统计信息，请单击“ **[!UICONTROL 分析]** ”选项卡。

   使用情况统计信息包括：

   * 资产的查看或下载次数
   * 渠道/设备，资产通过这些设备
   * 最近使用该资产的创意解决方案

   有关详细信息，请参阅 [资产分析](/help/assets/touch-ui-asset-insights.md)。

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。
1. 导航到用 [!DNL Assets] 户界面。 已编辑的元数据属性（包括标题、描述、评级等）将显示在卡片视图的资产卡上以及列表视图的相关列下。

## 复制资产 {#copying-assets}

在复制资产或文件夹时，会复制整个资产或文件夹及其内容结构。 复制的资产或文件夹会在目标位置重复。 源位置的资产不会更改。

资产特定副本的一些属性不会结转。 例如：

* 资产ID、创建日期和时间、版本和版本历史记录。 其中一些属性由属性 `jcr:uuid`、 `jcr:created`和表示 `cq:name`。

* 每个资产及其每个演绎版的创建时间和引用路径都是唯一的。

其他属性和元数据信息将被保留。 复制资产时不会创建部分副本。

1. 在界 [!DNL Assets] 面中，选择一个或多个资产，然后 **[!UICONTROL 单击工]** 具栏中的复制。 或者，也可以从资 **[!UICONTROL 产卡]**![中选择资产界面工具栏中的](assets/do-not-localize/copy_icon.png) “复制”复制选项。

   >[!NOTE]
   >
   >如果您使用复 [!UICONTROL 制快速] 操作，则一次只能复制一个资产。

1. 导航到要将资产复制到的位置。

   >[!NOTE]
   >
   >If you copy an asset at the same location, [!DNL Experience Manager] automatically generates a variation of the name. For example, if you copy an asset titled `Square`, [!DNL Experience Manager] automatically generates the title for its copy as `Square1`.

1. 单击工 **[!UICONTROL 具栏]**![中资产工具栏中的](assets/do-not-localize/paste.png) “粘贴粘贴”选项。 资产随后会被复制到此位置。

   >[!NOTE]
   >
   >The **[!UICONTROL Paste]** option is available in the toolbar until the paste operation is completed.

### 移动或重命名资产 {#moving-or-renaming-assets}

1. 导航到要移动的资产所在的位置。

1. 选择资产，然后单击工 **[!UICONTROL 具栏]** 中的移动选项。
   ![“资产”工具栏中的“移动”选项](assets/do-not-localize/move.png)

1. In the [!UICONTROL Move Assets] wizard, do one of the following:

   * 指定资产在移动后的名称。 然后，单 **[!UICONTROL 击]** “下一步”继续。

   * Click **[!UICONTROL Cancel]** to stop the process.
   >[!NOTE]
   >
   >* 您可以为资产指定相同的名称，前提是新位置中没有使用该名称的资产。但是，如果您将资产移动到存在同名资产的位置，则应使用其他名称。 如果使用相同的名称，系统将自动生成该名称的变体。 例如，如果您的资产的名称为“Square”，系统会为其副本生成名称“Square1”。
   >* 重命名时，文件名中不允许有空格。


1. On the **[!UICONTROL Select Destination]** dialog, do one of the following:

   * Navigate to the new location for the assets, and then click **[!UICONTROL Next]** to proceed.

   * Click **[!UICONTROL Back]** to return to the **[!UICONTROL Rename]** screen.

1. 如果被移动的资产具有任何引用页面、资产或收藏集，则调整引 **[!UICONTROL 用选项卡会出]** 现在选择目 **[!UICONTROL 标选项卡]** 的旁边。

   在“调整引用”屏幕中执 **[!UICONTROL 行下列操作]** :

   * Specify the references to be adjusted based on the new details, and then click **[!UICONTROL Move]** to proceed.

   * From the **[!UICONTROL Adjust]** column, select/unselect references to the assets.
   * Click **[!UICONTROL Back]** to return to the **[!UICONTROL Select Destination]** screen.

   * 单击 **[!UICONTROL 取消]** ，以停止移动操作。

   如果您不更新引用，则它们会继续指向资产的上一路径。 如果您调整引用，它们将更新为新的资产路径。

## 管理再现 {#managing-renditions}

1. 您可以为资产添加或删除演绎版，但原始形式除外。导航到您要为其添加或删除演绎版的资产所在的位置。

1. 单击资产以打开其页面。
1. 在Experience Manager界面中，从 **[!UICONTROL 列表中]** 选择演绎版。

   ![左边栏以打开菜单并选择演绎版选项](assets/renditions_menu.png)

1. 在&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中，查看为资产生成的演绎版列表。

   ![“资产详细信息”页面上的演绎版面板](assets/renditions_panel.png)

   >[!NOTE]
   >
   >默认情况下， [!DNL Assets] 不会在预览模式下显示资产的原始演绎版。 如果您是管理员，则可以使用叠加配置以 [!DNL Assets] 在预览模式下显示原始演绎版。

1. 选择一个演绎版以进行查看或删除。

   **删除演绎版**

   从演绎版面板 **[!UICONTROL 中选择]** ，然后单击删除演绎版选 **[!UICONTROL 项]** 以从工具栏中删除演绎版 ![](assets/do-not-localize/deleteoutline.png) 选项。 资产处理完成后，无法批量删除演绎版。 对于单个资产，您可以从用户界面手动删除演绎版。 对于多个资产，您可以自定义Experience Manager以删除特定演绎版或删除资产，然后重新上传已删除的资产。

   **上传新再现**

   导航到资产的资产详细信息页面，然后单击 **[!UICONTROL 添加]**![演绎版选项，以上传工具栏中的新演绎版选项](assets/do-not-localize/add.png) ，以上传资产的新演绎版。

   >[!NOTE]
   >
   >如果您从演绎版面板中选 **[!UICONTROL 择了演绎版]** ，工具栏会更改上下文并仅显示与演绎版相关的那些操作。 Options, such as the [!UICONTROL Upload Rendition] option is not displayed. 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以配置要在图像或视频资产的详细信息页面中显示的演绎版的尺寸。 根据您指定的尺寸，显 [!DNL Assets] 示具有精确或最接近尺寸的再现。

   要在资产详细信息级别配置图像的演绎版尺寸，请叠 `renditionpicker` 加节点(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)并配置width属性的值。 配置属性大 **[!UICONTROL 小（长）(以KB]** )代替宽度，以根据图像大小在资产详细信息页面上自定义再现。 对于基于大小的自定义，如果匹 `preferOriginal` 配的再现的大小大于原始再现，则属性会为原始再现分配首选项。

   同样，您也可以通过覆盖来自定义“注释”页面图 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`像。

   ![在CRXDE中叠加重新显示选取器节点以自定义注释页面图像](assets/renditionpicker-node-crxde.png)

   要为视频资产配置演绎版维度，请导航到CRX `videopicker` 存储库中位于该位置的节 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`点，叠加该节点，然后编辑相应的属性。

   >[!NOTE]
   >
   >视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。此外，该功能支持不同的视频格式，具体视浏览器而定。

有关生成和查看子资产的详细信息，请参阅 [管理子资产](managing-linked-subassets.md#generate-subassets)。

## Delete assets {#deleting-assets}

要删除资产，用户需要具有的删除权限 `dam/asset`。 如果您只具有修改权限，则只能编辑资产元数据并向资产添加注释。 但是，您无法删除资产或其元数据。

要解析或删除其他页面中的传入引用，请在删除资产之前更新相关引用。 要禁止用户删除引用的资产和离开断开的链接，请使用叠加禁用强制删除选项。

1. 导航至要删除的资产所在的位置。

1. 选择资产，然后单击工 **[!UICONTROL 具栏]**![中的删](assets/do-not-localize/deleteoutline.png) 除选项。

1. 在确认对话框中，选择以下选项之一：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 删除]**，以确认操作：

      * 如果资产没有引用，则资产会被删除。
      * 如果资产具有引用，则会出现一条错误消息，通知您&#x200B;**一个或多个资产被引用**。您可以选择&#x200B;**[!UICONTROL 强制删除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。

   >[!NOTE]
   >
   >* 要解析或删除其他页面中的传入引用，请在删除资产之前更新相关引用。 此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产和离开断开的链接。
   >* 可以删除包含已签 *出的资* 源文件的文件夹。 删除文件夹之前，请确保用户未签出任何数字资产。


## 下载资产 {#downloading-assets}

请参 [阅从Experience Manager下载资产](/help/assets/download-assets-from-aem.md)。

## Publish assets {#publishing-assets}

>[!NOTE]
>
>有关Dynamic Media的详细信息，请参阅发 [布Dynamic Media资产。](/help/assets/publishing-dynamicmedia-assets.md)

1. 导航到要发布的资产／文件夹所在的位置。

1. Either select the **[!UICONTROL Publish]** quick action from the asset card, or select the asset and click the **[!UICONTROL Quick Publish]** option from the toolbar.
1. 如果资产引用了其他资产，向导中便会列出这些引用。仅显示自上次发布／取消发布后未发布或已修改的引用。 选择要发布的引用。

   >[!NOTE]
   >
   >属于您已发布文件夹的空文件夹不会发布。

1. Click **[!UICONTROL Publish]** to confirm the activation for the assets.

>[!CAUTION]
>
>如果您发布的资产正在处理，则仅会发布原始内容。 缺少再现。 等待处理完成，然后在处理完成后发布或重新发布资产。

## 取消发布资产 {#unpublishing-assets}

1. 导航到要从发布环境（取消发布）中删除的资产／资产文件夹的位置。

1. 选择要取消发布的资产／文件夹，然后单击工 **[!UICONTROL 具栏中]**![的管理发布](assets/do-not-localize/globe-publication.png) 选项。

1. 从列表 **[!UICONTROL 中选择]** “取消发布”操作。

   ![取消发布操作](assets/unpublish_action.png)

1. To unpublish the asset later, select **[!UICONTROL Unpublish Later]**, and then select a date for unpublishing the asset.
1. 计划一个资产在发布环境中不再可用的日期。
1. If the asset references other assets, choose the references you want to unpublish. Click **[!UICONTROL Unpublish]**.
1. 在确认对话框中，单击：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 取消发布]** ，以确认在指定日期已取消发布资产(在发布环境中不再可用)。

   >[!NOTE]
   >
   >取消发布复杂资产时，仅取消发布该资产。请避免取消发布引用，因为可能其他已发布的资产也引用了这些内容。

## 已关闭的用户组 {#closed-user-group}

已关闭的用户组(CUG)用于限制对从发布的特定资产文件夹的访问 [!DNL Experience Manager]。 如果为文件夹创建CUG，则仅对分配的成员或组具有对文件夹（包括文件夹资产和子文件夹）的访问权限。 要访问文件夹，他们必须使用其安全凭据登录。

CUG是限制访问您的资产的额外方式。 您还可以为文件夹配置登录页面。

1. 从界面中选择一 [!DNL Assets] 个文件夹，然后单 [!UICONTROL 击工具] 栏中的属性选项以显示属性页。
1. 在“权 **[!UICONTROL 限]** ”选项卡中，在“已关闭的用户组” **[!UICONTROL 下添加成员或组]**。

   ![在已关闭的用户组中添加用户](assets/add_user.png)

1. 要在用户访问文件夹时显示登录屏幕，请选择“启 **[!UICONTROL 用]** ”选项。 然后，选择登录页面的路径， [!DNL Experience Manager]并保存更改。

   ![启用并选择登录页面，以在用户访问文件夹时显示](assets/login_page.png)

   >[!NOTE]
   >
   >如果未指定登录页面的路径，则在发 [!DNL Experience Manager] 布实例中显示默认登录页面。

1. 发布文件夹，然后尝试从发布实例访问它。 将显示登录屏幕。
1. 如果您是CUG成员，请输入您的安全凭据。 对您进行身份验证后，将 [!DNL Experience Manager] 显示该文件夹。

## 搜索资产 {#assetsearch}

搜索资产对于数字资产管理系统的使用至关重要——无论是供创意人员进一步使用、供业务用户和营销人员对资产进行可靠管理，还是供DAM管理员管理。

要进行简单、高级和自定义搜索以发现和使用最合适的资产，请参 [阅以Experience Manager搜索资产](search-assets.md)。

## 快速操作 {#quick-actions}

快速操作图标一次只能用于单个资产。根据设备，执行以下操作以显示快速操作图标：

* 触控设备：触摸并按住。 例如，在iPad上，您可以点按并按住资产，以便显示快速操作。
* 非触控设备：悬停指针。 例如，在桌面设备上，如果将指针悬停在资产缩略图上，则会显示快速操作栏。

### 导航并选择资产 {#navigating-and-selecting-assets}

您可以使用选择选项视图、导航和选择具有任何可用视图(卡片、列和列表)的 **[!UICONTROL 资产]** 。

在列表视图和列视图中，当 **[!UICONTROL 将指针]** 悬停在资产缩略图上时，将显示选择选项。

![在列表视图中选择资产](assets/select_quick_in_listview.png)

![在列视图中选择资产](assets/select_quick_in_columnview.png)

在卡视图中，选 **[!UICONTROL 择]** (Select)选项显示为快速操作。

![选择卡快速操作视图](assets/select_quick_action.png)

在浏览器中的用户界面中 [!DNL Assets] 浏览文件夹或集合时，可以使用右上角的全选选 [!UICONTROL 择] ，选择所有显示或加载的资产。 最初，只有100个资产以卡视图加载，200个资产以列表视图加载。 滚动搜索结果页面时，将以视图加载更多资产。 全 [!UICONTROL 选] ”选项只选择加载的资产。

有关详细信息，请参 [阅视图和选择资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。

## 编辑图像 {#editing-images}

界面中的编辑工 [!DNL Assets] 具可让您对图像资源执行小型编辑作业。 您可以对图像进行裁剪、旋转、翻转和执行其他编辑作业。 您还可以向资产添加图像映射。

>[!NOTE]
>
>对于某些组件，全屏模式还提供其他可用选项。

1. 执行以下操作之一以在编辑模式下打开资产：

   * 选择资产，然后单击工 **[!UICONTROL 具栏]** 中的编辑。
   * 单击 **[!UICONTROL 卡视图]** 中资产上显示的编辑选项。
   * 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

   ![工具栏中的编辑选项](assets/do-not-localize/edit_icon.png)

1. 要裁剪图像，请单 **[!UICONTROL 击]**![裁剪选项以裁剪图像](assets/do-not-localize/crop.png)。

1. 从列表中选择所需的选项。图像上会根据您选择的选项显示裁剪区域。利用&#x200B;**手绘**&#x200B;选项，您可以不受纵横比限制裁剪图像。

   ![裁剪选项](assets/crop-options.png)

1. 选择要裁剪的区域，并在图像上调整其大小或位置。

1. 使用撤消 **[!UICONTROL 撤消工]** 具栏选 ![项和重](assets/do-not-localize/undo.png) 做工 **[!UICONTROL 具栏选]**![](assets/do-not-localize/redo.png) 项图像，或分别恢复到未裁剪的图像或保留裁剪后的图像。
1. 单击相应 **[!UICONTROL 的“旋]** 转”选项可顺时针或逆时针旋转图像。

   ![顺时针和逆时针旋转选项](assets/do-not-localize/rotate-options.png)

1. 单击相应的“ **[!UICONTROL 翻转]** ”选项，以水平 ![翻转图像水平](assets/do-not-localize/flip-horizontal.png) 反射选项 ![，或垂直](assets/do-not-localize/flip-vertical.png)反射垂直选项。

1. 要完成图像编辑，请单击“完 **[!UICONTROL 成]**![”选项](assets/do-not-localize/check-ok-done-icon.png)。 单击 **完成** ，还会开始再现的再生。

>[!NOTE]
>
>BMP、GIF、PNG和JPEG文件格式支持图像编辑。

You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md).

>[!NOTE]
>
>要编辑TXT文件，请从 **Configuration Manager中设置** Day CQ Link Externalizer。

## 时间轴 {#timeline}

通过时间轴，您可以视图选定项目的各种事件，如资产的活动工作流、注释／注释、活动日志和版本。

![对资产的时间轴条目进行排序](assets/sort_timeline.gif)

*图：对资产的时间轴条目进行排序。*

>[!NOTE]
>
>在“收 [藏集](/help/assets/managing-collections-touch-ui.md#navigating-the-collections-console)”控制台中， **[!UICONTROL “显示全部]** ”列表提供选项，仅用于视图注释和工作流。 此外，时间轴仅对控制台中列出的顶级集合显示。 如果您在任何集合中导航，则不会显示该集合。

>[!NOTE]
>
>时间轴包含特 [定于内容片段的多个选项](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

## 注释资产 {#annotating}

注释是指添加到图像或视频的评论或解释性说明。注释使营销人员能够协作并留下资产反馈。

视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。支持的视频 [!DNL Assets] 格式取决于浏览器。

>[!NOTE]
>
>对于内容片段， [将在片段编辑器中创建注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)。

1. 导航到要添加注释的资产所在的位置。
1. 单击以 **[!UICONTROL 下任]** 一选项中的“注释”(Annotate)选项：

   * [快速操作](/help/assets/managing-assets-touch-ui.md#quick-actions)
   * 在选择资产或导航到资产页面后，从工具栏中

   ![注释选项](assets/annotate-option.png)

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

   ![添加注释对话框中的注释框](assets/annotation-comment-box.png)

1. 要向用户通知有关注释的信息，请指定用户的电子邮件地址并添加评论。 例如，要向 Aaron MacDonald 发送有关注释的通知，请输入 @aa。此时会出现一个列表，其中显示了所有匹配用户的提示。从列表中选择Aaron的电子邮件地址，用评论标记她。 同样，您可以在批注中的任意位置，或批注前后标记更多用户。

   ![指定用户的电子邮件地址并添加注释以通知用户](assets/annotation-add-user-email.png)

   >[!NOTE]
   >
   >对于非管理员用户，仅当用户在CRXDE的路径上具有读取权限时，才 `/home` 会显示建议。

1. After adding the annotation, click **[!UICONTROL Add]** to save it. A notification for the annotation is sent to Aaron.

   ![添加按钮以保存注释](assets/annotation-add.png)

   >[!NOTE]
   >
   >在保存注释之前，可以添加多个注释。

1. Click **[!UICONTROL Close]** to exit from the Annotation mode.
1. To view the notification, log in to [!DNL Assets] with Aaron MacDonald&#39;s credentials and click the **[!UICONTROL Notifications]** option to view the notification.

   >[!NOTE]
   >
   >您也可以对视频资产添加注释。在对视频添加注释时，播放器会暂停，让您对帧添加注释。 有关详细信息，请参 [阅管理视频资产](/help/assets/managing-video-assets.md)。

1. 要选择不同的颜色，以便您能够区分不同的用户，请单击用户档案选项，然后单击“我的 **[!UICONTROL 首选项”]**。

   ![选择用户用户档案选项，然后选择我的首选项以打开用户首选项](assets/User-profile-preferences.png)

   Specify the desired color in the **[!UICONTROL Annotation Color]** box and then click **[!UICONTROL Accept]**.

   ![在用户首选项中选择注释颜色以设置用户角色颜色](assets/Annotation-color.png)

>[!NOTE]
>
>您还可以向集合添加注释。 但是，如果集合包含子集合，则只能向父集合添加注释／注释。 子集合不提供“注释”选项。

### 视图保存的注释 {#viewing-saved-annotations}

1. 要视图已保存的资产注释，请导航到资产所在的位置，然后打开资产页面。

1. 在Experience Manager界面中，选择时 **[!UICONTROL 间轴]**。

   ![时间轴选项在Experience Manager中可用](assets/view-timeline.png)

1. 从时间线的&#x200B;**[!UICONTROL 显示全部]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 注释]**&#x200B;以根据注释过滤结果。

   ![在时间轴中显示所有列表](assets/timeline-show-all-option.png)

   单击“时间轴”面 **[!UICONTROL 板中]** 的注释以视图图像上的相应注释。

   ![视图图像注释的时间轴面板](assets/timeline-view-annotations.png)

   单击 **[!UICONTROL 删除]**，以删除特定注释。

### 打印批注 {#printing-annotations}

如果资产具有批注或已经受审核工作流程的影响，您可以将资产连同批注和审阅状态打印为PDF文件，以便脱机审阅。

您还可以选择仅打印注释或审阅状态。

要打印批注和审阅状态，请单 **[!UICONTROL 击]** “打印”，然后按照向导中的说明操作。 仅当 **[!UICONTROL 资产至]** 少分配了一个注释或审核状态时，才会在工具栏中显示打印选项。

1. 在界面 [!DNL Assets] 中，打开资产的预览页面。
1. 执行下列操作之一：

   * 要打印所有注释和审阅状态，请跳过步骤3并直接转到步骤4。
   * 要打印特定注释和审阅状态，请打 [开时](/help/assets/managing-assets-touch-ui.md#timeline) 间轴，然后转到步骤3。

1. 要打印特定注释，请从时间轴中选择注释。

   ![从时间轴中选择注释以进行打印](assets/timeline-select-annotations.png)

   要仅打印审阅状态，请从时间轴中选择它。

1. Click **[!UICONTROL Print]** from the toolbar.

   ![工具栏中的打印选项](assets/do-not-localize/print.png)

1. 从“打印”对话框中，选择您希望批注／审阅状态在PDF上显示的位置。 例如，如果希望在包含打印图像的页面的右上方打印注释／状态，请使用左 **上方的** 设置。 默认情况下为选中状态。

   ![从“打印”对话框中选择要在PDF上显示的批注／审阅状态的位置](assets/Print-annotation-dialog.png)

   您可以根据希望在打印的 PDF 中显示批注/状态的位置选择其他设置。如果希望批注/状态显示在与打印资产不同的页面中，请选择&#x200B;**[!UICONTROL 下一页]**。

   >[!NOTE]
   >
   >长批注在PDF文件中可能无法正常呈现。 为获得最佳渲染效果，Adobe建议您将注释限制为50字。

1. 单击“ **[!UICONTROL 打印]**”。 根据您在步骤 2 中选择的选项，生成的 PDF 会在指定位置显示批注/状态。例如，如果您选择使用&#x200B;**左上角**&#x200B;设置打印批注和审阅状态，则生成的输出将类似于此处描述的 PDF 文件。

   ![生成的PDF的批注和审阅状态](assets/annotation-status-pdf.png)

1. 下 ![载PDF的](assets/do-not-localize/download.png) “下 ![载”选项或使用右上](assets/do-not-localize/print.png) 方的选项在PDF上打印PDF的打印选项。

   >[!NOTE]
   >
   >如果资产具有子资产，您可以打印所有子资产及其特定的页面注释。

   要修改呈现的PDF文件的外观，例如注释和状态的字体颜色、大小和样式、背景颜色，请从Configuration Manager **[!UICONTROL 中打开]** “注释PDF”配置，并修改所需的选项。 例如，要更改批准状态的显示颜色，请修改相应字段中的颜色代码。 有关更改批注的字体颜色的信息，请参阅 [批注](/help/assets/managing-assets-touch-ui.md#annotating)。

   ![在PDF文档上打印资产注释的配置](assets/annotation-print-pdf-config.png)

   返回渲染的PDF文件并刷新它。 刷新的PDF反映了您所做的更改。

如果资产包含外语（尤其是非拉丁语言）的批注，您必须首先在服务器上配置CQ-DAM-Handler-Gibson字体管理器服务 [!DNL Experience Manager] ，才能打印这些批注。 在配置CQ-DAM-Handler-Gibson字体管理器服务时，请提供所需语言的字体所在的路径。

1. 从URL打开CQ-DAM-Handler-Gibson字体管理器服务配置页 `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`。
1. 要配置CQ-DAM-Handler-Gibson字体管理器服务，请执行下列操作之一：

   * 在“系统字体”目录选项中，指定系统上字体目录的完整路径。 例如，如果您是Mac用户，则可以在“System Fonts”目录选 *项中将路径指定为* /Library/Fonts。 [!DNL Experience Manager] 从此目录中获取字体。
   * 在文件夹内创 `fonts` 建一个名 `crx-quickstart` 为的目录。 CQ-DAM-Handler-Gibson字体管理器服务自动获取位置的字体 `crx-quickstart/fonts`。 您可以从Adobe服务器字体目录选项中覆盖此默认路径。

   * 在系统中为字体创建新文件夹，并将所需的字体存储在该文件夹中。 然后，在Customer Fonts目录选项中指定该文件夹的完整路径。

1. 从URL访问批注PDF配置 `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`。
1. 按照以下方式使用正确的字体系列配置“批注PDF”:

   * 在font- `<font_family_name_of_custom_font, sans-serif>` family选项中包含字符串。 例如，如果要在CJK（中文、日文和韩文）中打印批注，请在字体系列选 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` 项中包含该字符串。 如果要以印地语打印批注，请下载相应的字体并将字体系列配置为Arial Unicode MS、Noto Sans、Noto Sans CJK JP、Noto Sans Devagari、sans-serif。

1. 重新启动 [!DNL Experience Manager] 部署。

下面是如何配置以在CJK( [!DNL Experience Manager] 中文、日文和韩文)中打印批注的示例：

1. 通过以下链接下载Google Noto CJK字体，并将其存储在Font Manager Service中配置的字体目录中。

   * 全部在一个超级CJK字体中： [https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans（适用于欧洲语言）: [https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 您选择的语言的Noto字体： [https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. 通过将font-family参数设置为配置批注PDF文 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`件。 此配置默认可用，适用于所有欧洲和CJK语言。
1. 如果您选择的语言与步骤2中提到的语言不同，请在默认字体系列后面附加一个适当（以逗号分隔）的条目。

## 创建、管理、预览和还原资产版本 {#asset-versioning}

版本控制创建数字资产在某个特定时间点的快照。版本控制有助于在以后将资产恢复到以前的状态。 例如，如果您要撤消对资产所做的更改，请恢复该资产的未编辑版本。 在中 [!DNL Experience Manager]，您可以创建一个版本，视图当前修订版本，视图两个图像版本之间的并排差异，以及将资产恢复到其先前版本。

您可以在以下情 [!DNL Experience Manager] 况下创建版本：

* 上传文件名与同一位置相同的资产。 它可以是新资产或同一资产的已修改版本。
* 在中编辑图 [!DNL Experience Manager] 像并保存更改。
* 编辑资产的元数据。
* 使用 [!DNL Experience Manager] 桌面应用程序签出现有资产、编辑资产并上 [传更改](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets)。

您还可以通过工作流启用自动版本控制。 为资产创建版本时，元数据和演绎版会与该版本一起保存。 演绎版是相同图像的替代内容，例如，已上传JPEG文件的PNG演绎版。

1. 导航到您要为其创建版本的资产所在的位置，然后单击该资产以打开其预览。 从页面的左上角，打开菜单，然后选择时 **[!UICONTROL 间轴]**。

   ![从左侧导航菜单中，选择时间轴选项](assets/timeline.png)

   *图：从页面的左上角区域打开菜单，然后选择“时[!UICONTROL 间轴]”选项。*

1. 要创建资产版本，请执行以下操作：

   * 单击 **[!UICONTROL 底部的]** “操作”。
   * Click **[!UICONTROL Save as Version]** to create a version for the asset. （可选）添加标签和注释。
   * 单击 **[!UICONTROL 创建]** ，以创建版本。

      ![从提要栏创建资产版本](assets/create-new-version-from-timeline.png)

      *图：从时间轴左侧提要栏中创建资[!UICONTROL 产的]版本。*

1. 要视图某个版本的资产，请执行以下操作：

   * 单击“ **[!UICONTROL 在时间轴中]** 显示 [!UICONTROL 全部]”。
   * 单击“ **[!UICONTROL 版本]**”。 为资产创建的所有版本都列在左侧提要栏中。

      ![ 从时间轴中选择版本选项](assets/versions_option.png)

   * 选择资产的特定版本，然后单击 **[!UICONTROL 预览版本]**。

1. 要还原到资产的旧版本，请执行以下操作。 还原后，此版本显示在 [!DNL Assets] 界面中并可供使用。

   * 单击资产的某个版本。 （可选）添加标签和评论。
   * Click **[!UICONTROL Revert to this Version]**.

      ![选择要还原到的版本](assets/select_version.png)

      *图：选择一个版本并还原到它。 它将成为当前版本，DAM用户随后可使用它。*

1. 要比较图像的两个版本，请执行以下步骤：
   * 单击要与当前版本进行比较的版本。
   * 向左拖动滑块，将此版本叠加到当前版本上并进行比较。

   ![使用滑块将资产的选定版本与当前版本进行比较](assets/version-slider.gif)

   *图：使用滑块可轻松将资产的选定版本与当前版本进行比较。*

### 开始资产上的工作流 {#starting-a-workflow-on-an-asset}

要应用工作流来处理资产，请参阅 [开始资产工作流](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset)。

## 收藏集 {#collections}

集合是一组有序的资产。 使用集合在用户之间共享相关资产或将类似资产聚类在一起，以便轻松发现。

* 收藏集可以包含来自不同位置的资产，因为它们只包含对这些资产的引用。 每个收藏集都保持资产的引用完整性。
* 您可以与具有不同权限级别的多个用户共享集合，包括编辑、查看等。

有关集 [合管理的详](/help/assets/managing-collections-touch-ui.md) 细信息，请参阅管理集合。
