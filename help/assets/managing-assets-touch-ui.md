---
title: 使用AEM资产管理数字资产
description: 了解资产管理任务，如上传、下载、编辑、搜索、删除、批注以及对数字资产进行版本管理。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 24c72d79fe1ebd140d7746759d73cbaffdd1ea2d

---


# 管理数字资产 {#managing-assets-with-the-touch-optimized-ui}

本文介绍如何在Adobe Experience Manager(AEM)资产中管理和编辑资产。 要开始使用用户界面和布局，请参阅触 [屏UI的基本处理](/help/sites-authoring/basic-handling.md)。 要管理内容片段，请参阅 [管理内容片段](content-fragments-managing.md) 。

## 创建文件夹 {#creating-folders}

在组织资产集合（例如，所有图像）时，您 `Nature` 可以创建文件夹以将它们放在一起。 您可以使用文件夹对资产进行分类和组织。 AEM资产不要求您组织文件夹中的资产以更好地工作。

>[!NOTE]
>
>* 共享到Marketing Cloud时，不 `sling:OrderedFolder`支持共享类型的“资产”文件夹。 如果要共享文件夹，请勿在创建文件夹 [!UICONTROL 时选择] “已排序”。
>* Experience Manager不允许将单 `subassets` 词用作文件夹的名称。 它是为包含复合资产子资产的节点保留的关键字。


1. 导航到数字资产文件夹中要创建新文件夹的位置。 在菜单中，单击“创 **[!UICONTROL 建”]**。 选择“ **[!UICONTROL 新建文件夹]**”。
1. 在“标 **[!UICONTROL 题]** ”字段中，提供文件夹名称。 默认情况下，DAM使用您提供的标题作为文件夹名称。 创建文件夹后，您可以覆盖默认文件夹并指定其他文件夹名称。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的文件夹会显示在数字资产文件夹中。

不支持以下(以空格分隔的列表)字符：

* 资产文件名中不能包含以下任意字符： `* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称不能包含以下任意字符： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Upload assets {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

您可以将各种类型的资产（包括图像、PDF文件、RAW文件等）从本地文件夹或网络驱动器上传到AEM资产。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，您只能上传文件大小为2 GB或更小的资产。

您可以选择在分配了或没有分配了处理用户档案的情况下将资产上传到文件夹。

对于分配了处理用户档案的文件夹，用户档案名称显示在卡视图的缩略图上。 在列表视图中，用户档案名称显示在“处理 **用户档案** ”列中。 请参阅[处理配置文件](/help/assets/processing-profiles.md)。

在上传资产之前，请确保其格式 [为](/help/assets/assets-formats.md) AEM资产支持的格式。

1. 在“资产”用户界面中，导航到要添加数字资产的位置。
1. 要上传资产，请执行以下操作之一：

   * On the toolbar, tap the **[!UICONTROL Create]** icon. 然后，在菜单中，点按文 **[!UICONTROL 件]**。 如果需要，可以重命名显示的对话框中的文件。
   * 在支持HTML5的浏览器中，直接将资产拖动到“资产”用户界面上。 不显示要重命名文件的对话框。
   ![在aem中创建选项](assets/create-options.png)

   要选择多个文件，请按Ctrl或Command键，然后在文件选取器对话框中选择资产。 使用iPad时，一次只能选择一个文件。

   您可以暂停上传大资产（大于500 MB），稍后从同一页面继续它。 点按上 **** 传开始时显示的进度栏旁边的“暂停”图标。

   ![chlimage_1-211](assets/chlimage_1-5.png)

   可以配置资产大于其大小的资产。 例如，您可以配置系统以将大于1000 MB（而不是500 MB）的资产视为大资产。 在这种情况下，当 **[!UICONTROL 上传大于]** 1000 MB的资产时，进度栏上会显示“暂停”。

   如果上传的文件大于1000 MB且文件小于1000 MB，则“暂停”按钮不显示。 但是，如果取消小于1000 MB的文件上传，将显示“暂 **[!UICONTROL 停]** ”按钮。

   要修改大小限制，请在CRX `chunkUploadMinFileSize` 存储库中 `fileupload`配置节点的属性。

   单击“暂停” **[!UICONTROL 图标]** ，将切换为“播 **[!UICONTROL 放”图标]** 。 要继续上传，请单击“播 **[!UICONTROL 放]** ”图标。

   ![chlimage_1-212](assets/chlimage_1-6.png)

   To cancel an ongoing upload, click close (`X`) next to the progress bar. 当您取消上传操作时，AEM资产会删除部分上传的资产。

   在低带宽情况和网络故障中，恢复上传的功能尤为有用，因为上传大型资产需要很长时间。 您可以暂停上传操作，稍后在情况改善时继续。 在继续时，从您暂停开始的位置上传该内容。

   在上传操作过程中，AEM会将上传的资产部分另存为CRX存储库中的数据块。 上传完成后，AEM会将这些区块合并到存储库中的单个数据块中。

   要为未完成的区块上传作业配置清除任务，请转至 `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`。

   如果上传的资产名称与上传资产时所在位置已可用的资产名称相同，则会显示一个警告对话框。

   您可以选择替换现有资产，创建另一个版本，或者重命名上传的新资产以同时保留两个资产。如果您替换现有资产，则资产的元数据以及您对现有资产所做的任何先前修改（例如注释或裁剪）都将被删除。 如果选择保留这两个资产，则新资产将重命名，并在其名称 `1` 中附加数字。

   ![chlimage_1-213](assets/chlimage_1-7.png)

   >[!NOTE]
   >
   >在“名称冲 **[!UICONTROL 突]** ”对话框中选择  “替换”时，将为新资产重新生成资产ID。 此ID与上一个资产的ID不同。
   >
   >如果启用资产分析功能来跟踪Adobe Analytics的展示次数／点击次数，则重新生成的资产ID将使在Analytics上为资产捕获的数据无效。

   If the asset you upload exists in AEM Assets, the **[!UICONTROL Duplicates Detected]** dialog warns that you are attempting to upload a duplicate asset. 仅当现有资产的二进制文 `SHA 1` 件的校验和值与您上传的资产的校验和值匹配时，才显示该对话框。 在这种情况下，资产名称并不重要。

   >[!NOTE]
   >
   >The [!UICONTROL Duplicates Detected] dialog appears only when the duplicate detection feature is enabled. To enable the duplicate detection feature, see [Enable Duplicate Detection](/help/assets/duplicate-detection.md).

   ![chlimage_1-214](assets/chlimage_1-8.png)

   要在AEM资产中保留重复资产，请点按／单击保 **[!UICONTROL 留]**。 要删除您上传的重复资产，请点按／单击删 **[!UICONTROL 除]**。

   AEM资产可阻止您上传文件名中包含禁止字符的资产。 如果您尝试上传的资产的文件名中包含不允许的字符或更多字符，则AEM资产会显示一条警告消息并停止上传，直到您删除这些字符或上传时使用允许的名称。

   为了适合您组织的特定文件命名约定，您可以在“上 [!UICONTROL 传资产] ”对话框中为上传的文件指定长名。

   但是，不支持以下(以空格分隔的列表)字符：

   * 资产文件名不得包含 `* / : [ \\ ] | # % { } ? &`
   * 资产文件夹名称不能包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`
   ![chlimage_1-215](assets/chlimage_1-10.png)

   此外，资产用户界面还会显示您上传的最近的资产或您首先创建的文件夹。

   如果在上传文件之前取消上传操作，AEM资产将停止上传当前文件并刷新内容。 但是，不会删除已上传的文件。

   AEM资产中的上传进度对话框显示成功上传的文件的计数以及无法上传的文件。

### 串行上传 {#serialuploads}

批量上传大量资产会占用大量I/O资源，这可能会对AEM资产实例的性能产生不利影响。 特别是，如果Internet连接速度较慢，则由于磁盘I/O激增，上传的时间会大大增加。此外，您的Web浏览器可能会对AEM资产可处理的并发资产上传的POST请求数施加其他限制。 因此，上传操作会失败或过早终止。 换句话说，AEM资产在摄取大量文件时可能会丢失某些文件，或完全无法摄取任何文件。

为了克服这种情况，AEM资产在批量上传操作期间一次摄取一个资产（序列上传），而不是同时摄取所有资产。

默认情况下，资产的序列上传处于启用状态。 要禁用该功能并允许并发上传，请在Crx-de `fileupload` 中叠加该节点并将属性的值设 `parallelUploads` 置为 `true`。

### 使用FTP上传资产 {#uploading-assets-using-ftp}

Dynamic Media支持通过FTP服务器批量上传资产。 如果要上传大资产(> 1 GB)或上传整个文件夹和子文件夹，则应使用FTP。 您甚至可以设置FTP上传，以在重复计划的基础上进行。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，您只能上传文件大小为2 GB或更小的资产。

>[!NOTE]
>
>要在Dynamic Media - Scene7模式下通过FTP上传资产，请在AEM作者实例上安装功能包18912。 请联 [系Adobe客户关怀](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) ，获取FP-18912并完成FTP帐户的设置。 有关详细信息，请参 [阅安装功能包18912以批量迁移资产](/help/assets/bulk-ingest-migrate.md)。
>
>如果您使用FTP上传资产，则会忽略在AEM中指定的上传设置。 而是使用Dynamic Media Classic中定义的文件处理规则。

**使用FTP上传资产**

1. 使用您选择的FTP客户端，使用您从供应电子邮件收到的FTP用户名和密码登录到FTP服务器。 在FTP客户端中，将文件或文件夹上传到FTP服务器。
1. [使用从供应电子邮件中收到的凭据](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) ，登录到Dynamic Media Classic。 在全局导航栏上，点按上 **[!UICONTROL 传]**。

1. 在上传页面左上角附近，点按通过FTP选 **[!UICONTROL 项卡]** 。
1. 在页面左侧，选择要从中上传文件的FTP文件夹；在页面的右侧，选择目标文件夹。
1. 在页面的右下角附近，单击“作 **[!UICONTROL 业选项]** ”，然后根据您选择的文件夹中的资产设置所需的选项。

   请参阅 [上传作业选项](#upload-job-options)。

   >[!NOTE]
   >
   >当您通过FTP上传资产时，您在Dynamic Media Classic(S7)中设置的上传作业选项会优先于在AEM中设置的资产处理参数。

1. 在“上传作业选项”对话框的右下角，点按保 **[!UICONTROL 存]**。
1. 在上传页面的右下角，点按提交 **[!UICONTROL 上传]**。

   要视图上传进度，请在全局导航栏上点按作 **[!UICONTROL 业]**。 “作业”页面显示上传的进度。 您可以继续在AEM中工作，并随时返回Dynamic Media Classic中的“作业”页面以查看进行中的作业。
要取消正在进行的上载作业，请点按持 **[!UICONTROL 续时间旁]** 边的取消。

#### 上传作业选项 {#upload-job-options}

| 上传选项 | 子选项 | 描述 |
|---|---|---|
| 作业名称 |  | 在文本字段中预填充的默认名称包括用户输入的名称部分和日期和时间戳。 您可以使用默认名称，或为此上传作业输入您自己创建的名称。 <br>作业以及其他上传和发布作业将记录在“作业”页面上，您可以在该页面中检查作业的状态。 |
| 上传后发布 |  | 自动发布您上传的资产。 |
| 在任意文件夹中覆盖相同的基本资产名称，而不考虑扩展名 |  | 如果希望上传的文件用相同的名称替换现有文件，请选择此选项。 此选项的名称可能不同，具体取决于“应用程序设置 **[!UICONTROL ”>“常规设置”]** >“上传到应用程序” **[!UICONTROL >“覆]**********&#x200B;盖图像”中的设置。 |
| 上传时解压缩Zip或Tar文件 |  |  |
| 作业选项 |  | 点按／单 **[!UICONTROL 击作业选项]** ，打开“上传作 [!UICONTROL 业选项”对话框] ，然后选择影响整个上传作业的选项。 这些选项对于所有文件类型都是相同的。<br>您可以从“应用程序常规设置”页面开始选择上传文件的默认选项。 要打开此页，请选择“设 **[!UICONTROL 置]** ”>“应 **[!UICONTROL 用程序设置”]**。 点按默 **[!UICONTROL 认上传选项]** ，打开上传作 [!UICONTROL 业选项对话框] 。 |
|  | 当 | 选择“一次”或“重复”。 要设置重复作业，请选择“重复”选项（“每日”、“每周”、“每月”或“自定义”），以指定您希望FTP上传作业重复的时间。 然后根据需要指定计划选项。 |
|  | 包含子文件夹 | 上传要上传的文件夹中的所有子文件夹。 您上传的文件夹及其子文件夹的名称将自动输入到AEM资产中。 |
|  | 裁剪选项 | 要从图像的两侧手动裁剪，请选择“裁剪”菜单，然后选择“手动”。 然后输入要从图像的任何一侧或每一侧裁剪的像素数。 裁剪的图像多少取决于图像文件中的 ppi（每英寸像素数）设置。例如，如果图像显示 150 ppi，您在“顶部”、“右”、“底部”和“左”文本框中分别输入 75，则会从每个侧边裁剪半英寸。<br> 要从图像自动裁切空白像素，请打开“裁切”菜单，选择“手动”，然后在“顶部”、“右”、“底部”和“左”字段中输入像素度量值以从两侧进行裁切。 您还可以在“裁剪”菜单上选择“修剪”，然后选择以下选项：<br> **根据** <ul><li>**颜色** -选择颜色选项。 然后选择“角”菜单，并选择图像的角，其颜色最能代表要裁剪的空白颜色。</li><li>**透明度** -选择“透明度”选项。<br> **容差** -拖动滑块可指定从0到1的容差。对于基于颜色的修剪，指定0可仅在像素与您在图像角中选择的颜色完全匹配时裁剪像素。 接近1的数字允许更多的颜色差异。<br>对于基于透明度的修剪，指定0可仅在像素透明时裁剪像素。 接近1的数字可以增加透明度。</li></ul><br>请注意，这些裁剪选项是无损的。 |
|  | 颜色用户档案选项 | 在创建用于投放的优化文件时，选择颜色转换：<ul><li>默认颜色保留：只要图像包含色彩空间信息，就保留源图像颜色；没有颜色转换。 现在几乎所有图像都已嵌入相应的颜色用户档案。 但是，如果CMYK源图像不包含嵌入的颜色用户档案，则这些颜色将转换为sRGB（标准红绿蓝）色彩空间。 sRGB是在网页上显示图像的推荐色彩空间。</li><li>保留原始色彩空间：保留原始颜色，点上不进行任何颜色转换。 对于没有嵌入颜色用户档案的图像，使用“发布”设置中配置的默认颜色用户档案进行任何颜色转换。 颜色用户档案可能与使用此选项创建的文件中的颜色不对齐。 因此，建议您使用“默认颜色保留”选项。</li><li>“自定义自”>“至<br> ”打开菜单，因此您可以选择“转换自”和“转换为色彩空间”。 此高级选项将覆盖嵌入到源文件中的任何颜色信息。 当您提交的所有图像都包含错误或缺少颜色用户档案数据时，请选择此选项。</li></ul> |
|  | 图像编辑选项 | 您可以保留图像中的剪切蒙版，并选择颜色用户档案。<br> 请参阅 [在上传时设置图像编辑选项](#setting-image-editing-options-at-upload)。 |
|  | Postscript选项 | 您可以栅格化PostScript®文件、裁剪文件、保持透明背景、选择分辨率和选择色彩空间。<br> 请参 [阅设置PostScript和Illustrator上传选项](#setting-postscript-and-illustrator-upload-options)。 |
|  | Photoshop选项 | 您可以从Adobe® Photoshop®文件创建模板、维护图层、指定如何命名图层、提取文本以及指定如何将图像定位到模板中。<br> 请注意，AEM中不支持模板。<br> 请参 [阅设置Photoshop上传选项](#setting-photoshop-upload-options)。 |
|  | PDF选项 | 您可以栅格化文件、提取搜索词和链接、自动生成电子目录、设置分辨率和选择色彩空间。<br> 请注意，AEM中不支持eCatalog。 <br> 请参 [阅设置PDF上传选项](#setting-pdf-upload-options)。 |
|  | Illustrator选项 | 您可以栅格化Adobe Illustrator®文件、保持透明背景、选择分辨率和选择色彩空间。<br> 请参 [阅设置PostScript和Illustrator上传选项](#setting-postscript-and-illustrator-upload-options)。 |
|  | EVideo选项 | 您可以通过选择“视频预设”来转码视频文件。<br> 请参 [阅设置eVideo上传选项](#setting-evideo-upload-options)。 |
|  | 批集预设 | 要从上传的文件创建图像集或旋转集，请单击要使用的预设的活动列。 您可以选择多个预设。 您可以在Dynamic Media Classic的“应用程序设置／批量集预设”页中创建预设。<br> 请参 [阅将批集预设配置为自动生成图像集和旋转集](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) ，以了解有关创建批集预设的更多信息。<br> 请参阅 [在上传时设置批集预设](#setting-batch-set-presets-at-upload)。 |

#### 在上传时设置图像编辑选项 {#setting-image-editing-options-at-upload}

上传图像文件（包括AI、EPS和PSD文件）时，您可以在“上传作业选项”对话框中执行 [!UICONTROL 以下编辑操作] :

* 从图像边缘裁切空白（请参阅上表中的说明）。
* 从图像的两侧手动裁切（请参阅上表中的说明）。
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

上传PostScript(EPS)或Illustrator(AI)图像文件时，可以采用各种格式设置这些文件。 您可以栅格化文件、保持透明背景、选择分辨率和选择色彩空间。 在“上传作业选项”对话框的“PostScript选项”和“ [!UICONTROL Illustrator选项”下，可以使用用于设置PostScript和Illustrator文] 件格式的 [!UICONTROL 选项]。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 正在处理 |  | 选择 **[!UICONTROL 栅格化]** ，将文件中的矢量图形转换为位图格式。 |
| 在渲染后的图像中保持透明背景 |  | 保持文件的背景透明度。 |
| 分辨率 |  | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| 色彩空间 |  | 选择“色彩空间”菜单，然后从以下色彩空间选项中进行选择： |
|  | 自动检测 | 保留文件的色彩空间。 |
|  | 强制为RGB | 转换为RGB色彩空间。 |
|  | 强制为CMYK | 转换为CMYK色彩空间。 |
|  | 强制为灰度 | 转换为灰度色彩空间。 |

#### 设置Photoshop上传选项 {#setting-photoshop-upload-options}

Photoshop文档(PSD)文件最常用于创建图像模板。 上传PSD文件时，可以自动从文件创建图像模板(在“上传”屏幕上选 [!UICONTROL 择“创建模板] ”选项)。

如果您使用PSD文件创建模板，Dynamic Media会使用图层从PSD文件创建多个图像；它为每个图层创建一个图像。

使用上述 [!UICONTROL 的“裁剪选项] ”和“ [!UICONTROL 颜色用户档案选项”]，并配以Photoshop上传选项。

>[!NOTE]
>
>AEM中不支持模板。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 维护图层 |  | 将PSD中的图层（如果有）拆分到单个资源中。 资产图层仍与PSD关联。 可以通过在“细节”视图中打开PSD文件并选择图层面板来视图它们。 |
| 创建模板 |  | 从PSD文件中的图层创建模板。 |
| 提取文本 |  | 提取文本，以便用户可以在查看器中搜索文本。 |
| 将图层扩展到背景大小 |  | 将已撕开的图像图层的大小扩展到背景图层的大小。 |
| 图层命名 |  | PSD文件中的图层将作为单独的图像上传。 |
|  | 图层名称 | 在PSD文件中将图像命名为图层名称后面的图像。 例如，原始PSD文件中名为Price Tag的图层将变为名为Price Tag的图像。 但是，如果PSD文件中的图层名称是默认的Photoshop图层名称（背景、图层1、图层2等），则图像将以PSD文件中的图层编号命名，而不是以其默认图层名称命名。 |
|  | Photoshop和图层编号 | 在PSD文件中将图像命名为其图层编号之后，忽略原始图层名称。 图像以Photoshop文件名和附加的图层编号命名。 例如，名为Spring Ad.psd的文件的第二个图层命名为Spring Ad_2，即使它在Photoshop中具有非默认名称。 |
|  | Photoshop和图层名称 | 在PSD文件后面命名图像，后跟图层名称或图层编号。 如果PSD文件中的图层名称是默认的Photoshop图层名称，则使用图层编号。 例如，在名为SpringAd的PSD文件中名为Price Tag的图层被命名为Spring Ad_Price Tag。 具有默认名称Layer 2的图层称为Spring Ad_2。 |
| 锚点 |  | 指定如何在从PSD文件生成的分层合成生成的模板中定位图像。 默认情况下，锚点为中心。 中心锚点允许替换图像最好地填充相同空间，而不管替换图像的长宽比如何。 当引用模板并使用参数替换时，具有替代此图像的不同方面的图像会有效地占据相同的空间。 如果应用程序需要替换图像以填充模板中分配的空间，请更改为其他设置。 |

#### 设置PDF上传选项 {#setting-pdf-upload-options}

上传PDF文件时，可以采用各种格式设置它。 您可以裁切其页面、提取搜索词、输入每英寸像素分辨率并选择色彩空间。 PDF文件通常包含裁切边距、裁切标记、套版色标记和其他打印机标记。 在上传PDF文件时，您可以从页面两侧裁切这些标记。

>[!NOTE]
>
>AEM中不支持eCatalog。

从以下选项中进行选择：

| 选项 | 子选项 | 描述 |
|---|---|---|
| 正在处理 | 栅格化 | （默认）翻页PDF文件中的页面，并将矢量图形转换为位图图像。 选择此选项可创建电子目录。 |
| 提取 | 搜索词 | 从PDF文件提取单词，以便在eCatalog查看器中按关键字搜索文件。 |
|  | 链接 | 从PDF文件中提取链接并将其转换为在eCatalog查看器中使用的图像映射。 |
| 从多页PDF自动生成电子目录 |  | 自动从PDF文件创建电子目录。 eCatalog以您上传的PDF文件命名。 （只有在上传PDF文件时栅格化该文件时，此选项才可用。） |
| 分辨率 |  | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认为 150。 |
| 色彩空间 |  | 选择“色彩空间”菜单，为PDF文件选择色彩空间。 大多数PDF文件都有RGB和CMYK彩色图像。 RGB色彩空间是联机查看的首选。 |
|  | 自动检测 | 保留PDF文件的色彩空间。 |
|  | 强制为RGB | 转换为RGB色彩空间。 |
|  | 强制为CMYK | 转换为CMYK色彩空间。 |
|  | 强制为灰度 | 转换为灰度色彩空间。 |

#### 设置eVideo上传选项 {#setting-evideo-upload-options}

通过从各种视频预设中进行选择来转码视频文件。

| 选项 | 子选项 | 描述 |
|---|---|---|
| 自适应视频 |  | 一个编码预设，可与任何宽高比配合使用，用于创建视频以投放到移动设备、平板电脑和桌面。 使用此预设编码的已上载源视频设置为固定高度。 但是，宽度会自动缩放以保持视频的宽高比。 <br>最佳实践是使用自适应视频编码。 |
| 单个编码预设 | 对编码预设进行排序 | 选择“名称”或“大小”，按名称或分辨率大小对在桌面、手机和平板电脑下列出的编码预设进行排序。 |
|  | 桌面设备 | 创建MP4文件，以便向台式计算机提供流式或渐进式视频体验。选择一个或多个长宽比，其分辨率大小和目标数据速率符合您的要求。 |
|  | 移动设备 | 创建MP4文件，以便在iPhone或Android移动设备上投放。选择一个或多个长宽比，其分辨率大小和目标数据速率为您所需。 |
|  | 平板电脑 | 创建MP4文件，以便在iPad或Android平板电脑设备上投放。选择一个或多个长宽比，其分辨率大小和目标数据速率为您所需。 |

#### 在上传时设置批集预设 {#setting-batch-set-presets-at-upload}

如果要从上传的图像自动创建图像集或旋转集，请单击要使用的预设的活动列。 您可以选择多个预设。

请参 [阅将批集预设配置为自动生成图像集和旋转集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) ，以了解有关创建批集预设的更多信息。

### 流式上传 {#streamed-uploads}

如果您将许多资产上传到AEM，则对服务器的I/O请求会显着增加，这会降低上传效率，甚至会导致某些上传任务超时。 AEM资产支持流式上传资产。 流式上传可避免在将磁盘复制到存储库之前，在服务器上的临时文件夹中存储资产，从而减少上传操作期间的磁盘I/O。 而是直接将数据传输到存储库。 这样，上传大型资产的时间和超时的可能性就会减少。 默认情况下，流式上传在AEM资产中处于启用状态。

>[!NOTE]
>
>对于在JEE服务器上运行的AEM，其servlet-api版本低于3.1，将禁用流上传。

### 提取包含资产的ZIP存档 {#extractzip}

您可以像上传任何其他受支持的资产一样上传ZIP存档。 同一文件名规则适用于ZIP文件。 AEM允许您将ZIP存档解压缩到DAM位置。 如果存档文件不包含ZIP作为扩展名，请使用内容启用文件类型检测。

一次选择一个ZIP存档，单击“提取存 **[!UICONTROL 档”]**，然后选择目标文件夹。 选择一个选项以处理冲突（如果有）。 如果目标文件夹中已存在ZIP文件中的资产，您可以选择以下选项之一：跳过提取、替换现有文件、通过重命名保留两个资源或创建新版本。

提取完成后，AEM会在通知区域通知您。 在AEM提取ZIP时，您可以返回工作，而不会中断提取。

![ZIP提取通知](assets/Zip-extraction-notification.png)

该功能的一些限制是：

* 如果目标位置存在同名的文件夹，则ZIP文件中的资产会解压缩到现有文件夹中。
* 如果取消提取，则不会删除已提取的资产。
* 不能同时选择两个ZIP文件并解压缩它们。 一次只能提取一个ZIP存档。
* 上传ZIP存档时，如果上传对话框显示500服务器错误，请在安装最新的服务包后重试。

## 预览资产 {#previewing-assets}

要预览资产，请执行以下步骤。

1. 在资产用户界面中，导航到要预览的资产所在的位置。
1. 点按所需的资产以将其打开。

1. 在预览模式中，缩放选项可用于支持的图 [像类型](/help/assets/assets-formats.md#supported-raster-image-formats) （通过交互式编辑）。

   要放大资产，请点按／单 `+` 击（或点按／单击资产上的放大镜）。 要缩小，请点按／单击 `-`。 放大时，可以通过平移来仔细查看图像上的任意区域。重置缩放箭头将您带回到原始视图。

   ![上载图标](assets/uploadicon.png)

   Tap **[!UICONTROL Reset]** to reset the view to the original size.

   ![chlimage_1-216](assets/chlimage_1-11.png)

**预览仅使用键盘键的资源**

要使用键盘预览资产，请执行以下步骤：

1. 在资产用户界面中，使用和方向键导航到所需 `Tab` 的资产。

1. 按所 `Enter` 需资产上的键以将其打开。 您可以在预览模式下放大资源。

1. 要放大资产，请执行以下操作：
   1. 使 `Tab` 用键将焦点移动到放大图标。
   1. 使 `Enter` 用键放大图像。
   要缩小，请使 `Tab` 用键将焦点移到缩小图标，然后按 `Enter`。

1. 使 `Shift` 用+ `Tab` 键将焦点移回图像上。

1. 使用箭头键在缩放后的图像周围移动。

See also [Preview Dynamic Media Assets.](/help/assets/previewing-assets.md)

## 编辑属性和元数据 {#editing-properties}

1. 导航到要编辑元数据的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中的]** “属性”以视图资产属性。 或者，选择资产 **[!UICONTROL 卡上的]** “属性”快速操作。

   ![properties_quickaction](assets/properties_quickaction.png)

1. 在“属 [!UICONTROL 性] ”页中，编辑各个选项卡下的元数据属性。 例如，在“基 **[!UICONTROL 本]** ”选项卡下，编辑标题、说明等。

   >[!NOTE]
   >
   >属性页面的布 [!UICONTROL 局] ，以及可用的元数据属性取决于基础元数据模式。 要了解如何修改“属性”页面的布 [!UICONTROL 局] ，请参阅元 [数据模式](/help/assets/metadata-schemas.md)。

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![使用“开始时间”字段中的日期时间选取器或键盘键为资产激活添加日期和时间](assets/schedule-activation.png)

   *图：计划资产激活*

1. 要在特定持续时间后取消激活资产，请从“结束时间”字段旁边的日期选取器中选择取消激 **[!UICONTROL 活日期]** /时间。 取消激活日期应晚于资产的激活日期。 结束 [!UICONTROL 时间后]，资产及其演绎版不能通过资产Web界面或通过HTTP API使用。

   ![使用“结束时间”字段中的日期时间选取器或键盘键，为资产取消激活添加日期和时间](assets/schedule-deactivation.png)

   *图：计划资产取消激活*

1. 在“标 **[!UICONTROL 记]** ”字段中，选择一个或多个标记。 要添加自定义标记，请在框中键入标记的名称，然后按Enter。 新标记将保存在AEM中。 YouTube需要标记才能发布。 See [publish videos to YouTube](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >要创建标记，您需要在CRX存储库中 `/content/cq:tags/default` 的写入权限。

1. 要为资产提供评级，请点按／单击 **[!UICONTROL 高级]** 选项卡，然后点按／单击相应位置的星形以指定所需的评级。

   ![评级](assets/ratings.png)

   您为资产分配的评级分数显示在您的评 **[!UICONTROL 级下]**。 对资产进行评级的用户收到的资产平均评级分数显示在“评 **[!UICONTROL 级”下]**。 此外，对平均评级得分有贡献的评级得分的分解显示在“评级细 **[!UICONTROL 分”下]**。 您可以根据平均评级分数搜索资产。

1. 要视图资产的使用情况统计信息，请单击／点按 **[!UICONTROL Insights]** 选项卡。

   使用情况统计信息包括：

   * 查看或下载资产的次数
   * 渠道/设备，通过这些设备使用资产
   * 最近使用该资产的创意解决方案
   有关详细信息，请参阅 [资产分析](/help/assets/touch-ui-asset-insights.md)。

1. 点按／单击保 **[!UICONTROL 存并关闭]**。
1. 导航到资产用户界面。 已编辑的元数据属性（包括标题、描述、评级等）显示在卡片视图中的资产卡片上以及列表视图中相关列下。

## 复制资产 {#copying-assets}

复制资产或文件夹时，会复制整个资产或文件夹及其内容结构。 复制的资产或文件夹会复制到目标位置。 源位置的资产不会更改。

资产特定副本的一些属性不会结转。 例如：

* 资产ID、创建日期和时间以及版本和版本历史记录。 其中一些属性由属性、 `jcr:uuid`和 `jcr:created`表示 `cq:name`。

* 每个资产及其每个演绎版的创建时间和引用路径都是唯一的。

其他属性和元数据信息将被保留。 复制资产时不会创建部分副本。

1. 从资产UI中，选择一个或多个资产，然后点按／单击工具栏中 **[!UICONTROL 的复制]** 图标。 或者，从资产 **[!UICONTROL 卡中选择]** “复制快速操作”。
   ![copy_icon](assets/copy_icon.png)

   >[!NOTE]
   >
   >如果您使用复 [!UICONTROL 制快速操作] ，则一次只能复制一个资产。

1. 导航到要将资产复制到的位置。

   >[!NOTE]
   >
   >如果您在同一位置复制资产，AEM会自动生成该名称的变体。 For example, if you copy an asset titled `Square`, AEM automatically generates the title for its copy as `Square1`.

1. Click/ tap the **[!UICONTROL Paste]** asset icon from the toolbar.

   ![chlimage_1-219资产](assets/chlimage_1-14.png)随后会复制到此位置。

   >[!NOTE]
   >
   >The **[!UICONTROL Paste]** icon is available in the toolbar until the paste operation is completed.

### 移动或重命名资产 {#moving-or-renaming-assets}

1. 导航到要移动的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中的]** “移动”图标。
   ![move_icon](assets/move_icon.png)

1. 在“移动资产”向导中，执行下列操作之一：

   * 指定资产在移动后的名称。 然后点按／单击 **[!UICONTROL 下一步]** ，以继续。

   * 点按／单 **[!UICONTROL 击取消]** ，以停止该过程。
   >[!NOTE]
   >
   >* 您可以为资产指定相同的名称，前提是新位置中没有使用该名称的资产。但是，如果您将资产移动到存在同名资产的位置，则应使用其他名称。 如果使用相同的名称，系统会自动生成该名称的变体。 例如，如果您的资产的名称为“Square”，则系统会为其副本生成名称“Square1”。
   >* 重命名时，文件名中不允许有空格。


1. On the **[!UICONTROL Select Destination]** dialog, do one of the following:

   * Navigate to the new location for the assets, and then tap/click **[!UICONTROL Next]** to proceed.

   * Tap/click **[!UICONTROL Back]** to return to the **[!UICONTROL Rename]** screen.

1. 如果被移动的资产具有任何引用页面、资产或集合，则“选择目标”选 **[!UICONTROL 项卡旁边将显示]** “调整引 **[!UICONTROL 用”选项卡]** 。

   在“调整引用”屏幕中，执行 **[!UICONTROL 下列操作之一]** :

   * Specify the references to be adjusted based on the new details, and then tap/click **[!UICONTROL Move]** to proceed.

   * From the **[!UICONTROL Adjust]** column, select/unselect references to the assets.
   * Tap/click **[!UICONTROL Back]** to return to the **[!UICONTROL Select Destination]** screen.

   * 点按／单击 **[!UICONTROL 取消]** ，以停止移动操作。
   如果您不更新引用，则它们会继续指向资产的上一个路径。 如果您调整引用，这些引用将更新为新的资产路径。

## 管理再现 {#managing-renditions}

1. 您可以为资产添加或删除演绎版，但原始形式除外。导航到您要为其添加或删除演绎版的资产所在的位置。

1. 点按／单击资产以打开其资产页面。

   ![chlimage_1-220](assets/chlimage_1-15.png)

1. 点按／单击GlobalNav图标，然后从列表中 **[!UICONTROL 选择]** “演绎版”。

   ![renditions_menu](assets/renditions_menu.png)

1. 在&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中，查看为资产生成的演绎版列表。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >默认情况下，AEM资产不会在预览模式下显示资产的原始演绎版。 如果您是管理员，则可以使用叠加将AEM资产配置为在预览模式下显示原始演绎版。

1. 选择一个演绎版以进行查看或删除。

   **删除再现**

   Select a rendition from the **[!UICONTROL Renditions]** panel, and then tap/click the **[!UICONTROL Delete Rendition]** icon from the toolbar.

   ![用于删除再现的选项](assets/delete_renditionicon.png)

   **上传新再现**

   导航到资产的资产详细信息页面，然后点按／单击工具栏中的 **[!UICONTROL 添加演绎版]** ，以上传资产的新演绎版。

   ![chlimage_1-221](assets/chlimage_1-16.png)

   >[!NOTE]
   >
   >如果您从演绎版面板中选 **[!UICONTROL 择了演绎版]** ，工具栏会更改上下文并仅显示与演绎版相关的那些操作。 不显示“上传演绎版”图标等选项。 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以配置要在图像或视频资产的详细信息页面中显示的再现的尺寸。 根据您指定的维，AEM资产会显示具有精确或最接近的维度的再现。

   要在资产详细信息级别配置图像的演绎版尺寸，请叠 `renditionpicker` 加节点(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)并配置width属性的值。 配置属性大 **[!UICONTROL 小（长）(以KB]** )代替宽度，以根据图像大小在资产详细信息页面上自定义再现。 对于基于大小的自定义，如果匹 `preferOriginal` 配的再现的大小大于原始再现，则属性会为原始再现分配首选项。

   同样，您也可以通过覆盖来自定义“注释”页面图像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`。

   ![chlimage_1-222](assets/chlimage_1-17.png)

   要为视频资产配置再现维度，请导航到CRX存储库中位于 `videopicker` 该位置的节点，覆盖该节点 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`，然后编辑相应的属性。

   >[!NOTE]
   >
   >视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。此外，该功能支持不同的视频格式，具体视浏览器而定。

有关生成和查看子资产的详细信息，请参阅 [管理子资产](managing-linked-subassets.md#generate-subassets)。

## Delete assets {#deleting-assets}

要从其他页面解析或删除传入的引用，请在删除资产之前更新相关引用。

此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产和离开断开的链接。

1. 导航至要删除的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中]** 的删除图标。

   ![delete_icon](assets/delete_icon.png)

1. 在确认对话框中，单击：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 删除]**，以确认操作：

      * 如果资产没有引用，则资产会被删除。
      * 如果资产具有引用，则会出现一条错误消息，通知您&#x200B;**一个或多个资产被引用**。您可以选择&#x200B;**[!UICONTROL 强制删除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。
   >[!NOTE]
   >
   >要删除资产，用户需要具有的删除权限 `dam/asset`。 如果您只具有修改权限，则只能编辑资产元数据并向资产添加注释。 但是，您无法删除资产或其元数据。

   >[!NOTE]
   >
   >要从其他页面解析或删除传入的引用，请在删除资产之前更新相关引用。 此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产和离开断开的链接。

## 下载资产 {#downloading-assets}

See [Download assets from AEM](/help/assets/download-assets-from-aem.md).

## Publish assets {#publishing-assets}

>[!NOTE]
>
>有关Dynamic Media的详细信息，请参阅发 [布Dynamic Media资产。](/help/assets/publishing-dynamicmedia-assets.md)

1. 导航到要发布的资产／文件夹所在的位置

1. 从资产卡中选择&#x200B;**[!UICONTROL 发布]**&#x200B;以进行快速操作，或选择资产，然后点按/单击工具栏中的&#x200B;**[!UICONTROL 快速发布]**&#x200B;图标。
1. 如果资产引用了其他资产，向导中便会列出这些引用。只显示自上次发布／取消发布以来未发布或已修改的引用。 选择要发布的引用。

   >[!NOTE]
   >
   >空文件夹（属于您已发布的文件夹的一部分）不会发布。

1. Tap/click **[!UICONTROL Publish]** to confirm the activation for the assets.

>[!CAUTION]
>
>如果您发布的资产正在被处理，则仅会发布原始内容。 缺少再现。 等待处理完成，然后在处理完成后发布或重新发布资产。

## 取消发布资产 {#unpublishing-assets}

1. 导航到要从发布环境（取消发布）中删除的资产／资产文件夹的位置。

1. 选择要取消发布的资产／文件夹，然后点按／单击工 **[!UICONTROL 具栏中的管理发布]** 图标。

   ![manage_publication](assets/manage_publication.png)

1. 从列表 **[!UICONTROL 中选择]** “取消发布”操作。

   ![unpublish_action](assets/unpublish_action.png)

1. To unpublish the asset later, select **[!UICONTROL Unpublish Later]**, and then select a date for unpublishing the asset.
1. 计划一个资产在发布环境中不再可用的日期。
1. 如果资产引用了其他资产，请选择要取消发布的引用。 点按／单击取 **[!UICONTROL 消发布]**。
1. 在确认对话框中，点按／单击：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 取消发布]** ，以确认在指定日期已取消发布资产(在发布环境中不再可用)。
   >[!NOTE]
   >
   >取消发布复杂资产时，仅取消发布该资产。请避免取消发布引用，因为可能其他已发布的资产也引用了这些内容。

## 已关闭的用户组 {#closed-user-group}

已关闭的用户组(CUG)用于限制对从AEM发布的特定资产文件夹的访问。 如果为文件夹创建了CUG，则仅对分配的成员或用户组具有对文件夹（包括文件夹资源和子文件夹）的访问权限。 要访问文件夹，他们必须使用其安全凭据登录。

CUG是限制对资产访问的额外方式。 您还可以为文件夹配置登录页面。

1. 从资产UI中选择一个文件夹，然后点按／单击工具栏中的属性图标以显示属性页面。
1. 从“权 **[!UICONTROL 限]** ”选项卡，在“已关闭的用户组”下添加 **[!UICONTROL 成员或组]**。

   ![add_user](assets/add_user.png)

1. 要在用户访问文件夹时显示登录屏幕，请选择“启 **[!UICONTROL 用]** ”选项。 然后，在AEM中选择登录页面的路径，并保存更改。

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >如果未指定登录页面的路径，AEM将在发布实例中显示默认登录页面。

1. 发布文件夹，然后尝试从发布实例访问它。 将显示登录屏幕。
1. 如果您是CUG成员，请输入您的安全凭据。 AEM对您进行身份验证后，将显示该文件夹。

## 搜索资产 {#assetsearch}

搜索资产是数字资产管理系统使用的核心——无论是供创意人员进一步使用、供商业用户和营销人员对资产进行可靠管理还是供DAM管理员管理。

要进行简单、高级和自定义搜索以发现和使用最合适的资产，请参阅 [在AEM中搜索资产](search-assets.md)。

## 快速操作 {#quick-actions}

快速操作图标一次只能用于单个资产。根据设备的不同，执行以下操作以显示快速操作图标：

* 触控设备：触控并按住。 例如，在iPad上，您可以点按并按住资产，以便显示快速操作。
* 非触控设备：悬停指针。 例如，在桌面设备上，如果将指针悬停在资产缩略图上，则会显示快速操作栏。

### 导航并选择资产 {#navigating-and-selecting-assets}

您可以使用“选择”选项视图、导航和选择具有任何可用视图(卡片、列和列表)的 **[!UICONTROL 资产]** 。

在列表视图和列视图中，当您将指针悬停在资 **[!UICONTROL 产缩略图上时]** ，将显示选择选项。

![select_quick_in_listview](assets/select_quick_in_listview.png)

![select_quick_in_columnview](assets/select_quick_in_columnview.png)

在卡视图中，“选 **[!UICONTROL 择]** ”选项显示为快速操作。

![select_quick_action](assets/select_quick_action.png)

在浏览器中的“资产”用户界面中浏览文件夹或收藏集时，您可以使用右上角的“全选”选项选择所有显示或加载的资产  。 如果不在下方滚动，则卡视图中仅加载100个资源，列表视图中加载200个资源。 选择全部选项将仅选择这些资产。

有关详细信息，请参阅 [视图和选择资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。

## 编辑图像 {#editing-images}

AEM资产界面中的编辑工具可让您对图像资产执行小型编辑作业。 您可以对图像进行裁剪、旋转、翻转和执行其他编辑作业。 您还可以向资产添加图像映射。

>[!NOTE]
>
>对于某些组件，全屏模式还有其他可用选项。

1. 执行以下操作之一以在编辑模式下打开资产：

   * 选择资产，然后单击／点按工 **[!UICONTROL 具栏中]** 的编辑图标。
   * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
   * 在资产页面中，点按／单击工 **[!UICONTROL 具栏中]** 的编辑图标。
   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-22.png)

1. 从列表中选择所需的选项。图像上会根据您选择的选项显示裁剪区域。利用&#x200B;**手绘**&#x200B;选项，您可以不受纵横比限制裁剪图像。

   ![chlimage_1-227](/help/assets/assets/chlimage_1-23.png)

1. 选择要裁剪的区域，并在图像上调整其大小或位置。
1. 使用“ **完成** ”图标（右上角）裁剪图像。 Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-24.png)

1. 使用右 **上角的** “撤消”和 **** “重做”图标分别恢复到未裁剪的图像或保留裁剪的图像。

   ![chlimage_1-229](assets/chlimage_1-25.png)

1. 点按／单击相应的旋转图标以顺时针或逆时针旋转图像。

   ![chlimage_1-230](assets/chlimage_1-26.png)

1. 点按／单击相应的翻转图标，以水平或垂直翻转图像。

   ![chlimage_1-231](assets/chlimage_1-27.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-28.png)

>[!NOTE]
>
>BMP、GIF、PNG和JPEG文件格式支持图像编辑。

You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md).

>[!NOTE]
>
>要编辑TXT文件，请从“配置 **管理器”中设置Day CQ Link Externalizer** 。

## 时间轴 {#timeline}

时间轴允许您视图选定项目的各种事件，如资产的活动工作流、注释／注释、活动日志和版本。

![对资产的时间轴条目进行排序](assets/sort_timeline.gif)

*图：对资产的时间轴条目进行排序*

>[!NOTE]
>
>在“收 [藏集”控制台](/help/assets/managing-collections-touch-ui.md#navigating-the-collections-console),“显示全 **** 部”列表提供了仅用于视图注释和工作流的选项。 此外，时间轴仅对控制台中列出的顶级集合显示。 如果您在任何集合中导航，则不会显示该集合。

>[!NOTE]
>
>时间轴包含特 [定于内容片段的多个选项](/help/assets/content-fragments-managing.md#timeline-for-content-fragments)。

## 注释资产 {#annotating}

注释是指添加到图像或视频的评论或解释性说明。通过注释，营销人员可以协作并保留有关资产的反馈。

视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。AEM资产支持的视频格式取决于浏览器。

>[!NOTE]
>
>对于内容片段， [将在片段编辑器中创建注释](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)。

1. 导航到要添加注释的资产所在的位置。
1. 点按／单击以 **[!UICONTROL 下任一]** :

   * [快速操作](/help/assets/managing-assets-touch-ui.md#quick-actions)
   * 在选择资产或导航到资产页面后，从工具栏中
   ![chlimage_1-233](assets/chlimage_1-29.png)

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

   ![chlimage_1-234](assets/chlimage_1-30.png)

1. 要向用户通知注释，请指定用户的电子邮件地址并添加评论。 例如，要向 Aaron MacDonald 发送有关注释的通知，请输入 @aa。此时会出现一个列表，其中显示了所有匹配用户的提示。从列表中选择Aaron的电子邮件地址，用评论标记她。 同样，您可以在注释内的任意位置或注释前后标记更多用户。

   >[!NOTE]
   >
   >对于非管理员用户，仅当用户在Crx-de中具有“在 */home* ”的“读取”权限时，才显示建议。

   ![chlimage_1-235](assets/chlimage_1-31.png)

1. After adding the annotation, click **[!UICONTROL Add]** to save it. A notification for the annotation is sent to Aaron.

   ![chlimage_1-236](assets/chlimage_1-32.png)

   >[!NOTE]
   >
   >在保存注释之前，可以添加多个注释。

1. Tap/click **[!UICONTROL Close]** to exit from the Annotation mode.
1. To view the notification, log in to AEM Assets with Aaron MacDonald&#39;s credentials and click the **[!UICONTROL Notifications]** icon to view the notification.

   >[!NOTE]
   >
   >您也可以对视频资产添加注释。在对视频添加注释时，播放器会暂停，让您在帧上添加注释。 有关详细信息，请参 [阅管理视频资产](/help/assets/managing-video-assets.md)。

1. 要选择不同的颜色以便您能够区分不同的用户，请单击／点按用户档案图标，然后单击／点按我的 **[!UICONTROL 首选项]**。

   ![选择用户用户档案图标，然后选择我的首选项以打开用户首选项](assets/User-profile-preferences.png)

   在&#x200B;**[!UICONTROL 批注颜色]**&#x200B;框中指定所需颜色，然后单击/点按&#x200B;**[!UICONTROL 接受]**。

   ![在“用户首选项”中选择注释颜色以设置用户角色颜色](assets/Annotation-color.png)

>[!NOTE]
>
>您还可以向集合添加注释。 但是，如果集合包含子集合，则只能向父集合添加注释／注释。 “注释”选项对子集合不可用。

### 视图保存的注释 {#viewing-saved-annotations}

1. 要视图已保存的资产注释，请导航到资产所在的位置，然后打开资产的资产页面。

1. 点按／单击GlobalNav图标，然后从列表中 **[!UICONTROL 选择]** “时间轴”。

   ![chlimage_1-239](assets/chlimage_1-35.png)

1. 从时间线的&#x200B;**[!UICONTROL 显示全部]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 注释]**&#x200B;以根据注释过滤结果。

   ![chlimage_1-240](assets/chlimage_1-36.png)

   点按／单击“时间轴”面板中 **[!UICONTROL 的注释]** ，以视图图像上的相应注释。

   ![chlimage_1-241](assets/chlimage_1-37.png)

   点按／单击 **[!UICONTROL 删除]**，以删除特定注释。

### 打印批注 {#printing-annotations}

如果资产有注释或已受到审阅工作流程的影响，您可以将资产连同注释和审阅状态打印为PDF文件，以便脱机审阅。

您还可以选择仅打印注释或审阅状态。

要打印注释和审阅状态，请点按／单击“打 **[!UICONTROL 印]** ”图标，然后按照向导中的说明操作。 仅当 **[!UICONTROL 资产至少分配了一个注释或审核状态时]** ,“打印”图标才会显示在工具栏中。

1. 从资产UI中，打开资产的预览页面。
1. 执行下列操作之一：

   * 要打印所有注释和审阅状态，请跳过步骤3并直接转到步骤4。
   * 要打印特定注释和审阅状态，请打开时 [间轴](/help/assets/managing-assets-touch-ui.md#timeline) ，然后转到步骤3。

1. 要打印特定注释，请从时间轴中选择注释。

   ![chlimage_1-242](assets/chlimage_1-38.png)

   要仅打印审阅状态，请从时间轴中选择它。

   ![chlimage_1-243](assets/chlimage_1-39.png)

1. Tap/click the **[!UICONTROL Print]** icon from the toolbar.

   ![chlimage_1-244](assets/chlimage_1-40.png)

1. 从“打印”对话框中，选择您希望批注／审阅状态在PDF上显示的位置。 例如，如果希望在包含打印图像的页面的右上方打印注释／状态，请使用左 **上角设置** 。 默认情况下，它处于选中状态。

   ![从“打印”对话框中选择要在PDF上显示的注释／审阅状态的位置](assets/Print-annotation-dialog.png)

   您可以根据希望在打印的 PDF 中显示批注/状态的位置选择其他设置。如果希望批注/状态显示在与打印资产不同的页面中，请选择&#x200B;**[!UICONTROL 下一页]**。

   >[!NOTE]
   >
   >冗长的批注可能无法在PDF文件中正确呈现。 为获得最佳渲染效果，Adobe建议您将注释限制为50个字。

1. 点按/单击&#x200B;**[!UICONTROL 打印]**。根据您在步骤 2 中选择的选项，生成的 PDF 会在指定位置显示批注/状态。例如，如果您选择使用&#x200B;**左上角**&#x200B;设置打印批注和审阅状态，则生成的输出将类似于此处描述的 PDF 文件。

   ![chlimage_1-246](assets/chlimage_1-42.png)

1. 使用右上角的选项下载或打印PDF。

   ![chlimage_1-247](assets/chlimage_1-43.png)

   >[!NOTE]
   >
   >如果资产包含子资产，您可以打印所有子资产及其特定的页面注释。

   要修改渲染后的PDF文件的外观（例如，注释和状态的字体颜色、大小和样式、背景颜色），请从“配置管理器”中打开“注释 **[!UICONTROL PDF]** ”配置，并修改所需的选项。 例如，要更改批准状态的显示颜色，请修改相应字段中的颜色代码。 有关更改注释的字体颜色的信息，请参阅 [注释](/help/assets/managing-assets-touch-ui.md#annotating)。

   ![chlimage_1-248](assets/chlimage_1-44.png)

   返回渲染的PDF文件并刷新它。 刷新的PDF反映了您所做的更改。

如果资产包含外语（尤其是非拉丁语言）的批注，您必须首先在AEM服务器上配置CQ-DAM-Handler-Gibson字体管理器服务，以便能够打印这些批注。 在配置CQ-DAM-Handler-Gibson字体管理器服务时，请提供所需语言的字体所在的路径。

1. 从URL打开CQ-DAM-Handler-Gibson字体管理器服务配置页 `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`。
1. 要配置CQ-DAM-Handler-Gibson字体管理器服务，请执行下列操作之一：

   * 在“系统字体”目录选项中，指定系统上字体目录的完整路径。 例如，如果您是Mac用户，则可以在“系统字体”目录选项中将路径指定为 */Library* /Fonts。 AEM从此目录中获取字体。
   * 在文件夹内创建 `fonts` 一个名 ``crx-quickstart`` 称目录。 CQ-DAM-Handler-Gibson字体管理器服务自动获取位置的字体 `crx-quickstart/fonts`。 您可以从Adobe Server Fonts目录选项中覆盖此默认路径。

   * 为系统中的字体创建一个新文件夹，并将所需的字体存储在该文件夹中。 然后，在“客户字体”目录选项中指定该文件夹的完整路径。

1. 从URL访问注释PDF配置 `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`。
1. 按照以下方式使用正确的字体系列配置“注释PDF”:

   * 在字体系 `<font_family_name_of_custom_font, sans-serif>` 列选项中包含该字符串。 例如，如果要在CJK（中文、日文和韩文）中打印批注，请在字体系列选 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` 项中包含该字符串。 如果要以印地语打印注释，请下载相应的字体并将字体系列配置为Arial Unicode MS、Noto Sans、Noto Sans CJK JP、Noto Sans Devagari、sans-serif。

1. 重新启动AEM实例。

以下是如何配置AEM以在CJK（中文、日文和韩文）中打印注释的示例：

1. 通过以下链接下载Google Noto CJK字体，并将其存储在Font Manager Service中配置的字体目录中。

   * 所有字体都在一个超级CJK字体中： [https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans（针对欧洲语言）: [https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 您选择的语言无需字体： [https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. 通过将font-family参数设置为，配置注释PDF文件 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`。 此配置默认可用，适用于所有欧洲语言和CJK语言。
1. 如果您选择的语言与第2步中提到的语言不同，请在默认字体系列后面附加相应的（以逗号分隔）条目。

## 创建、管理、预览和还原资产版本 {#asset-versioning}

版本控制创建数字资产在某个特定时间点的快照。版本控制有助于在以后将资产恢复到以前的状态。 例如，如果要撤消对资产所做的更改，请恢复该资产的未编辑版本。 在Experience Manager中，您可以创建一个版本，视图当前修订版本，视图两个图像版本之间的并排差异，并将资产恢复到先前版本。

您可以在以下情况下在Experience Manager中创建版本：

* 上传文件名与同一位置相同的资产。 它可以是新资产或同一资产的修改版本。
* 在Experience Manager中编辑图像并保存更改。
* 编辑资产的元数据。
* 使用AEM桌面应用程序签出现有资产、编辑资产并上 [传更改](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets)。

您还可以通过工作流启用自动版本控制。 为资产创建版本时，元数据和演绎版会与版本一起保存。 演绎版是相同图像的替代格式，例如，已上载JPEG文件的PNG演绎版。

1. 导航到您要为其创建版本的资产所在的位置，然后单击该资产以打开其预览。 从页面的左上角，打开菜单，然后选择时间 **[!UICONTROL 轴]**。

   ![从左侧导航菜单中，选择时间轴选项](assets/timeline.png)

   *图：从页面的左上角区域打开菜单，然后选择“时[!UICONTROL 间轴]”选项。*

1. 要创建资产版本，请执行以下操作：

   * 单击底 **[!UICONTROL 部的]** “操作”。
   * Click **[!UICONTROL Save as Version]** to create a version for the asset. （可选）添加标签和注释。
   * 单击 **[!UICONTROL 创建]** ，以创建版本。

      ![chlimage_1-251](assets/create-new-version-from-timeline.png)

      *图：从时间轴左侧提要栏中创建资[!UICONTROL 产的版]本。*

1. 要视图某个版本的资产，请执行以下操作：

   * 单击“ **[!UICONTROL 在时间轴中]** 显示 [!UICONTROL 全部”]。
   * 单击“ **[!UICONTROL 版本]**”。 为资产创建的所有版本均列在左侧提要栏中。

      ![versions_option](assets/versions_option.png)

   * 选择资产的特定版本，然后单击 **[!UICONTROL 预览版本]**。

1. 要还原到资产的旧版本，请执行以下操作。 还原后，此版本将显示在界 [!DNL Assets] 面中并可供使用。

   * 单击资产的某个版本。 （可选）添加标签和评论。
   * Click **[!UICONTROL Revert to this Version]**.

      ![select_version](assets/select_version.png)

      *图：选择一个版本并恢复到它。 它成为DAM用户随后可用的当前版本。*

1. 要比较某个图像的两个版本，请执行以下步骤：
   * 单击要与当前版本进行比较的版本。
   * 向左拖动滑块可将此版本叠加到当前版本上并进行比较。
   ![使用滑块将资产的选定版本与当前版本进行比较](assets/version-slider.gif)

   *图：使用滑块可轻松地将资产的选定版本与当前版本进行比较。*

### 开始资产上的工作流 {#starting-a-workflow-on-an-asset}

要应用工作流来处理资产，请参阅 [开始资产工作流](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset)。

## 收藏集 {#collections}

集合是一组有序的资产。 使用集合在用户之间共享相关资产或将类似资产聚类在一起，以便轻松发现。

* 收藏集可以包含来自不同位置的资产，因为这些资产只包含对这些资产的引用。 每个集合都保持资产的引用完整性。
* 您可以与具有不同权限级别（包括编辑、查看等）的多个用户共享集合。

有关集 [合管理的详细信息](/help/assets/managing-collections-touch-ui.md) ，请参阅管理集合。
